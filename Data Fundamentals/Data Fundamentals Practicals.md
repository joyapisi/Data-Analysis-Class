

# 🚀 Data Careers Online Curriculum: 10 Practical Projects
This repository contains a structured, hands-on curriculum featuring data roles calibrated strictly to a modern analytics stack: **SQL, Posit Cloud (R, Shiny, Python), Excel, Metricool, GA4, and PostgreSQL**. Roles are strategically repeated across different core technologies to maximize practical skill depth.
---## 📋 Curriculum Overview
| # | Career Path | Project Focus | Core Tools |
|---|:---|:---|:---|
| 1 | [Data Analyst](#1-data-analyst---excel) | Macroeconomic GDP Visualization | Posit Cloud, R, ggplot2 |
| 2 | [Data Analyst](#2-data-analyst---posit-cloud--r) | E-Commerce Sales Performance | Excel / Sheets |
| 3 | [Product Analyst](#3-product-analyst---ga4) | User Acquisition & Checkout Funnel | Google Analytics 4 (GA4) |
| 4 | [Product Analyst](#4-product-analyst---posit-cloud--shiny) | Multi-Step Dynamic Registration App | Posit Cloud, RShiny |
| 5 | [Marketing Data Analyst](#5-marketing-data-analyst---metricool) | Cross-Channel Social ROI Performance | Metricool |
| 6 | [Marketing Data Analyst](#6-marketing-data-analyst---sql) | Ad Spend & Conversion Attribution | PostgreSQL, SQL |
| 7 | [Data Engineer](#7-data-engineer---sql) | Financial Transaction Database Schema | PostgreSQL, SQL |
| 8 | [Data Engineer](#8-data-engineer---posit-cloud) | Automated Scheduled Report Pipeline | Posit Cloud, RMarkdown / Quarto |
| 9 | [Business Analytics Translator](#9-business-analytics-translator---excel) | Cohort Retention & Financial Run Rate | Excel |
| 10 | [Business Analytics Translator](#10-business-analytics-translator---shiny) | Executive Scenario Planning Simulator | Posit Cloud, RShiny |
---

## 🛠️ Career Modules & Practicals

## 1. Data Analyst - Posit Cloud & R*
**Core Focus:** Writing reproducible scripts to fetch, clean, and map global economic indicators.* 
**Online Practical:** **Macroeconomic GDP Trend Visualization**
  * **Tools Needed:** Posit Cloud workspace, R (`tidyverse`, `WDI` or `ggplot2`).
  * **Objective:** Programmatically ingest international development data to calculate historical GDP growth variations across regions.
  * **Deliverable:** An R script file hosted in Posit Cloud that generates an annotated multi-line trend chart and a localized clean summary table.

  ```
//# 1. Install required packages (run these if you haven't installed them yet)
install.packages("WDI")
install.packages("ggplot2")
install.packages("dplyr")
install.packages("scales")

//# 2. Load the libraries
library(WDI)
library(ggplot2)
library(dplyr)
library(scales)

// # 3. Fetch Kenya's GDP data from the WDI API
// # NY.GDP.MKTP.CD = GDP (Current USD)
// # NY.GDP.MKTP.KD.ZG = GDP growth (annual %)
kenya_gdp_data <- WDI(
  country = "KE", 
  indicator = c("gdp_usd" = "NY.GDP.MKTP.CD", "gdp_growth" = "NY.GDP.MKTP.KD.ZG"), 
  start = 1990, 
  end = 2025
)

// # 4. Preview the downloaded data structure
head(kenya_gdp_data)

# ==========================================
# VISUALIZATION 1: Kenya's GDP (Current USD)
# ==========================================
ggplot(kenya_gdp_data, aes(x = year, y = gdp_usd)) +
  geom_line(color = "#006633", size = 1.2) + # Distinct green line
  geom_point(color = "#990000", size = 2) +   # Dark red point indicators
  scale_y_continuous(labels = label_dollar(scale = 1e-9, suffix = "B")) + # Formats to Billions ($B)
  labs(
    title = "Kenya's Gross Domestic Product (GDP) Trend",
    subtitle = "Data source: World Bank World Development Indicators (1990-2025)",
    x = "Year",
    y = "GDP (Current USD)"
  ) +
  theme_minimal(base_size = 13) +
  theme(
    plot.title = element_text(face = "bold", hjust = 0.5),
    plot.subtitle = element_text(hjust = 0.5, color = "gray40"),
    panel.grid.minor = element_blank()
  )

# ==========================================
# VISUALIZATION 2: Annual GDP Growth Rate (%)
# ==========================================
ggplot(kenya_gdp_data, aes(x = year, y = gdp_growth)) +
  geom_col(aes(fill = gdp_growth > 0), show.legend = FALSE) + # Color bars based on positive/negative growth
  scale_fill_manual(values = c("TRUE" = "#006633", "FALSE" = "#990000")) +
  geom_hline(yintercept = 0, color = "black", linetype = "dashed") +
  scale_y_continuous(labels = label_percent(scale = 1/100)) +
  labs(
    title = "Kenya's Annual GDP Growth Rate",
    subtitle = "Data source: World Bank World Development Indicators (1990-2025)",
    x = "Year",
    y = "Annual Growth Rate (%)"
  ) +
  theme_minimal(base_size = 13) +
  theme(
    plot.title = element_text(face = "bold", hjust = 0.5),
    plot.subtitle = element_text(hjust = 0.5, color = "gray40")
  )

  ```
## 2. Data Analyst - Excel*
**Core Focus:** Cleaning transaction records, calculating baseline metrics, and summarizing operational trends.
  * **Online Practical:** **E-Commerce Sales Performance Analysis**
  * **Tools Needed:** Microsoft Excel or Google Sheets.
  * **Objective:** Clean a raw `.csv` transaction export using nested formulas (VLOOKUP/XLOOKUP, IFS) and isolate seasonal sales variations.
  * **Deliverable:** A functional workbook containing automated summary sheets, dynamic Pivot Tables, and a list of underperforming product categories.
```
Transaction_ID,Date,Product_Category,Product_Name,Quantity,Unit_Price,Customer_Region,Payment_Method
TXN_1001,2026-01-15,Electronics,Wireless Headphones,2,89.99,North,Credit Card
TXN_1002,2026-01-16,ELECTRONICS, USB-C Cable ,5,15.50,South,PayPal
TXN_1003,2026-01-16,Clothing,Winter Jacket,1,120.00,East,Credit Card
TXN_1004,2026-01-17,Home & Kitchen, Blender ,1,,West,Debit Card
TXN_1005,2026-01-18,Clothing, Running Shoes ,2,75.00,North,PayPal
TXN_1006,2026-02-01,Home & Kitchen,Coffee Maker,1,45.00,South,Credit Card
TXN_1007,2026-02-02,electronics,Wireless Headphones,1,89.99,West,Crypto
TXN_1008,2026-02-03,Clothing, Winter Jacket ,2,120.00,East,Credit Card
TXN_1009,2026-02-14,Home & Kitchen, Air Fryer ,1,110.00,North,Debit Card
TXN_1010,2026-02-15,Electronics,USB-C Cable,10,15.50,South,PayPal
TXN_1011,2026-03-01,CLOTHING,Running Shoes,1,75.00,West,Credit Card
TXN_1012,2026-03-02,Electronics,Smart Watch,1,,East,Credit Card
TXN_1013,2026-03-12,Home & Kitchen,Blender,2,35.00,North,PayPal
TXN_1014,2026-03-15,Electronics,Wireless Headphones,3,89.99,South,Debit Card
TXN_1015,2026-03-22,Clothing,T-Shirt,5,19.99,West,PayPal
```
This guide provides a structured blueprint and formulas to clean a raw `.csv` transaction export and isolate seasonal sales variations within Microsoft Excel or Google Sheets.

## Identified Data Integrity Issues

Use the DIRTY framework:
**D** - Duplicate records
**I** - Inconnsistent formatting
**R** - Rogue spaces
**T** - Typos and casing
**Y** - Yieldless Blanks

* **Inconsistent Text Casing**: Mixed capitalization across fields (e.g., `ELECTRONICS` vs `electronics`).
* **Hidden Trailing Spaces**: Excess padding in string entries (e.g., `" Blender "`).
* **Missing Value Anomalies**: Blank entries in critical fields like `Unit_Price` (e.g., records `TXN_1004` and `TXN_1012`).

---

## Spreadsheet Blueprint & Formulas

Add the following helper columns to your spreadsheet layout to transform the dirty source data into a standardized analytics layer.

### a. Product Name Sanitization (Column I)
Removes hidden leading and trailing white spaces that break matches.
* **Formula (Cell I2):** 
  ```excel
  =TRIM(D2)
  ```

### b. Missing Unit Price Recovery (Column J)
Employs a logical fallback test leveraging `product_mapping.csv` to replace empty price attributes automatically.
* **Modern Excel Formula (Cell J2):**
  ```excel
  =IF(ISBLANK(F2), XLOOKUP(I2, product_mapping.csv!$A:$A, product_mapping.csv!$C:$C, 0), F2)
  ```
* **Legacy VLOOKUP Alternative (Cell J2):**
  ```excel
  =IF(OR(ISBLANK(F2), F2=""), IFERROR(VLOOKUP(I2, product_mapping.csv!$A:$C, 3, FALSE), 0), F2)
  ```

### c. Total Sales Calculation (Column K)
Calculates gross line items cleanly.
* **Formula (Cell K2):** 
  ```excel
  =E2 * J2
  ```

### d. Seasonal Variance Isolation (Column L)
Uses a nested `IFS` conditional tree to segment dates into calendar seasons based on the ISO text sequence extraction.
* **Formula (Cell L2):** 
  ```excel
  =IFS(
    ISBLANK(B2), "Unknown",
    OR(MONTH(B2)=12, MONTH(B2)<=2), "Winter Peak",
    MONTH(B2)<=5, "Spring Shoulder",
    MONTH(B2)<=8, "Summer Peak",
    MONTH(B2)<=11, "Autumn Shoulder"
  )
  ```

---

## Reference Dataset Output Evaluation

Once populated down all rows, the system evaluates your raw export into the following cleaned structured table matrix:

| Transaction_ID | Date | Product_Category | Cleaned_Product (Col I) | Quantity | Cleaned_Price (Col J) | Total_Sales (Col K) | Season (Col L) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TXN_1001** | 2026-01-15 | Electronics | Wireless Headphones | 2 | 89.99 | 179.98 | Winter Peak |
| **TXN_1002** | 2026-01-16 | ELECTRONICS | USB-C Cable | 5 | 15.50 | 77.50 | Winter Peak |
| **TXN_1003** | 2026-01-16 | Clothing | Winter Jacket | 1 | 120.00 | 120.00 | Winter Peak |
| **TXN_1004** | 2026-01-17 | Home & Kitchen | Blender | 1 | **35.00** *(Looked up)* | 35.00 | Winter Peak |
| **TXN_1005** | 2026-01-18 | Clothing | Running Shoes | 2 | 75.00 | 150.00 | Winter Peak |
| **TXN_1006** | 2026-02-01 | Home & Kitchen | Coffee Maker | 1 | 45.00 | 45.00 | Winter Peak |
| **TXN_1007** | 2026-02-02 | electronics | Wireless Headphones | 1 | 89.99 | 89.99 | Winter Peak |
| **TXN_1008** | 2026-02-03 | Clothing | Winter Jacket | 2 | 120.00 | 240.00 | Winter Peak |
| **TXN_1009** | 2026-02-14 | Home & Kitchen | Air Fryer | 1 | 110.00 | 110.00 | Winter Peak |
| **TXN_1010** | 2026-02-15 | Electronics | USB-C Cable | 10 | 15.50 | 155.00 | Winter Peak |
| **TXN_1011** | 2026-03-01 | CLOTHING | Running Shoes | 1 | 75.00 | 75.00 | Spring Shoulder |
| **TXN_1012** | 2026-03-02 | Electronics | Smart Watch | 1 | **199.99** *(Looked up)* | 199.99 | Spring Shoulder |
| **TXN_1013** | 2026-03-12 | Home & Kitchen | Blender | 2 | 35.00 | 70.00 | Spring Shoulder |
| **TXN_1014** | 2026-03-15 | Electronics | Wireless Headphones | 3 | 89.99 | 269.97 | Spring Shoulder |
| **TXN_1015** | 2026-03-22 | Clothing | T-Shirt | 5 | 19.99 | 99.95 | Spring Shoulder |

## 3. Product Analyst - GA4* 
**Core Focus:** Tracking web traffic conversions, mapping user interactions, and identifying application friction points.* **Online Practical:** 
**User Acquisition & Checkout Funnel Analysis**
  * **Tools Needed:** Google Analytics 4 ([GA4 Demo Account](https://support.google.com/analytics/answer/6367342?hl=en#zippy=%2Cin-this-article) or Test Property).
  * **Objective:** Build a custom exploration funnel to audit where users drop off between viewing an item and finalizing a purchase.
  * **Deliverable:** A GA4 Exploration Funnel report detailing specific stage-to-stage drop-off rates and three data-backed UX recommendations.

  <img width="500" height="375" alt="image" src="https://github.com/user-attachments/assets/e5f58c48-861b-44ce-ba65-0d15ad03e4bc" />
 
### Implementation Steps for Practical 3 (Product Analyst - GA4)
This practical utilizes the official Google Analytics 4 (GA4) Merchandise Store Demonstration Account. Students do not need to configure code snippets or manage a live website deployment to complete this analysis.
### Step 1: Access the Environment

   1. Open a web browser and navigate to the official [Google Analytics Help Center](https://support.google.com/analytics/answer/6366960).
   2. Scroll down to the Access the demo account section and click the link for the GA4 Google Merchandise Store web property.
   3. Log in with any standard Google account credentials.

### Step 2: Open the Explorations Workspace

   1. Locate the left-hand navigation sidebar inside the GA4 interface.
   2. Click on Explore (represented by a blank canvas icon with a trend graph) to bypass standard canned reporting layouts.
   3. Select Blank to spin up an unrestricted custom analytics exploration layout from scratch.
   4. Rename your configuration tab in the top-left section from Untitled Exploration to User Acquisition & Checkout Funnel Analysis.

### Step 3: Configure the Funnel Parameters

   1. Look at the Variables column on the far left. Find Technique and change the drop-down menu setting from Free Form to Funnel Exploration.
   2. Scroll down to the Tab Settings column (the middle column) and locate the Steps configuration panel. Click the Pencil Icon to open the custom funnel step builder modal.

### Step 4: Map Out the Four Funnel Stages
Define the following sequential micro-conversions using standard GA4 event variables within the modal layout:

* Step 1: User Ingestion (Session Start)
* Step Name: Session Started
   * Event Definition: Select session_start from the event dropdown menu.
* Step 2: Product Engagement (View Item)
* Click Add Step.
   * Step Name: Product Viewed
   * Event Definition: Select view_item.
* Step 3: Intent to Purchase (Add to Cart)
* Click Add Step.
   * Step Name: Added to Cart
   * Event Definition: Select add_to_cart.
* Step 4: Final Conversion (Purchase Complete)
* Click Add Step.
   * Step Name: Purchase Completed
   * Event Definition: Select purchase.

Click the blue Apply button in the top right corner of the step builder window.
### Step 5: Isolate Growth Bottlenecks and Formulate Insights

   1. Analyze the automatically generated bar graph visual asset in the main canvas pane.
   2. Record the Abandonment Rate (the red down-arrow metric) calculated between Step 2 (Product Viewed) and Step 3 (Added to Cart). This usually indicates design flaws, confusing pricing displays, or weak call-to-action buttons.
   3. Drag the Session Source/Medium dimension from the Variables column down into the Breakdown box under Tab Settings to group the funnel rows by ad traffic channels. Identify which pipeline channel drops off most aggressively.

### Step 6: Export Your Deliverable

   1. Click the Export Data icon located in the upper right quadrant of the main canvas pane.
   2. Select Google Sheets or CSV to save the tabular row outputs.
   3. Compile these calculations into a clean Markdown document or executive memo summarizing three UI optimization ideas aimed directly at the highest drop-off stage.

## 4. Product Analyst - Posit Cloud & Shiny* 
**Core Focus:** Building front-end web interfaces to capture user inputs and handle structured analytical workflows.* 
**Online Practical:** **Multi-Step Dynamic Registration Form App**
  * **Tools Needed:** Posit Cloud, R Shiny framework.
  * **Objective:** Develop a reactive 3-step sign-up interface that validates inputs (email, age, region) on the fly and simulates database submission status.
  * **Deliverable:** A live UI link and a source `app.R` script processing user form interactions reactively in the cloud.

  #### Step 1
  a. Open your project in Posit Cloud.
b. In the Console pane at the bottom left, install the required packages by running
   
   ```
install.packages(c("shiny", "bslib"))
```
#### Step 2
Replace all default code in your app.R file with the following complete script:

```
library(shiny)
library(bslib)

ui <- page_fluid(
  theme = bs_theme(version = 5, bootswatch = "flatly"),
  
  div(
    style = "max-width: 500px; margin: 50px auto;",
    card(
      card_header(
        h4("Account Registration", class = "mb-0"),
        textOutput("step_indicator", inline = TRUE)
      ),
      card_body(
        # Hidden tabset acts as a multi-step wizard container
        tabsetPanel(
          id = "wizard_steps",
          type = "hidden",
          
          # --- STEP 1: EMAIL ---
          tabPanel(
            "step1",
            h5("Step 1: Contact Information"),
            textInput("email", "Email Address", placeholder = "name@example.com", width = "100%"),
            uiOutput("email_feedback"),
            div(
              class = "d-flex justify-content-end mt-4",
              actionButton("to_step2", "Next", class = "btn-primary", disabled = TRUE)
            )
          ),
          
          # --- STEP 2: AGE ---
          tabPanel(
            "step2",
            h5("Step 2: Age Verification"),
            numericInput("age", "Your Age", value = NA, min = 1, max = 120, width = "100%"),
            uiOutput("age_feedback"),
            div(
              class = "d-flex justify-content-between mt-4",
              actionButton("back_to_1", "Back", class = "btn-secondary"),
              actionButton("to_step3", "Next", class = "btn-primary", disabled = TRUE)
            )
          ),
          
          # --- STEP 3: REGION & SUBMIT ---
          tabPanel(
            "step3",
            h5("Step 3: Regional Preferences"),
            selectInput(
              "region", "Select Your Region",
              choices = c("Choose a region..." = "", "North America", "Europe", "Asia-Pacific", "Africa", "Latin America"),
              width = "100%"
            ),
            uiOutput("region_feedback"),
            hr(),
            uiOutput("summary_box"),
            div(
              class = "d-flex justify-content-between mt-4",
              actionButton("back_to_2", "Back", class = "btn-secondary"),
              actionButton("submit_btn", "Create Account", class = "btn-success", disabled = TRUE)
            )
          ),
          
          # --- STEP 4: SUBMISSION STATUS ---
          tabPanel(
            "step4",
            uiOutput("submission_status_ui")
          )
        )
      )
    )
  )
)

server <- function(input, output, session) {
  
  # Track current step for the header badge
  current_step <- reactiveVal(1)
  
  output$step_indicator <- renderText({
    if (current_step() <= 3) {
      paste("Step", current_step(), "of 3")
    } else {
      "Complete"
    }
  })
  
  # --- 1. ON-THE-FLY EMAIL VALIDATION ---
  is_email_valid <- reactive({
    req(input$email)
    grepl("^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}$", trimws(input$email))
  })
  
  output$email_feedback <- renderUI({
    if (is.null(input$email) || trimws(input$email) == "") {
      return(tags$small(class = "text-muted", "Enter a valid email address to continue."))
    }
    if (is_email_valid()) {
      tags$small(class = "text-success fw-bold", "✓ Valid email format.")
    } else {
      tags$small(class = "text-danger", "✗ Please enter a valid email (e.g., user@domain.com).")
    }
  })
  
  observe({
    valid <- isTRUE(tryCatch(is_email_valid(), error = function(e) FALSE))
    updateActionButton(session, "to_step2", disabled = !valid)
  })
  
  # --- 2. ON-THE-FLY AGE VALIDATION ---
  is_age_valid <- reactive({
    !is.na(input$age) && is.numeric(input$age) && input$age >= 18 && input$age <= 120
  })
  
  output$age_feedback <- renderUI({
    if (is.na(input$age)) {
      return(tags$small(class = "text-muted", "You must be at least 18 years old."))
    }
    if (is_age_valid()) {
      tags$small(class = "text-success fw-bold", "✓ Age verified.")
    } else if (input$age < 18) {
      tags$small(class = "text-danger", "✗ You must be 18 or older to register.")
    } else {
      tags$small(class = "text-danger", "✗ Please enter a realistic age (18–120).")
    }
  })
  
  observe({
    updateActionButton(session, "to_step3", disabled = !is_age_valid())
  })
  
  # --- 3. ON-THE-FLY REGION VALIDATION & SUMMARY ---
  is_region_valid <- reactive({
    !is.null(input$region) && input$region != ""
  })
  
  output$region_feedback <- renderUI({
    if (is_region_valid()) {
      tags$small(class = "text-success fw-bold", paste("✓ Region selected:", input$region))
    } else {
      tags$small(class = "text-muted", "Please select your geographic region.")
    }
  })
  
  output$summary_box <- renderUI({
    req(is_region_valid())
    div(
      class = "alert alert-light border",
      tags$strong("Review Your Details:"),
      tags$ul(
        class = "mb-0 mt-1",
        tags$li(paste("Email:", trimws(input$email))),
        tags$li(paste("Age:", input$age)),
        tags$li(paste("Region:", input$region))
      )
    )
  })
  
  observe({
    updateActionButton(session, "submit_btn", disabled = !is_region_valid())
  })
  
  # --- WIZARD NAVIGATION ---
  observeEvent(input$to_step2, {
    updateTabsetPanel(session, "wizard_steps", selected = "step2")
    current_step(2)
  })
  
  observeEvent(input$back_to_1, {
    updateTabsetPanel(session, "wizard_steps", selected = "step1")
    current_step(1)
  })
  
  observeEvent(input$to_step3, {
    updateTabsetPanel(session, "wizard_steps", selected = "step3")
    current_step(3)
  })
  
  observeEvent(input$back_to_2, {
    updateTabsetPanel(session, "wizard_steps", selected = "step2")
    current_step(2)
  })
  
  # --- 4. SIMULATED DATABASE SUBMISSION ---
  db_status <- reactiveVal("idle")
  
  observeEvent(input$submit_btn, {
    # Switch to status view and set state to saving
    updateTabsetPanel(session, "wizard_steps", selected = "step4")
    current_step(4)
    db_status("saving")
    
    # Show native Shiny progress notification during simulated network delay
    withProgress(message = "Connecting to database...", value = 0.3, {
      Sys.sleep(0.8)
      incProgress(0.4, detail = "Validating record uniqueness...")
      Sys.sleep(0.8)
      incProgress(0.3, detail = "Committing transaction...")
      Sys.sleep(0.5)
    })
    
    # Simulate a database rule: reject emails containing "taken"
    if (grepl("taken", tolower(input$email))) {
      db_status("error")
    } else {
      db_status("success")
    }
  })
  
  output$submission_status_ui <- renderUI({
    status <- db_status()
    
    if (status == "saving") {
      div(
        class = "text-center py-4",
        div(class = "spinner-border text-primary mb-3", role = "status"),
        h5("Submitting to Database..."),
        p(class = "text-muted", "Please wait while we write your record.")
      )
    } else if (status == "success") {
      div(
        class = "text-center py-3",
        div(class = "alert alert-success", h5("✓ Registration Complete!"), "Your profile has been saved to the database."),
        p(tags$strong("Transaction ID: "), paste0("USR-", sample(100000:999999, 1))),
        actionButton("reset_wizard", "Register Another User", class = "btn-outline-primary mt-2")
      )
    } else if (status == "error") {
      div(
        class = "text-center py-3",
        div(
          class = "alert alert-danger",
          h5("✗ Database Error: Duplicate Entry"),
          "That email address is already registered in our system."
        ),
        actionButton("retry_step1", "Change Email Address", class = "btn-warning mt-2")
      )
    }
  })
  
  # Reset or retry handlers
  observeEvent(input$retry_step1, {
    updateTabsetPanel(session, "wizard_steps", selected = "step1")
    current_step(1)
    db_status("idle")
  })
  
  observeEvent(input$reset_wizard, {
    updateTextInput(session, "email", value = "")
    updateNumericInput(session, "age", value = NA)
    updateSelectInput(session, "region", selected = "")
    updateTabsetPanel(session, "wizard_steps", selected = "step1")
    current_step(1)
    db_status("idle")
  })
}

shinyApp(ui, server)
```
#### Step 3
a. Click the Run App button at the top right of the app.R editor pane.
b. Test live validation: Type a partial email or an age under 18 to watch the status messages update immediately while keeping the Next button disabled.
c. Test database failure handling: Enter an email containing the word taken (such as taken@example.com) to trigger the simulated duplicate-record error state.

## 5. Marketing Data Analyst - Metricool* 
**Core Focus:** Managing organic engagement loops, evaluating community metrics, and benchmarking content efficacy.* 
**Online Practical:** 
**Cross-Channel Social ROI Performance Auditing**
  * **Tools Needed:** Metricool dashboard (Free or Sandbox tier).
  * **Objective:** Aggregate impressions, click-through rates (CTR), and follower growth patterns from unified social channels over 90 days.
  * **Deliverable:** A client-ready marketing performance PDF generated directly from Metricool metrics, accompanied by a content strategy review.

  ### Cross-Channel Social ROI Performance Audit (Metricool)

A step-by-step execution guide for auditing 90-day organic social media performance, evaluating engagement loops, and delivering a client-ready PDF report with a strategic review.

---

#### 📋 Overview

- **Role:** Marketing Data Analyst
- **Core Focus:** Organic engagement loops, community metrics, and content efficacy benchmarking
- **Tool:** Metricool Dashboard (Free or Sandbox tier)
- **Timeframe:** Last 90 Days
- **Final Deliverables:**
  1. A client-ready **Marketing Performance PDF** exported from Metricool.
  2. A **Content Strategy Review** (executive summary + actionable recommendations).

---

#### 🛠️ Prerequisites

Before starting the audit, ensure you have:
- [ ] Access to a **Metricool account** (Free tier or Sandbox environment).
- [ ] At least **2+ active social channels** connected (e.g., Instagram, LinkedIn, X/Twitter, Facebook, TikTok, or YouTube) with historical data, or access to Metricool's demo/sandbox data.
- [ ] A document editor (Google Docs, Notion, or Word) to draft your Content Strategy Review.

---

### 🚀 Step-by-Step Execution Guide

#### Phase 1: Environment Setup & Data Aggregation
1. **Log into Metricool:** Open your dashboard and navigate to the **Analytics** tab in the top navigation bar.
2. **Verify Connected Channels:** Check the left-hand sidebar to confirm all target social profiles are connected and syncing properly.
3. **Set the 90-Day Date Range:**
   - Click the date picker in the top-right corner.
   - Select **Last 90 Days** (or manually set a 90-day window).
   - Enable the **"Compare with previous period"** toggle to benchmark growth against the prior 90 days.

### Phase 2: Metric Extraction & Auditing
Review each connected channel individually and record the following core metrics:

| Metric Category | Key Data Points to Capture | What to Look For |
| :--- | :--- | :--- |
| **Reach & Visibility** | Total Impressions, Reach, Profile Views | Upward/downward trends; spikes tied to viral posts or campaigns. |
| **Traffic & Conversion** | Link Clicks, Click-Through Rate (CTR) | Which formats/CTAs actually drive off-platform traffic. |
| **Community Growth** | Net Follower Growth, Followers Gained vs. Lost | Churn spikes (unfollows) vs. steady organic acquisition. |
| **Engagement Loops** | Engagement Rate, Comments, Shares, Saves | High saves/shares indicate high content value and algorithmic boost. |

#### Phase 3: Benchmarking Content Efficacy
1. **Audit Top & Bottom Performers:**
   - Go to the **List of Posts** table within each channel's analytics view.
   - Sort posts by **Impressions**, **Engagement**, and **Clicks** (descending and ascending).
   - Identify the **Top 3** and **Bottom 3** posts across your channels.
2. **Pattern Recognition:**
   - Note the **content format** (Reels/Short video, Carousels, Single Image, Text/Links).
   - Note the **posting day/time** (check Metricool's *Best Time to Post* heatmap).
   - Note the **topic/hook** used in top-performing posts.

#### Phase 4: Generate the Metricool PDF Report
1. Navigate to **Analytics > Reports** in the left-hand menu.
2. Select the **90-Day timeframe** you audited.
3. Choose the channels to include in the report.
4. **Customize Sections:** Toggle on *Summary*, *Community Growth*, *Engagement*, and *Top Posts* (disable irrelevant sections to keep it clean).
5. *(Optional)* Upload a custom brand/client logo for a polished look.
6. Click **Download PDF** and verify that all charts and tables render cleanly without cut-offs.

#### Phase 5: Write the Content Strategy Review
Create a concise, 1–2 page executive document (or appendix to your PDF) using the structure below:

1. **Executive Summary (3–4 sentences):** High-level overview of 90-day performance (e.g., *"Organic impressions rose 18% over 90 days, led by LinkedIn carousels, though overall CTR dipped 0.4%."*).
2. **Cross-Channel Scorecard:** A quick summary table comparing Impressions, CTR, Engagement Rate, and Net Follower Growth across channels.
3. **What Worked (Engagement Loops):** Highlight top content pillars and formats that drove shares, saves, and comments.
4. **Gaps & Bottlenecks:** Point out underperforming channels, high follower churn periods, or weak CTAs hurting CTR.
5. **Actionable 30-Day Recommendations (3–5 bullets):** Specific changes to make next (e.g., *"Shift 40% of static image posts to short-form video,"* *"A/B test link placement in captions to lift CTR"*).

---

## 6. Marketing Data Analyst - SQL* 
**Core Focus:** Joining distributed advertising metrics to calculate exact customer acquisition costs.* 
**Online Practical:** 
**Ad Spend & Conversion Attribution Tuning**
  * **Tools Needed:** PostgreSQL, pgAdmin.
  * **Objective:** Write advanced relational SQL queries (`JOIN`, `GROUP BY`, `CASE WHEN`) to reconcile ad platform costs against backend transactional conversions.
  * **Deliverable:** A raw SQL script that calculates Return on Ad Spend (ROAS) and Cost Per Acquisition (CPA) grouped by traffic source.

## 7. Data Engineer - SQL* 
**Core Focus:** Defining relational architectures, enforcing data constraints, and ensuring database indexing sanity.* 
**Online Practical:** 
**Financial Transaction Database Schema Modeling**
  * **Tools Needed:** PostgreSQL, pgAdmin.
  * **Objective:** Design and write DDL scripts to build tables for customers, accounts, and transactions with correct primary/foreign key relationships.
  * **Deliverable:** A validated `.sql` database creation script that includes indices for optimized transaction history retrieval.

## 8. Data Engineer - Posit Cloud* 
**Core Focus:** Building automated data collection intervals and scheduling hands-off analytical documents.* 
**Online Practical:** **Automated Scheduled Report Pipeline**
  * **Tools Needed:** Posit Cloud, R Markdown or Quarto, Cron jobs/Posit Connect.
  * **Objective:** Write a script that checks a live web data source, structures new records, and updates a stylized analytical report document layout.
  * **Deliverable:** A reproducible Quarto template that executes on a schedule to render a refreshed, standalone summary report document.

## 9. Business Analytics Translator - Excel* 
**Core Focus:** Bridging complex underlying data frameworks into clear operational forecasting models for business leads.* **Online Practical:** 
**User Cohort Retention & Financial Run Rate Forecast**
  * **Tools Needed:** Microsoft Excel.
  * **Objective:** Translate raw cohort activity dates into a monthly subscription retention matrix and map future corporate cash flow projections.
  * **Deliverable:** A financial forecasting model complete with conditional formatting heatmaps and a 12-month forward-looking executive summary.

## 10. Business Analytics Translator - Shiny* 
**Core Focus:** Democratizing statistical calculation engines by creating easy-to-use, interactive tools for non-technical stakeholders.* 
**Online Practical:** 
**Executive Scenario Planning Simulator**
  * **Tools Needed:** Posit Cloud, RShiny framework.
  * **Objective:** Wrap an R-based predictive model into an app with slider controls for price adjustments, hiring plans, and marketing budgets.
  * **Deliverable:** An interactive application allowing non-technical leaders to adjust input variables and see instant financial projections.
