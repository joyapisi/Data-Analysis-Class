# Final Exam Project (30 Points)
# Kenya Hospitality & Airbnb Guest Intelligence System

## 1. Project Overview

You are a data analyst working with a hospitality business in Kenya.

Your task is to develop a visitor data collection and analysis system that collects guest information through an R Shiny application, cleans the collected data using Microsoft Excel, and stores and analyses visitor records using an SQLite database.

The objective is to generate useful hospitality market insights that can help Kenyan hotels, resorts, and Airbnb businesses understand their visitors and develop targeted packages.

The project consists of three connected stages:

### Part A: Data Collection – R Shiny on Posit Cloud (12 Points)

Build an interactive guest check-in form using R Shiny on Posit Cloud.

The application should:
- Collect visitor information through six input fields.
- Validate essential fields before accepting submissions.
- Allow realistic free-text variations in names, countries, and citizenship.
- Store submitted information in an SQLite database.
- Display submitted records in a live data table.
- Allow users to download collected records as a CSV file.

IMPORTANT:
The objective of Part A is to collect RAW DATA.

Do not automatically standardize spelling, capitalization, or spacing in text fields.

For example, the following entries should be accepted:

- kenya
- Kenya
- KENYA
- Kenya (with trailing spaces)
- usa
- USA
- U.S.A.

These variations are intentional and will be corrected during Part B.

Input validation should only ensure that required information is provided and that entries meet basic requirements.

### Part B: Data Cleaning – Microsoft Excel (8 Points)

Import the raw CSV exported from Part A into Microsoft Excel.

Clean and standardize the data by:
- Removing unnecessary spaces.
- Correcting inconsistent capitalization.
- Standardizing country names.
- Removing duplicate records.
- Checking and handling missing values.

**[OPTIONAL]** Create a Cleaning Log documenting the changes made.

**[OPTIONAL]** Finally, create a Pivot Table summarizing visitor patterns by country of residence and citizenship.

### Part C: Database & SQL Analysis – SQLite (10 Points)

Connect the R Shiny application to an SQLite database.

Automatically save every valid form submission to the database.

Use SQL queries through R to generate hospitality business insights, including:

1. Visitor market breakdown by country.
2. International guests with long stays.
3. Returning Kenyan diaspora visitors.

---

## 2. Project Folder Structure

Your completed Posit Cloud project should contain:

kenya-hospitality-exam/

- README.md
- app.R
- kenya_hospitality.sqlite
- sql_analysis.R
- raw_guest_entries.csv
- cleaned_guest_entries.xlsx

The SQLite database should be generated automatically when the Shiny application runs.

The raw CSV should be downloaded from the Shiny application.

The cleaned Excel workbook should be created in Microsoft Excel.

---

## 3. Prerequisites and Setup

Create a new RStudio project on Posit Cloud.

Install the required R packages using the R Console:

```r
install.packages(c(
  "shiny",
  "DBI",
  "RSQLite",
  "DT",
  "dplyr"
))
```

---

# PART A: DATA COLLECTION – R SHINY
## 12 Points

## 4. Build the Guest Check-In Form

Create an R Shiny application in a file named app.R.

The form must collect the following six variables:

| Variable | Input Type | Description |
|---|---|---|
| id | Text input | Guest / Booking ID |
| name | Text input | Guest full name |
| country | Text input | Country of residence |
| citizenship | Text input | Guest citizenship / nationality |
| length_of_stay | Numeric input | Number of nights spent |
| most_preferred_amenity | Checkbox group | Preferred guest amenities |

For most_preferred_amenity, provide these choices:

- cultural experiences
- wildlife packages
- airport transfers

Allow guests to select more than one amenity.

If multiple amenities are selected, combine them into a single comma-separated string before saving.

Example:

wildlife packages, airport transfers

### 4.1 Input Validation

Add a Submit button.

Your application must implement the following validation rules:

1. Guest / Booking ID cannot be empty.
2. Guest name cannot be empty.
3. Length of stay must be greater than zero.
4. Length of stay must be a whole number.
5. At least one preferred amenity must be selected.

Display appropriate error messages when validation fails.

IMPORTANT: DATA QUALITY VS INPUT VALIDATION

The purpose of the form is to collect raw visitor information.

Do not use dropdown lists for country or citizenship.

Do not automatically apply TRIM(), PROPER(), UPPER() or other text-cleaning functions to the submitted text fields.

Do not automatically correct:
- Capitalization differences.
- Country spelling variations.
- Alternative country abbreviations.
- Extra spaces in names or text entries.

For example, Kenya, kenya, KENYA and USA, usa, U.S.A. should be allowed as submitted text.

These variations will be corrected in Microsoft Excel during Part B.

Input validation should prevent incomplete or invalid submissions, not eliminate realistic data-quality problems.

