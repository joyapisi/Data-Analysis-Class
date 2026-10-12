# Excel Practicals: Data Management and Lookup Skills

**Audience:** Beginner Excel students\
**Suggested duration:** 2--3 lessons\
**Software:** Microsoft Excel or Excel Online\
**Submission:** One workbook containing a worksheet for each practical,
plus a short `README` or notes sheet explaining what was done.

## General instructions

1.  Create a new workbook named `Excel_Data_Management_Practicals.xlsx`.
2.  Use the sample datasets provided in each practical. You may type
    them in or paste them into Excel.
3.  Keep a copy of the original data before cleaning it.
4.  Name worksheets clearly, for example `P1_DataTypes`,
    `P2_Validation`, and so on.
5.  Save your workbook regularly.
6.  Unless a task specifically asks for a formula, students may use the
    Excel ribbon or menu commands.

------------------------------------------------------------------------

## Practical 1: Identify Data Types in a Table

**Objective:** Recognize common Excel data types and apply suitable
formats.

### Dataset

Enter the following into a worksheet named `P1_DataTypes`.

  -------------------------------------------------------------------------------------------------------------
  Student_ID   Student_Name   Course      Date_Registered        Marks    Fee_KES   Attendance_Rate Submitted
  ------------ -------------- ----------- ----------------- ---------- ---------- ----------------- -----------
  ADM001       Amina Otieno   Graphic     05/09/2026                78      25000              0.92 TRUE
                              Design                                                                

  ADM002       Brian Mwangi   Film        08/09/2026                64      30000              0.85 FALSE

  ADM003       Wanjiku Njeri  Animation   10/09/2026                91      28000              0.97 TRUE

  ADM004       Kevin Ouma     Graphic     12/09/2026                49      25000              0.72 FALSE
                              Design                                                                
  -------------------------------------------------------------------------------------------------------------

### Tasks

1.  Identify the likely data type for each column: text, number, date,
    logical value or formula.
2.  Format `Date_Registered` as a date.
3.  Format `Fee_KES` as currency in Kenyan shillings, where available.
4.  Format `Attendance_Rate` as a percentage.
5.  Keep `Student_ID` as text so leading zeros or letters are preserved.
6.  In a new column called `Result`, enter a formula that displays Pass
    when Marks are at least 50 and Fail otherwise.
7.  Explain the difference between a cell's underlying value and its
    displayed format.

**Expected result:** A table with readable formats and a
formula-generated `Result` column.

**Reflection:** Why should student IDs and phone numbers usually be
stored as text rather than used in arithmetic?

------------------------------------------------------------------------

## Practical 2: Data Validation

**Objective:** Restrict data entry to acceptable values and provide
clear error messages.

### Dataset

Create a worksheet named `P2_Validation` with these headings:

  Student_ID   Student_Name   Course             Marks Date_Registered
  ------------ -------------- ---------------- ------- -----------------
  ADM001       Amina Otieno   Graphic Design        78 05/09/2026
  ADM002       Brian Mwangi   Film                  64 08/09/2026

### Tasks

1.  Apply a **drop-down list** to `Course` with these options:
    `Graphic Design`, `Film`, `Animation`, `Digital Marketing`.
2.  Restrict `Marks` to whole numbers between 0 and 100.
3.  Restrict `Date_Registered` to dates between 01/01/2026 and
    31/12/2026.
4.  Add an input message to `Marks`: "Enter a whole-number mark from 0
    to 100."
5.  Add a Stop-style error alert for invalid marks.
6.  Test the rules by trying a mark of 120, a negative mark, and a
    course that is not on the list.
7.  Record which entries Excel rejects and which it accepts.

**Extension:** Create a custom validation rule that prevents duplicate
student IDs. If the first ID is in cell A2, select the relevant input
range and use a formula such as `=COUNTIF($A$2:$A$100,A2)=1` (adjust the
range to match the selected rows).

**Expected result:** A registration sheet that helps prevent common
entry errors.

------------------------------------------------------------------------

