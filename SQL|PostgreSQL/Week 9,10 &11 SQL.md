
# Practical 2: Building a Social Media UI with Shiny and PostgreSQL

## 1. Practical Overview

**Topic:** Building a User Interface with R Shiny  
**Platform:** Posit Cloud (RStudio)  
**Database:** PostgreSQL  
**Duration:** 90 minutes  
**Prerequisite:** Completion of the PostgreSQL schema and CRUD practical.

### Learning Objectives

By the end of this practical, students should be able to:

1. Explain the relationship between a database, an application and a user interface.
2. Create a basic Shiny application using R.
3. Connect a Shiny application to a PostgreSQL database.
4. Display database records in a browser-based interface.
5. Insert records into PostgreSQL through UI input fields.
6. Use buttons, dropdowns and tables in Shiny.
7. Refresh the UI when database records change.

---

## 2. Scenario: Build a Social Media Dashboard

In the previous practical, you created a PostgreSQL schema containing three tables:

- `social_app.users`
- `social_app.posts`
- `social_app.likes`

You will now create a small social media dashboard that allows users to interact with this database without writing SQL commands directly.

Imagine a user opens your application in a browser.

They should be able to:

- View published posts.
- See who published each post.
- See how many likes each post has received.
- Create a new post.
- Like an existing post.

### How the Application Works

The application has three main components:

| Component | Technology | Responsibility |
|---|---|---|
| Database | PostgreSQL | Stores users, posts and likes. |
| Application logic | R | Connects to PostgreSQL and processes requests. |
| User interface | Shiny | Displays tables, text fields, dropdowns and buttons. |

The workflow is:

**User action → Shiny input → R code → PostgreSQL → Updated UI**

For example, when a user publishes a post, Shiny captures the text, R sends an SQL `INSERT` statement to PostgreSQL, and the interface refreshes to display the new post.

---

## 3. Step 1: Open Your Existing Posit Cloud Project

