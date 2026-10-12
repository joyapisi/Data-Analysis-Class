

# 🚀 Data Careers Online Curriculum: 10 Practical Projects
This repository contains a structured, hands-on curriculum featuring data roles calibrated strictly to a modern analytics stack: **SQL, Posit Cloud (R, Shiny, Python), Excel, Metricool, GA4, and PostgreSQL**. Roles are strategically repeated across different core technologies to maximize practical skill depth.
---## 📋 Curriculum Overview
| # | Career Path | Project Focus | Core Tools |
|---|:---|:---|:---|
| 1 | [Data Analyst](#2-data-analyst---posit-cloud--r) | Macroeconomic GDP Visualization | Posit Cloud, R, ggplot2 |
| 2 | [Data Analyst](#1-data-analyst---excel) | E-Commerce Sales Performance | Excel / Sheets |
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

### 1. Data Analyst - Posit Cloud & R* 
**Core Focus:** Writing reproducible scripts to fetch, clean, and map global economic indicators.* 
**Online Practical:** **Macroeconomic GDP Trend Visualization**
  * **Tools Needed:** Posit Cloud workspace, R (`tidyverse`, `WDI` or `ggplot2`).
  * **Objective:** Programmatically ingest international development data to calculate historical GDP growth variations across regions.
  * **Deliverable:** An R script file hosted in Posit Cloud that generates an annotated multi-line trend chart and a localized clean summary table.

  ```
// Install required libraries if they are missing
// install.packages (c("tidyverse", "scales"))

# Load libraries
library(tidyverse)
library(scales)

# 1. Generate clean, reproducible Macroeconomic Dataset internally
set.seed(42)
years <- 2015:2025
regions <- c("North America", "Europe & Central Asia", "East Asia & Pacific", "Sub-Saharan Africa")

gdp_data <- expand.grid(Year = years, Region = regions) %>%
  mutate(
    # Simulate a realistic baseline and positive growth trajectory per region
    Base_GDP = case_when(
      Region == "North America" ~ 20,
      Region == "Europe & Central Asia" ~ 18,
      Region == "East Asia & Pacific" ~ 15,
      Region == "Sub-Saharan Africa" ~ 2.5
    ),
    Growth_Rate = case_when(
      Region == "North America" ~ 0.022,
      Region == "Europe & Central Asia" ~ 0.018,
      Region == "East Asia & Pacific" ~ 0.045,
      Region == "Sub-Saharan Africa" ~ 0.038
    ),
    # Add minor random economic fluctuations
    Noise = rnorm(n(), mean = 0, sd = 0.2),
    GDP_Trillions = Base_GDP * (1 + Growth_Rate)^(Year - 2015) + Noise
  ) %>%
  select(Year, Region, GDP_Trillions)

# 2. Inspect data frame structures 
print("First 6 rows of clean Macroeconomic Dataset:")
print(head(gdp_data))

# 3. Build an annotated, professional multi-line trend visualization
gdp_plot <- ggplot(gdp_data, aes(x = Year, y = GDP_Trillions, color = Region, group = Region)) +
  geom_line(linewidth = 1.2) +
  geom_point(size = 2.5) +
  theme_minimal(base_size = 14) +
  labs(
    title = "Macroeconomic GDP Trend Analysis (2015 - 2025)",
    subtitle = "Comparative analysis of regional economic output over a decade",
    x = "Calendar Year",
    y = "Gross Domestic Product (USD, In Trillions)",
    caption = "Source: Simulated Global Development Database"
  ) +
  scale_y_continuous(labels = dollar_format(suffix = "T")) +
  scale_x_continuous(breaks = seq(2015, 2025, by = 2)) +
  scale_color_brewer(palette = "Set1") +
  theme(
    legend.position = "bottom",
    plot.title = element_text(face = "bold", size = 16),
    plot.subtitle = element_text(color = "gray40"),
    panel.grid.minor = element_blank()
  )

# 4. Render the chart visualization to the plot viewer pane
print(gdp_plot)

# 5. Export clean data and final plot image directly to the cloud workspace
write.csv(gdp_data, "clean_regional_gdp_trends.csv", row.names = FALSE)
ggsave("gdp_trends_chart.png", plot = gdp_plot, width = 10, height = 6, dpi = 300)

print("Process Complete. 'clean_regional_gdp_trends.csv' and 'gdp_trends_chart.png' successfully saved to Posit Cloud.")

  ```
### 2. Data Analyst - Excel
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
 

### 3. Product Analyst - GA4* 
**Core Focus:** Tracking web traffic conversions, mapping user interactions, and identifying application friction points.* **Online Practical:** 
**User Acquisition & Checkout Funnel Analysis**
  * **Tools Needed:** Google Analytics 4 (GA4 Demo Account or Test Property).
  * **Objective:** Build a custom exploration funnel to audit where users drop off between viewing an item and finalizing a purchase.
  * **Deliverable:** A GA4 Exploration Funnel report detailing specific stage-to-stage drop-off rates and three data-backed UX recommendations.
  <img width="500" height="375" alt="image" src="https://github.com/user-attachments/assets/e5f58c48-861b-44ce-ba65-0d15ad03e4bc" />
  ```
  ## 3. Implementation Steps for Practical 3 (Product Analyst - GA4)
This practical utilizes the official Google Analytics 4 (GA4) Merchandise Store Demonstration Account. Students do not need to configure code snippets or manage a live website deployment to complete this analysis.
## Step 1: Access the Environment

   1. Open a web browser and navigate to the official [Google Analytics Help Center](https://support.google.com/analytics/answer/6366960).
   2. Scroll down to the Access the demo account section and click the link for the GA4 Google Merchandise Store web property.
   3. Log in with any standard Google account credentials.

## Step 2: Open the Explorations Workspace

   1. Locate the left-hand navigation sidebar inside the GA4 interface.
   2. Click on Explore (represented by a blank canvas icon with a trend graph) to bypass standard canned reporting layouts.
   3. Select Blank to spin up an unrestricted custom analytics exploration layout from scratch.
   4. Rename your configuration tab in the top-left section from Untitled Exploration to User Acquisition & Checkout Funnel Analysis.

## Step 3: Configure the Funnel Parameters

   1. Look at the Variables column on the far left. Find Technique and change the drop-down menu setting from Free Form to Funnel Exploration.
   2. Scroll down to the Tab Settings column (the middle column) and locate the Steps configuration panel. Click the Pencil Icon to open the custom funnel step builder modal.

## Step 4: Map Out the Four Funnel Stages
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
## Step 5: Isolate Growth Bottlenecks and Formulate Insights

   1. Analyze the automatically generated bar graph visual asset in the main canvas pane.
   2. Record the Abandonment Rate (the red down-arrow metric) calculated between Step 2 (Product Viewed) and Step 3 (Added to Cart). This usually indicates design flaws, confusing pricing displays, or weak call-to-action buttons.
   3. Drag the Session Source/Medium dimension from the Variables column down into the Breakdown box under Tab Settings to group the funnel rows by ad traffic channels. Identify which pipeline channel drops off most aggressively.

## Step 6: Export Your Deliverable

   1. Click the Export Data icon located in the upper right quadrant of the main canvas pane.
   2. Select Google Sheets or CSV to save the tabular row outputs.
   3. Compile these calculations into a clean Markdown document or executive memo summarizing three UI optimization ideas aimed directly at the highest drop-off stage.
```

### 4. Product Analyst - Posit Cloud & Shiny* 
**Core Focus:** Building front-end web interfaces to capture user inputs and handle structured analytical workflows.* 
**Online Practical:** **Multi-Step Dynamic Registration Form App**
  * **Tools Needed:** Posit Cloud, RShiny framework.
  * **Objective:** Develop a reactive 3-step sign-up interface that validates inputs (email, age, region) on the fly and simulates database submission status.
  * **Deliverable:** A live UI link and a source `app.R` script processing user form interactions reactively in the cloud.
### 5. Marketing Data Analyst - Metricool* 
**Core Focus:** Managing organic engagement loops, evaluating community metrics, and benchmarking content efficacy.* 
**Online Practical:** 
**Cross-Channel Social ROI Performance Auditing**
  * **Tools Needed:** Metricool dashboard (Free or Sandbox tier).
  * **Objective:** Aggregate impressions, click-through rates (CTR), and follower growth patterns from unified social channels over 90 days.
  * **Deliverable:** A client-ready marketing performance PDF generated directly from Metricool metrics, accompanied by a content strategy review.
### 6. Marketing Data Analyst - SQL* 
**Core Focus:** Joining distributed advertising metrics to calculate exact customer acquisition costs.* 
**Online Practical:** 
**Ad Spend & Conversion Attribution Tuning**
  * **Tools Needed:** PostgreSQL, pgAdmin.
  * **Objective:** Write advanced relational SQL queries (`JOIN`, `GROUP BY`, `CASE WHEN`) to reconcile ad platform costs against backend transactional conversions.
  * **Deliverable:** A raw SQL script that calculates Return on Ad Spend (ROAS) and Cost Per Acquisition (CPA) grouped by traffic source.
### 7. Data Engineer - SQL* 
**Core Focus:** Defining relational architectures, enforcing data constraints, and ensuring database indexing sanity.* 
**Online Practical:** 
**Financial Transaction Database Schema Modeling**
  * **Tools Needed:** PostgreSQL, pgAdmin.
  * **Objective:** Design and write DDL scripts to build tables for customers, accounts, and transactions with correct primary/foreign key relationships.
  * **Deliverable:** A validated `.sql` database creation script that includes indices for optimized transaction history retrieval.
### 8. Data Engineer - Posit Cloud* 
**Core Focus:** Building automated data collection intervals and scheduling hands-off analytical documents.* 
**Online Practical:** **Automated Scheduled Report Pipeline**
  * **Tools Needed:** Posit Cloud, RMarkdown or Quarto, Cron jobs/Posit Connect.
  * **Objective:** Write a script that checks a live web data source, structures new records, and updates a stylized analytical report document layout.
  * **Deliverable:** A reproducible Quarto template that executes on a schedule to render a refreshed, standalone summary report document.
### 9. Business Analytics Translator - Excel* 
**Core Focus:** Bridging complex underlying data frameworks into clear operational forecasting models for business leads.* **Online Practical:** 
**User Cohort Retention & Financial Run Rate Forecast**
  * **Tools Needed:** Microsoft Excel.
  * **Objective:** Translate raw cohort activity dates into a monthly subscription retention matrix and map future corporate cash flow projections.
  * **Deliverable:** A financial forecasting model complete with conditional formatting heatmaps and a 12-month forward-looking executive summary.
### 10. Business Analytics Translator - Shiny* 
**Core Focus:** Democratizing statistical calculation engines by creating easy-to-use, interactive tools for non-technical stakeholders.* 
**Online Practical:** 
**Executive Scenario Planning Simulator**
  * **Tools Needed:** Posit Cloud, RShiny framework.
  * **Objective:** Wrap an R-based predictive model into an app with slider controls for price adjustments, hiring plans, and marketing budgets.
  * **Deliverable:** An interactive application allowing non-technical leaders to adjust input variables and see instant financial projections.