## Practical 3: Data Cleaning --- Duplicates, Blanks and Inconsistencies

**Objective:** Detect and correct common data-quality problems without
losing important records.

### Dataset

Enter this data in `P3_Cleaning`.

  Student_ID   Student_Name    Course             Marks Phone
  ------------ --------------- ---------------- ------- ------------
  ADM001       Amina Otieno    Graphic Design        78 0712345678
  ADM002       Brian Mwangi    Film                  64 0723456789
  ADM003       Wanjiku Njeri   Animation             91 
  ADM002       Brian Mwangi    Film                  64 0723456789
  ADM004       kevin ouma      graphic design           0734567890
  ADM005       Mary Achieng    Animation             82 0745678901
  ADM006       Peter Kamau     Film                 105 0756789012

### Tasks

1.  Duplicate the worksheet and name the copy `P3_Cleaned`. Keep the
    original unchanged.
2.  Identify the duplicated record using `Student_ID`.
3.  Use **Data → Remove Duplicates** on the cleaned copy. Explain why
    you selected `Student_ID` as the key column.
4.  Find the missing phone number and missing mark. Do not invent
    values; mark them as `Missing` or leave them blank and record them
    for follow-up.
5.  Standardize `kevin ouma` and `graphic design` to the correct
    capitalization.
6.  Remove the extra space in `Mary  Achieng`.
7.  Investigate the mark of 105. Flag it as invalid rather than silently
    changing it.
8.  Create a `Cleaning_Notes` column describing each correction or
    issue.

**Expected result:** A cleaned copy, an unchanged original, and notes
explaining decisions.

**Reflection:** Why is it risky to delete every row containing a blank
cell?

------------------------------------------------------------------------

## Practical 4: Standardize Text, Dates and Number Formats

**Objective:** Make values consistent so they can be sorted, filtered
and analysed reliably.

### Dataset

Enter this data in `P4_Standardize`.

  Student_ID   Student_Name    Date_Registered   Fee_KES      Attendance
  ------------ --------------- ----------------- ------------ ------------
  ADM001       amina otieno    5 Sep 2026        25000        0.92
  ADM002       BRIAN MWANGI    08/09/2026        KES 30,000   85%
  ADM003       Wanjiku Njeri   2026-09-10        28000.00     0.97
  ADM004       kevin ouma      12/09/26          25,000       72%

### Tasks

1.  Standardize names to consistent capitalization using `PROPER` where
    appropriate.
2.  Remove leading, trailing and repeated spaces using `TRIM`.
3.  Convert all dates into real Excel dates, then display them in the
    same format, such as `dd-mmm-yyyy`.
4.  Convert all fees to numeric values and apply one currency format. Do
    not leave `KES 30,000` as text.
5.  Convert all attendance values to numeric percentages.
6.  Check whether Excel recognizes each date as a date rather than text.
7.  Document any value that cannot be interpreted confidently.

**Useful functions:** `=TRIM(B2)`, `=PROPER(TRIM(B2))`

**Expected result:** Consistent names, dates, currency values and
percentages.

**Note:** Date interpretation can depend on the computer's regional
settings. Check the resulting values rather than relying only on how
they look.

------------------------------------------------------------------------

## Practical 5: Sorting and Filtering Records

**Objective:** Retrieve subsets of a dataset and arrange records
meaningfully.

### Dataset

Enter this data in `P5_SortFilter`.

  Student_ID   Student_Name    Course             Marks Fee_Status
  ------------ --------------- ---------------- ------- ------------
  ADM001       Amina Otieno    Graphic Design        78 Paid
  ADM002       Brian Mwangi    Film                  64 Pending
  ADM003       Wanjiku Njeri   Animation             91 Paid
  ADM004       Kevin Ouma      Graphic Design        49 Pending
  ADM005       Mary Achieng    Animation             82 Paid
  ADM006       Peter Kamau     Film                  55 Paid
  ADM007       Faith Wairimu   Graphic Design        88 Pending

### Tasks