1. Sign in to [Posit Cloud](https://posit.cloud/).
2. Open the RStudio project used in the previous PostgreSQL practical.
3. Confirm that the following files are available:

   - `social_media_schema.sql`
   - `social_media_crud.sql`
   - `run_schema.R`

4. Confirm that your PostgreSQL database is accessible.
5. Confirm that the `social_app` schema and its three tables exist.

**Important:** Posit Cloud does not automatically provide a PostgreSQL server. You must use the database connection configured in the previous practical.

---

## 4. Step 2: Install the Required Packages

Open the R Console and run:

```r
install.packages(c("shiny", "DBI", "RPostgres"))
```

Load the packages in your application:

```r
library(shiny)
library(DBI)
library(RPostgres)
```

These packages serve different purposes:

- `shiny`: builds the user interface and application logic.
- `DBI`: provides a standard interface for database operations.
- `RPostgres`: connects R to PostgreSQL.

You only need to install the packages once in your project environment.

---

## 5. Step 3: Prepare Your Database Connection

The application needs to connect to the PostgreSQL database created in the previous practical.

Your database administrator or lecturer should provide the connection details:

- `PGHOST`
- `PGPORT`
- `PGDATABASE`
- `PGUSER`
- `PGPASSWORD`

Use the environment variables configured for your project.

Do not hardcode your database password in the application or commit it to a shared repository.

Test your connection in the R Console:

```r
library(DBI)
library(RPostgres)

con <- dbConnect(
  RPostgres::Postgres(),
  host = Sys.getenv("PGHOST"),
  port = as.integer(Sys.getenv("PGPORT", "5432")),
  dbname = Sys.getenv("PGDATABASE"),
  user = Sys.getenv("PGUSER"),
  password = Sys.getenv("PGPASSWORD"),
  sslmode = "require"
)

dbGetQuery(
  con,
  "SELECT table_name
   FROM information_schema.tables
   WHERE table_schema = 'social_app'
   ORDER BY table_name"
)

dbDisconnect(con)
```

### Expected Result

You should see these three table names:

```text
likes
posts
users
```

If you receive a connection error, verify the credentials, server availability, network access and SSL configuration before proceeding.

---

## 6. Step 4: Create the Shiny Application File

In RStudio:

1. Select **File → New File → R Script**.
2. Save the file as `app.R`.
3. Ensure it is saved in your project directory.

A basic Shiny application has two main parts:

```r
ui <- fluidPage(
  # User interface components
)

server <- function(input, output, session) {
  # Application logic
}

shinyApp(ui = ui, server = server)
```

The `ui` defines what users see.

The `server` defines what happens when users interact with the interface.

The `shinyApp()` function launches the application.

---

## 7. Step 5: Build the User Interface

Replace the contents of `app.R` with the following complete application.

```r
library(shiny)
library(DBI)
library(RPostgres)

# =========================================
# DATABASE CONNECTION
# =========================================

con <- dbConnect(
  RPostgres::Postgres(),
  host = Sys.getenv("PGHOST"),
  port = as.integer(Sys.getenv("PGPORT", "5432")),
  dbname = Sys.getenv("PGDATABASE"),
  user = Sys.getenv("PGUSER"),
  password = Sys.getenv("PGPASSWORD"),
  sslmode = "require"
)

# =========================================
# USER INTERFACE
# =========================================

ui <- fluidPage(

  titlePanel("Social Media Dashboard"),

  p("Explore posts and interact with the community."),

  tabsetPanel(

    # TAB 1: VIEW POSTS
    tabPanel(
      "View Posts",

      h3("Community Posts"),

      actionButton(
        "refresh",
        "Refresh Posts"
      ),

      br(),
      br(),

      tableOutput("posts_table")
    ),

    # TAB 2: CREATE POST
    tabPanel(
      "Create Post",

      h3("Publish a New Post"),

      uiOutput("author_input"),

      textAreaInput(
        "post_content",
        "Post Content",
        placeholder = "What would you like to share?",
        width = "100%",
        rows = 4
      ),

      actionButton(
        "publish",
        "Publish Post"
      ),

      br(),
      br(),

      textOutput("publish_message")
    ),

    # TAB 3: LIKE A POST
    tabPanel(
      "Like a Post",

      h3("Like a Community Post"),

      uiOutput("liker_input"),

      uiOutput("post_input"),

      actionButton(
        "like",
        "Like Post"
      ),

      br(),
      br(),

      textOutput("like_message")
    )
  )
)

# =========================================
# SERVER LOGIC
# =========================================

server <- function(input, output, session) {

  # Refresh trigger
  refresh_count <- reactiveVal(0)

  observeEvent(input$refresh, {
    refresh_count(refresh_count() + 1)
  })

  # Retrieve users from PostgreSQL
  users <- reactive({
    refresh_count()

    dbGetQuery(
      con,
      "SELECT user_id, username
       FROM social_app.users
       ORDER BY username"
    )
  })

  # Retrieve posts and calculate likes
  posts <- reactive({
    refresh_count()

    dbGetQuery(
      con,
      "SELECT
         p.post_id,
         u.username,
         p.content,
         COUNT(l.user_id) AS total_likes
       FROM social_app.posts p
       JOIN social_app.users u
         ON p.user_id = u.user_id
       LEFT JOIN social_app.likes l
         ON p.post_id = l.post_id
       GROUP BY
         p.post_id,
         u.username,
         p.content,
         p.created_at
       ORDER BY p.created_at DESC, p.post_id DESC"
    )
  })

  # Display the posts table
  output$posts_table <- renderTable({
    posts()
  }, striped = TRUE, bordered = TRUE)

  # Generate the author dropdown
  output$author_input <- renderUI({
    user_data <- users()

    selectInput(
      "author_id",
      "Select Author",
      choices = setNames(
        as.character(user_data$user_id),
        user_data$username
      )
    )
  })

  # Publish a post
  output$publish_message <- renderText("")

  observeEvent(input$publish, {

    req(input$author_id)

    content <- trimws(input$post_content)

    if (nchar(content) == 0) {
      output$publish_message <- renderText(
        "Please enter some content."
      )
      return()
    }

    tryCatch({

      dbExecute(
        con,
        "INSERT INTO social_app.posts
           (user_id, content)
         VALUES ($1, $2)",
        params = list(
          as.integer(input$author_id),
          content
        )
      )

      output$publish_message <- renderText(
        "Your post has been published!"
      )

      updateTextAreaInput(
        session,
        "post_content",
        value = ""
      )

      refresh_count(refresh_count() + 1)

    }, error = function(e) {

      output$publish_message <- renderText(
        "The post could not be published. Check the database connection."
      )

    })
  })

  # Generate the user dropdown for likes
  output$liker_input <- renderUI({
    user_data <- users()

    selectInput(
      "liker_id",
      "Who is liking the post?",
      choices = setNames(
        as.character(user_data$user_id),
        user_data$username
      )
    )
  })

  # Generate the post dropdown
  output$post_input <- renderUI({
    post_data <- posts()

    if (nrow(post_data) == 0) {
      return(p("There are no posts to like yet."))
    }

    selectInput(
      "post_id",
      "Select a Post",
      choices = setNames(
        as.character(post_data$post_id),
        paste0(
          "Post ", post_data$post_id,
          " - ", substr(post_data$content, 1, 50)
        )
      )
    )
  })

  output$like_message <- renderText("")

  # Record a like
  observeEvent(input$like, {

    req(input$liker_id, input$post_id)

    tryCatch({

      dbExecute(
        con,
        "INSERT INTO social_app.likes
           (user_id, post_id)
         VALUES ($1, $2)",
        params = list(
          as.integer(input$liker_id),
          as.integer(input$post_id)
        )
      )

      output$like_message <- renderText(
        "Your like has been recorded!"
      )

      refresh_count(refresh_count() + 1)

    }, error = function(e) {

      output$like_message <- renderText(
        "Could not record the like. You may have already liked this post."
      )

    })
  })

}

# =========================================
# CLOSE DATABASE CONNECTION ON EXIT
# =========================================

onStop(function() {
  if (DBI::dbIsValid(con)) {
    DBI::dbDisconnect(con)
  }
})

# =========================================
# RUN APPLICATION
# =========================================

shinyApp(ui = ui, server = server)
```

Save the file.

### Understanding the Interface

The application contains three tabs:

| Tab | Function |
|---|---|
| View Posts | Displays posts, authors and total likes. |
| Create Post | Lets a user select an author and publish content. |
| Like a Post | Lets a user select their account and a post to like. |

The interface uses `tabsetPanel()`, `selectInput()`, `textAreaInput()`, `actionButton()` and `tableOutput()`.

The database queries use parameters for user-entered values rather than inserting text directly into SQL strings.

---

## 8. Step 6: Run the Application

1. Save `app.R`.
2. Confirm that the PostgreSQL connection variables are configured.
3. Confirm that the database contains the three tables and at least one user.
4. Click **Run App** in the RStudio editor.
5. If prompted, choose to run the application in a separate window.
6. Wait for the Shiny interface to appear.

You should see the title:

**Social Media Dashboard**

Below it, you should see three tabs:

- View Posts
- Create Post
- Like a Post

If you receive an error about missing tables, return to the previous practical and execute the schema file.

If the dropdowns are empty, insert sample users and posts into the database.

---

## 9. Step 7: Test the Application

### Test A: View Posts

1. Open the View Posts tab.
2. Observe the list of posts.
3. Identify the author of each post.
4. Check the number of likes displayed for each post.
5. Click Refresh Posts.

**Expected result:** The interface displays records retrieved from PostgreSQL.

### Test B: Create a Post

1. Open the Create Post tab.
2. Select an author.
3. Type a message, such as:

   `Today I learned how Shiny connects to PostgreSQL!`

4. Click Publish Post.
5. Return to View Posts.
6. Click Refresh Posts if necessary.

**Expected result:** The new post appears in the posts table.

### Test C: Like a Post

1. Open the Like a Post tab.
2. Select the user who will like the post.
3. Select a post.
4. Click Like Post.
5. Return to View Posts.

**Expected result:** The like count for that post increases.

### Test D: Prevent Duplicate Likes

1. Select the same user again.
2. Select the same post.
3. Click Like Post.

**Expected result:** PostgreSQL rejects the duplicate because of the composite primary key in the Likes table. The application displays an error message.

---

## 10. Step 8: Understand the Shiny Code

### A. What is `fluidPage()`?

```r
ui <- fluidPage(
  titlePanel("Social Media Dashboard")
)
```

`fluidPage()` creates a responsive page layout, while `titlePanel()` displays the page title.

### B. What is `selectInput()`?

```r
selectInput(
  "author_id",
  "Select Author",
  choices = c("Amina" = "1", "Brian" = "2")
)
```

It creates a dropdown menu.

The first argument is the input ID. Shiny uses this ID to access the selected value through `input$author_id`.

### C. What is `actionButton()`?

```r
actionButton("publish", "Publish Post")
```

It creates a button that users can click to trigger an action.

The server responds to the click through:

```r
observeEvent(input$publish, {
  # Execute application logic
})
```

### D. What is `renderTable()`?

```r
output$posts_table <- renderTable({
  posts()
})
```

It displays data retrieved from the database in a table within the interface.

### E. What is `reactive()`?

```r
posts <- reactive({
  dbGetQuery(con, "SELECT * FROM social_app.posts")
})
```

A reactive expression retrieves and updates data when its reactive dependencies change.

In this application, `refresh_count()` triggers the posts query to run again after an update or when the refresh button is clicked.

### F. How Does Shiny Insert Data into PostgreSQL?

```r
dbExecute(
  con,
  "INSERT INTO social_app.posts (user_id, content)
   VALUES ($1, $2)",
  params = list(1, "My first Shiny post")
)
```

The SQL statement inserts a new record. The values are supplied separately through parameters.

This is safer than constructing SQL by joining user input directly into the query string.

---

## 11. Step 9: Practical Exercises

Complete the following tasks individually.

### Exercise 1: Improve the Interface (2 marks)

Change the page title to:

`ADMI Social Community`

Add a short welcome message below the title.

### Exercise 2: Add a Search Feature (2 marks)

Add a text input that allows users to search posts by content.

The posts table should display only records that match the search term.

### Exercise 3: Display More Information (2 marks)

Modify the posts table to display:
- Post ID
- Username
- Post content
- Date created
- Total likes

### Exercise 4: Improve Feedback (2 marks)

Display a clear message when:
- A post is successfully published.
- A user attempts to publish an empty post.
- A like is successfully recorded.
- A duplicate like is attempted.

### Exercise 5: Explain the Architecture (2 marks)

Write a short explanation of how the following work together:

- PostgreSQL
- R
- Shiny UI
- SQL queries

**Total: 10 marks**

---

## 12. Step 10: Submission Requirements

Submit the following:

1. `app.R` — the Shiny application.
2. `social_media_schema.sql` — the database schema.
3. `social_media_crud.sql` — the SQL CRUD operations.
4. Screenshots of the working interface.
5. A screenshot showing a newly created post.
6. A screenshot showing a like count before and after a like is recorded.
7. Answers to the five practical exercises.

### Reflection Questions

1. What is the difference between a command-line SQL query and a Shiny interface?
2. Why does the application need a database connection?
3. What does `input$publish` represent?
4. What is the purpose of `observeEvent()`?
5. Why should user input be passed to SQL through parameters?
6. How does the application know which user published a post?
7. What happens to the database when the Shiny application closes?

---

## 13. Expected Final Outcome

By the end of the practical, you should have a working browser-based social media dashboard connected to PostgreSQL.

You should be able to view posts, publish new posts, record likes and see database changes reflected in the interface.

You have progressed from writing SQL statements directly to building an application through which a user can interact with the database without writing SQL.

**Key takeaway:** PostgreSQL manages the data, R handles the application logic, and Shiny provides the user interface.
