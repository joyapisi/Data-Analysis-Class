# Final Exam Project (30 Points): Kenya Hospitality & Airbnb Guest Intelligence System

## 1. Project Overview & Business Scenario
You operate an Airbnb portfolio in Kenya (covering key destinations such as **Nairobi, Mombasa/Diani, Naivasha, and Maasai Mara**). To monetize visitor insights, you are building an end-to-end data collection, cleaning, and SQL analytics pipeline. 

Guests complete a digital **Visitor Experience & Travel Preference Form** built in **R Shiny** on **Posit Cloud**. The collected data is cleaned in **Excel** and stored in a local **SQLite relational database** directly inside Posit Cloud so you can generate actionable market reports to sell to Kenyan hotels, resorts, and tour operators.

---

## 2. Project Folder Structure (Posit Cloud)
Ensure your Posit Cloud workspace contains the following files upon submission:

```text
kenya-hospitality-exam/
├── README.md                     # Project documentation & exam rubric
├── app.R                         # Part A & C: R Shiny UI/Server + SQLite integration
├── kenya_hospitality.sqlite      # Part C: Local SQLite database file (auto-generated)
├── sql_analysis.R                # Part C: Standalone SQL verification & business queries
├── raw_guest_logs.csv            # Part B: Uncleaned sample/exported dataset
└── cleaned_kenya_hospitality.xlsx # Part B: Cleaned dataset, cleaning log & Pivot Table
```

---

## 3. Prerequisites & Setup on Posit Cloud
1. Log in to **Posit Cloud** and open this project workspace.
2. Run the following command in the **R Console** to install all required packages:
   ```r
   install.packages(c("shiny", "DBI", "RSQLite", "DT", "dplyr"))
   ```
3. No external database passwords or `.Renviron` configuration are needed—the SQLite backend runs locally inside the Posit Cloud directory.

---

## 4. Exam Deliverables & Grading Rubric (30 Points Total)

### Part A: Data Fundamentals & R Shiny App on Posit Cloud (12 Points)
Build and run an interactive R Shiny form in `app.R` tailored to the Kenyan hospitality industry.

* **UI Form Inputs (4 pts):**
  * **Guest Profile:** Guest Name, Guest ID, Country of Residence (`Kenya`, `USA`, `UK`, `Germany`, `Uganda`, `Other`), and Travel Party (`Solo`, `Couple`, `Family`, `Business Group`).
  * **Stay Details:** Length of Stay (nights).
  * **Hospitality Preferences:** Primary Purpose (`Leisure/Safari`, `Business/Conference`, `Staycation`, `Visiting Family`), Top Desired Amenity (`High-Speed Wi-Fi`, `Airport Transfer`, `Swahili/Local Cuisine`, `Swimming Pool`, `Co-working Space`).
* **Server Validation & Live Preview (4 pts):**
  * Validate inputs on **Submit** (prevent blank guest names or `nights <= 0`).
  * Show a confirmation notification and render an updated table of recent submissions using `DT::datatable()`.
* **Data Fundamentals & Commercial Pitch (4 pts):**
  * Include a short written section (in the app UI or a `report.md` note) classifying each variable by data type (**Nominal, Ordinal, Discrete, Continuous**) and explaining how a Kenyan hotel manager can use **two specific variables** from your form to increase revenue.

---

### Part B: Excel Data Cleaning & Exploratory Audit (8 Points)
Export or download at least **30–50 rows** of raw booking/survey records (`raw_guest_logs.csv`) and clean them in Excel (`cleaned_kenya_hospitality.xlsx`).

* **Text & Currency Standardization (3 pts):**
  * Clean inconsistent text casing and trailing spaces using `TRIM()` and `PROPER()` (e.g., `"nairobi "`, `"NRB"` → `"Nairobi"`; `"u.s.a"`, `"United States"` → `"USA"`).
  * Format dates consistently as `YYYY-MM-DD`.
  * Standardize all nightly budgets into **Kenyan Shillings (KES)** (convert any USD entries using a clearly documented exchange rate).
* **Deduplication & Missing Data (3 pts):**
  * Remove duplicate rows using **Data → Remove Duplicates** and record the exact number of duplicates removed in a **"Cleaning Log"** tab.
  * Handle blank cells systematically (impute median `budget_kes` for missing numeric budgets; label missing text fields as `"Not Specified"`).
* **Hospitality Pivot Table (2 pts):**
  * Build a **Pivot Table** on a dedicated tab displaying **Average Nightly Budget (KES)** and **Total Guest Count** segmented by **Country of Residence** and **Primary Purpose**.

---

### Part C: SQLite Database Integration & SQL Queries in Posit Cloud (10 Points)
Use `DBI` and `RSQLite` so your Shiny app writes directly to `kenya_hospitality.sqlite` inside Posit Cloud, then query the database using SQL.

* **Database & Table Initialization (3 pts):**
  * Automatically create `kenya_hospitality.sqlite` and initialize the `kenya_guest_survey` table when `app.R` launches:
    ```sql
    CREATE TABLE IF NOT EXISTS kenya_guest_survey (
      id INTEGER PRIMARY KEY AUTOINCREMENT,
      submitted_at TEXT,
      guest_name TEXT,
      guest_country TEXT,
      location TEXT,
      nights INTEGER,
      budget_kes REAL,
      purpose TEXT,
      amenity TEXT,
      rating INTEGER
    );
    ```
* **Live R Shiny \(\leftrightarrow\) SQLite Connection (4 pts):**
  * On button click, connect via `dbConnect(RSQLite::SQLite(), "kenya_hospitality.sqlite")`, append the new row using `dbWriteTable(..., append = TRUE)`, and close the connection cleanly with `dbDisconnect()`.
  * Populate the app's live data table directly from SQLite using `dbReadTable()`.
* **SQL Analytical Queries (`sql_analysis.R`) (3 pts):**
  * Write and execute **3 business SQL queries** via `dbGetQuery()` to answer key questions for hotel clients:
    1. **Destination Performance:** Total guests, average stay length, and average satisfaction rating grouped by Kenyan `location`.
    2. **High-Value International Segment:** Filter international guests (`guest_country != 'Kenya'`) staying `>= 4` nights with `budget_kes > 15000`, ordered from highest to lowest spend.
    3. **Business Traveler Demand:** Count the most requested `amenity` among guests visiting for `'Business/Conference'`.

---

## 5. How to Run & Verify the Project
1. Open `app.R` in Posit Cloud and click **Run App**.
2. Submit **at least 5 test entries** across different Kenyan locations and guest nationalities.
3. Stop the app and confirm that `kenya_hospitality.sqlite` appears in your Posit Cloud **Files** pane.
4. Open `sql_analysis.R` and run all lines (`Ctrl/Cmd + Enter`) to verify that your 3 SQL queries return clean summary tables from your stored submissions.

---

## 6. Grading Summary

| Component | Key Deliverables | Max Points |
| :--- | :--- | :---: |
| **Part A** | Functional R Shiny form on Posit Cloud, input validation & data fundamentals write-up | **12** |
| **Part B** | Cleaned `.xlsx` workbook, documented cleaning log, KES normalization & Pivot Table | **8** |
| **Part C** | Live `RSQLite` persistence in `app.R` + 3 working SQL business queries in `sql_analysis.R` | **10** |
| **Total** | | **30** |