1.  Sort students by `Marks` from largest to smallest.
2.  Sort by `Course` A--Z, then by `Marks` largest to smallest.
3.  Filter the records to show only `Graphic Design` students.
4.  Filter to show students with marks below 50.
5.  Filter to show students whose `Fee_Status` is `Pending`.
6.  Combine filters to find `Graphic Design` students with pending fees.
7.  Clear all filters and confirm that no records were deleted.

**Expected result:** The requested subsets can be displayed without
changing the underlying dataset.

------------------------------------------------------------------------

## Practical 6: Find and Replace

**Objective:** Correct repeated text errors efficiently and understand
the risks of broad replacements.

### Dataset

Enter this data in `P6_FindReplace`.

  Student_ID   Course           Campus
  ------------ ---------------- ---------
  ADM001       Graphic design   Nairobi
  ADM002       Graphic Design   Nairobi
  ADM003       Graphic Design   Nrb
  ADM004       Graphic design   Nrb
  ADM005       Film             Nairobi

### Tasks

1.  Use **Find** to locate every instance of `Nrb`.
2.  Use **Replace** to replace `Nrb` with `Nairobi`.
3.  Standardize `Graphic design` to `Graphic Design`.
4.  Before replacing, inspect the options for searching within the
    current sheet versus the entire workbook.
5.  Test **Replace All** on a copy of the data first.
6.  Explain why replacing a short word or number across an entire
    workbook can cause unintended changes.

**Expected result:** Consistent course and campus labels.

------------------------------------------------------------------------

## Practical 7: Text to Columns, TRIM and Text Functions

**Objective:** Split, clean and extract information from text fields.

### Dataset

Enter this data in `P7_TextFunctions`.

  Full_Name       Contact_Details      Student_Code
  --------------- -------------------- --------------
  Amina Otieno    Nairobi,0712345678   ADM-2026-001
  Brian Mwangi    Mombasa,0723456789   ADM-2026-002
  Wanjiku Njeri   Kisumu,0734567890    ADM-2026-003
  Kevin Ouma      Nairobi,0745678901   ADM-2026-004

### Tasks

1.  Use **Data → Text to Columns**, choosing comma as the delimiter, to
    split `Contact_Details` into `City` and `Phone`.
2.  Split `Full_Name` into first and last name. Consider what might
    happen with names containing more than two words.
3.  Use `TRIM` to remove unnecessary spaces from a deliberately messy
    copy of the data.
4.  Use `LEFT` to extract the prefix `ADM` from `Student_Code`.
5.  Use `RIGHT` to extract the final three digits of the code.
6.  Use `MID` to extract `2026` from the student code.
7.  Use `LEN` to count the characters in a student code.
8.  Use `CONCAT` or `TEXTJOIN` to combine first and last names.
9.  Keep phone numbers as text so their leading zero is not lost.

**Example formulas** (assuming the value is in A2):

-   `=LEFT(A2,3)`
-   `=RIGHT(A2,3)`
-   `=MID(A2,5,4)`
-   `=LEN(A2)`
-   `=TRIM(A2)`

**Expected result:** Separate, clean and reusable fields for analysis.

------------------------------------------------------------------------

## Practical 8: Excel Tables, Structured References and Column Naming

**Objective:** Organize records in an Excel Table and use formulas that
remain readable as the table grows.

### Tasks

1.  Enter the following data in `P8_Tables`.

  Student_ID   Student_Name    Course             Marks
  ------------ --------------- ---------------- -------
  ADM001       Amina Otieno    Graphic Design        78
  ADM002       Brian Mwangi    Film                  64
  ADM003       Wanjiku Njeri   Animation             91
  ADM004       Kevin Ouma      Graphic Design        49

2.  Select the data and use **Insert → Table** (or **Home → Format as
    Table**). Confirm that the table has headers.

3.  Rename the table `Students`.

4.  Use clear, unique column names without blank headings, such as
    `Student_ID` and `Marks`.