### 4.2 Live Data Preview

Use DT::datatable() to display all submitted records inside the Shiny application.

The table should update automatically whenever a new valid guest submission is received.

### 4.3 CSV Export

Add a Download CSV button using downloadHandler().

The downloaded file must be named:

raw_guest_entries.csv

The CSV should contain the original submitted text without automatic standardization.

### 4.4 Data Generation Requirement

Submit at least 20 realistic guest records through your running Shiny application.

Include a mixture of:

- Kenyan residents.
- International visitors.
- Kenyan citizens living abroad.
- Visitors with different lengths of stay.
- Different amenity preferences.

INTENTIONALLY INCLUDE DATA ANOMALIES:

Examples:

Country variations:
- Kenya
- kenya
- KENYA
- Kenya (with trailing spaces)
- USA
- usa
- U.S.A.
- United States
- UK
- United Kingdom

**[OPTIONAL]** Name variations:
- Jason Onyango
- jason ONYANGOO
-  Jason Onyango
- WANJIRU NJIRU

Duplicate submissions:
- Submit at least two records with the same ID and guest name.
- Ensure the repeated records are genuine duplicate test submissions.

Do not manually clean the records before exporting.

After entering at least 20 records, download raw_guest_entries.csv.

### 4.5 Data Fundamentals

In your README.md, explain the measurement/data type of each collected variable. Refer to Data Fundamentals Week 1&2 Notes for this.

| Variable | Data Type | Explanation |
|---|---|---|
| id | Enter Data Type here | Give Your Explanation Here |
| name | Enter Data Type here | Give Your Explanation Here |
| country | Enter Data Type here | Give Your Explanation Here |
| citizenship | Enter Data Type here | Give Your Explanation Here |
| length_of_stay | Enter Data Type here | Give Your Explanation Here |
| most_preferred_amenity | Enter Data Type here | Give Your Explanation Here |

e.g:

- Numeric/Nominal data: Categories without a natural order.
- Discrete data: Countable numerical values.

Identify which of these data types are represented in your dataset and which are not. Refer to Data Fundamentals Week 1&2 Notes for this.

### 4.6 Hospitality Business Application

Write a short explanation of how a Kenyan hotel can use country of residence, citizenship, and length of stay together.

Consider the following examples:

- International tourists may be interested in cultural experiences, wildlife packages, and airport transfers.
- Kenyan residents may respond to local weekend getaway packages.
- Kenyan citizens living abroad may be interested in diaspora family packages.
- Guests staying five or more nights may be targeted with extended-stay discounts.

Explain how combining these variables helps hospitality businesses understand their markets and develop targeted offers.

---

# PART B: DATA CLEANING – MICROSOFT EXCEL
## 8 Points

## 5. Import the Raw CSV

Open Microsoft Excel.

Import:

raw_guest_entries.csv

Save your working file as:

cleaned_guest_entries.xlsx

Create the following worksheets:

1. Raw Data
2. Cleaned Data
3. **[OPTIONAL]** Cleaning Log
4. **[OPTIONAL]** Hospitality Summary

Keep the original imported data in the Raw Data worksheet.

## 5.1 Text and Formatting Standardization (3 Points)

Clean ONLY the COUNTRY text fields:
- country

**[OPTIONAL]** Clean all the fields:
- id
- name
- country
- citizenship
- most_preferred_amenity

Use Excel functions such as:

TRIM()
PROPER()
UPPER()

Examples:

| Raw Entry | Cleaned Entry |
|---|---|
| kenya | Kenya |
| KENYA | Kenya |
| Kenya (extra spaces) | Kenya |
| jason ONYANGO | Jason Onyango |
|  Wanjiru Njiru | Wanjiru Njiru |
| usa | USA |
| U.S.A. | USA |

Note:
PROPER() alone will not standardize all country names.

For example, USA and U.S.A. require additional standardization rules. Use IF(), SUBSTITUTE(), or a lookup table where appropriate.

Ensure IDs follow a consistent uppercase format.

Format length_of_stay as a whole number with zero decimal places.

## 5.2 Deduplication and Missing Value Audit (3 Points)

Use Excel:

Data → Remove Duplicates in the country column

Remove repeated submissions.

**[OPTIONAL]** Check for blank cells across all variables.

Where appropriate:
- Replace missing text fields with "Not Specified".
- **[OPTIONAL]** If length_of_stay contains missing numerical values, calculate the median of available values and use it to fill the missing entries.

**[OPTIONAL]** Document the following in your Cleaning Log:

1. Total rows exported from Part A.
2. Number of duplicate rows removed.
3. Number of missing values identified.
4. How missing values were handled.
5. Text standardization rules applied.
6. Any additional corrections made.