5.  Add a `Result` column. In the first data row, enter:

    `=IF([@Marks]>=50,"Pass","Fail")`

6.  Add a `Fee_KES` column and enter sample fee amounts.

7.  Add a new student row and observe whether the table expands and the
    formula fills automatically.

8.  Use the table's filter arrows to display only students who passed.

9.  Explain one advantage of a named Excel Table over a fixed range such
    as `A1:D5`.

**Expected result:** A structured, expandable table with formulas and
filters.

------------------------------------------------------------------------

## Practical 9: Data Integrity and Quality Control

**Objective:** Apply rules that help ensure records are complete, valid
and consistent.

### Dataset

Create a worksheet named `P9_QualityControl`.

  Student_ID   Student_Name   Course             Marks Email
  ------------ -------------- ---------------- ------- -------------------
  ADM001       Amina Otieno   Graphic Design        78 amina@example.com
  ADM002       Brian Mwangi   Film                  64 brian@example.com
  ADM002       Brian Mwangi   Film                  64 brian@example.com
  ADM004       Kevin Ouma     Graphic Design       115 kevin.example.com
               Mary Achieng   Animation             82 mary@example.com

### Tasks

1.  Identify duplicate `Student_ID` values.
2.  Identify the missing student ID.
3.  Flag marks below 0 or above 100.
4.  Inspect email values for an `@` symbol and a dot after it. Treat
    this as a basic screening rule, not proof that an email address
    exists.
5.  Apply data validation to prevent invalid marks and duplicate IDs in
    future entries.
6.  Use conditional formatting to highlight duplicate IDs, blanks and
    out-of-range marks.
7.  Create a `Quality_Status` column that flags records for review.
8.  Produce a short report stating how many issues were found and how
    they should be resolved.

**Possible duplicate-check formula** (assuming IDs are in A2:A100):

`=COUNTIF($A$2:$A$100,A2)>1`

**Expected result:** A quality-control sheet that identifies records
requiring review.

------------------------------------------------------------------------

## Practical 10: Protecting Worksheets and Locking Formula Cells

**Objective:** Protect formulas from accidental edits while allowing
users to enter permitted data.

### Tasks

1.  Create a worksheet named `P10_Protection` with columns `Item`,
    `Quantity`, `Unit_Price` and `Total`.
2.  Enter three sample products.
3.  In the `Total` column, calculate each line total using `=B2*C2`.
4.  Decide which cells users should be allowed to edit and which contain
    formulas.
5.  Select the input cells, open **Format Cells → Protection**, and
    clear **Locked**.
6.  Leave formula cells locked.
7.  Use **Review → Protect Sheet**. Set a password only if instructed by
    your teacher; do not use a sensitive personal password.
8.  Test whether you can edit input cells and whether you can overwrite
    formula cells.
9.  Unprotect the sheet if authorized and explain the difference between
    worksheet protection and file encryption.

**Expected result:** Users can edit input fields but cannot accidentally
overwrite protected formula cells.

**Important:** Worksheet protection helps prevent accidental changes; it
is not strong security for confidential information.

------------------------------------------------------------------------

## Practical 11: Relative, Absolute and Mixed Cell References

**Objective:** Understand how cell references change when formulas are
copied.

### Dataset

Enter this data in `P11_References`.

  Product            Quantity   Unit_Price_KES   Line_Total
  ---------------- ---------- ---------------- ------------
  Wallpaper Roll            3             1800 
  Wall Panel                5             2500 
  Window Film               2             1200 

In cell `F1`, enter the tax rate `16%`. Label E1 `Tax_Rate`.

### Tasks

1.  **Relative reference:** In D2, calculate the line total using
    `=B2*C2`. Copy the formula down. Observe how the references change.
2.  **Absolute reference:** Add a `Tax` column and calculate tax using a
    formula such as `=D2*$F$1`. Copy it down and observe that `$F$1`
    stays fixed.
3.  **Mixed reference:** Create a small price comparison grid with
    quantities in `B2:B4` and unit prices across `C1:E1`. Use a formula
    with a mixed reference, such as `=$B2*C$1`, then copy it across and
    down.