## 5.3 (OPTIONAL) Hospitality Summary Pivot Table (2 Points)

Create a Pivot Table using the Cleaned Data worksheet.

Place the Pivot Table in the Hospitality Summary worksheet.

Configure it as follows:

ROWS:
- Country of Residence
- Citizenship

VALUES:
- ID → Count
- Length of Stay → Average

Rename the values to:

- Total Guests
- Average Length of Stay (Nights)

The Pivot Table should help a hotel understand where visitors reside, their citizenship, and how long they typically stay.

---

# PART C: DATABASE AND SQL ANALYSIS – SQLITE
## 10 Points

## 6. SQLite Database Setup

Create a local SQLite database named:

kenya_hospitality.sqlite

The database should be generated automatically when app.R runs.

Use the DBI and RSQLite packages.

Create a table named:

guest_submissions

The table should contain:

```sql
CREATE TABLE IF NOT EXISTS guest_submissions (
  id TEXT,
  name TEXT,
  country TEXT,
  citizenship TEXT,
  length_of_stay INTEGER,
  most_preferred_amenity TEXT
);
```

The additional most_preferred_amenity column is required to preserve all six form inputs.

## 6.1 Live Shiny and SQLite Integration (4 Points)

Modify the Submit button logic so that every valid submission is saved directly into SQLite.

Use:

dbWriteTable(
  con,
  "guest_submissions",
  new_guest,
  append = TRUE,
  row.names = FALSE
)

The live preview table must retrieve its data from SQLite using:

dbReadTable(con, "guest_submissions")

The CSV download button must also retrieve records directly from SQLite.

Ensure that the database retains records when the Shiny application is restarted.

## 6.2 SQL Analytical Queries (3 Points)

Create a separate R script named:

sql_analysis.R

Connect to the SQLite database using DBI and RSQLite.

Use dbGetQuery() to execute the following three SQL queries.

### Query 1: Market Breakdown

Count the number of guests and calculate the average length of stay grouped by country of residence.

Required output:
- Country
- Total Guests
- Average Length of Stay

### Query 2: Long-Stay International Guests

Identify visitors whose citizenship is not Kenyan and who stayed for five or more nights.

Required conditions:
- citizenship is not Kenya.
- length_of_stay >= 5.
- Results ordered from longest to shortest stay.

### Query 3: Domestic vs Diaspora Comparison

Identify returning Kenyan diaspora visitors.

These are guests who:
- Have Kenya as their citizenship.
- Currently reside outside Kenya.

Required condition:

country != 'Kenya'
AND citizenship = 'Kenya'

Display their names, countries of residence and length of stay.

Note:
Run these queries against the original submitted SQLite records. The raw database preserves the original text entries, so be mindful that values such as "Kenyan", "kenya" and "Kenya " may require normalization in SQL to avoid excluding relevant visitors.

## 6.3 Business Interpretation

For each query, provide a short interpretation of the results.

Explain what the results could mean for a Kenyan hotel or resort.

For example:
- Which countries contribute the most guests?
- Which international visitors stay the longest?
- How can hotels attract returning Kenyan diaspora visitors?

---

# 7. Final Submission Checklist

Before submitting, ensure that your Posit Cloud project contains:

| File | Expected Deliverable |
|---|---|
| README.md | Project documentation and data fundamentals |
| app.R | Working Shiny visitor check-in application |
| kenya_hospitality.sqlite | SQLite database with guest submissions |
| sql_analysis.R | Three working SQL queries and interpretations |
| raw_guest_entries.csv | Original exported visitor records |
| cleaned_guest_entries.xlsx | Cleaned data, Cleaning Log and Pivot Table |

## Final Assessment Breakdown

| Part | Assessment | Points |
|---|---|---:|
| A | Six-input Shiny form and validation | 4 |
| A | Server logic, data entry, live preview and CSV export | 5 |
| A | Data fundamentals and hotel pitch | 3 |
| B | Text and formatting standardization | 3 |
| B | Deduplication and missing value audit | 3 |
| B | Hospitality Pivot Table | 2 |
| C | SQLite database and table setup | 3 |
| C | Shiny and SQLite integration | 4 |
| C | SQL analytical queries | 3 |
| | TOTAL | 30 |

---

# 8. Project Learning Outcome

By completing this project, you should demonstrate the ability to:

1. Collect structured visitor data using an interactive web application.
2. Understand the difference between input validation and data cleaning.
3. Identify data quality issues in raw datasets.
4. Clean and standardize data using Microsoft Excel.
5. Generate hospitality market summaries using Pivot Tables.
6. Store persistent records using SQLite.
7. Retrieve and analyse records using SQL.
8. Translate analytical findings into actionable hospitality business insights.

Your final output should demonstrate a connected data pipeline from visitor registration to commercial intelligence.