4.  Explain why the dollar sign is needed in an absolute or mixed
    reference.
5.  Check your calculations manually for one row.

**Expected result:** Correct formulas that can be copied across rows and
columns without breaking the intended references.

------------------------------------------------------------------------

## Practical 12: VLOOKUP --- Retrieve Related Information

**Objective:** Use `VLOOKUP` to find a value in a reference table and
return related information.

### Dataset A: Course Reference

Create a worksheet named `Course_Reference`.

  Course_Code   Course_Name           Tuition_KES
  ------------- ------------------- -------------
  GD01          Graphic Design              25000
  FM01          Film                        30000
  AN01          Animation                   28000
  DM01          Digital Marketing           22000

### Dataset B: Student Registration

Create another worksheet named `P12_VLOOKUP`.

  Student_ID   Student_Name    Course_Code   Course_Name     Tuition_KES
  ------------ --------------- ------------- ------------- -------------
  ADM001       Amina Otieno    GD01                        
  ADM002       Brian Mwangi    FM01                        
  ADM003       Wanjiku Njeri   AN01                        
  ADM004       Kevin Ouma      GD01                        

### Tasks

1.  Use `VLOOKUP` to retrieve `Course_Name` from the `Course_Reference`
    worksheet.
2.  Use `VLOOKUP` to retrieve `Tuition_KES` from the same reference
    table.
3.  Use an **exact match** by setting the final argument to `FALSE`.
4.  Test what happens when a student has an unknown course code such as
    `XX01`.
5.  Improve the formula using `IFERROR` so missing course codes display
    `Not found`.
6.  Explain why the lookup value must be in the first column of the
    selected table range when using `VLOOKUP`.
7.  Add a new course to the reference table and consider how to keep the
    lookup range up to date.

**Example formula** (if the reference table is in
`Course_Reference!A2:C5` and the code is in C2):

`=VLOOKUP(C2,Course_Reference!$A$2:$C$5,2,FALSE)`

To retrieve the tuition fee:

`=VLOOKUP(C2,Course_Reference!$A$2:$C$5,3,FALSE)`

To handle missing codes:

`=IFERROR(VLOOKUP(C2,Course_Reference!$A$2:$C$5,2,FALSE),"Not found")`

**Expected result:** Course names and tuition amounts populate
automatically based on each student's course code.

------------------------------------------------------------------------

## Final Assessment: Build a Student Registration and Quality-Control Workbook

Create a workbook that combines the skills from these practicals.

### Requirements

-   A student registration table with at least 30 records.
-   Appropriate data types and number formats.
-   Drop-down validation for courses.
-   Marks validation between 0 and 100.
-   Duplicate and blank checks.
-   Standardized names, dates and currency values.
-   Sorting and filtering.
-   At least three formulas, including an `IF` formula.
-   An Excel Table with meaningful column names.
-   Protected formula cells.
-   At least one example each of relative, absolute and mixed
    references.
-   A `VLOOKUP` that retrieves a course name or tuition fee from a
    reference table.
-   A short quality-control summary describing errors found and
    corrected.

### Suggested marking rubric

  Criterion                                 Marks
  ------------------------------------- ---------
  Data types and formatting                    10
  Validation and data integrity                15
  Cleaning and standardization                 15
  Sorting, filtering and Find/Replace          10
  Text functions and Excel Tables              15
  Formulas and cell references                 15
  VLOOKUP and error handling                   10
  Protection and documentation                 10
  **Total**                               **100**

## Submission checklist

-   [ ] Workbook contains clearly named worksheets.
-   [ ] Original data is preserved where cleaning was required.
-   [ ] Validation rules have been tested.
-   [ ] Formulas return correct results.
-   [ ] Lookup formulas use exact matching.
-   [ ] Invalid or missing data is flagged rather than guessed.
-   [ ] Formula cells are protected where required.
-   [ ] Final workbook and quality-control summary are saved.
