# Data Dictionary — `HR_Data`

**Source:** `HR_Dashboard_Mock_Data.xlsx`, sheet `HR_Data` (the workbook also has `Read_Me` and `KPI_Summary` sheets, which are not loaded).
**Grain:** one row per employee per month (monthly snapshot). 106,903 rows, Jan 2024 – Dec 2025.
**Model:** a single flat import table. No relationships, no dimension tables. Measures live in a separate `_measures` table (see [measures.md](measures.md)).

> All data is synthetic mock data generated for this portfolio project. No real employees.

## Source columns

| Column | Type | Description | Values / range |
|---|---|---|---|
| Snapshot_Month | Int64 | First day of the snapshot month, stored as an Excel date serial (keeps PY logic simple without a date table) | Jan 2024 – Dec 2025 |
| Year | Int64 | Calendar year of the snapshot | 2024, 2025 |
| Month | Text | Month abbreviation (sorted by `Month No`) | Jan – Dec |
| Employee_ID | Text | Employee key | EMP00001 … |
| Department | Text | Department | Customer Service, Engineering, Finance, Human Resources, IT, Marketing, Operations, Sales |
| Job_Level | Text | Job level (use `Job Level` in visuals for correct sort) | Entry, Associate, Senior, Manager, Director |
| Gender | Text | Gender | Female, Male |
| Age | Int64 | Age in years | 21 – 74 |
| Age_Band | Text | Age band (use `Age Band` in visuals for correct sort) | <25, 25-34, 35-44, 45-54, 55+ |
| Location | Text | Work location (Malaysia) | Johor Bahru, Kota Kinabalu, Kuala Lumpur, Penang, Petaling Jaya, Shah Alam |
| Employment_Type | Text | Contract type | Permanent, Contract, Intern |
| Hire_Date | Int64 | Hire date (Excel date serial) | 1982 – 2025 |
| Tenure_Years | Decimal | Years of service at the snapshot | 0 – 42.7 |
| Monthly_Salary_MYR | Int64 | Base monthly salary (MYR) | 2,720 – 31,190 |
| Performance_Rating | Int64 | Latest performance rating | 1 (Low) – 5 (High) |
| Engagement_Score | Decimal | Monthly engagement pulse score | 1.1 – 5.0 |
| Absence_Days | Int64 | Unplanned absence days in the month | 0 – 9 |
| Overtime_Hours | Decimal | Overtime hours in the month | 0 – 25.8 |
| Training_Hours | Decimal | Training hours in the month | 0 – 10.7 |
| New_Hire_Flag | Int64 | 1 if the employee joined in this month | 0 / 1 |
| Exit_Flag | Int64 | 1 if the employee left in this month | 0 / 1 |
| Exit_Type | Text | Exit type (exit rows only) | Voluntary, Involuntary |
| Exit_Reason | Text | Exit reason (exit rows only) | Better Compensation, Career Growth, Contract End, Further Studies, Management Issues, Misconduct, Performance, Relocation, Restructuring, Work-Life Balance |

## Calculated columns (DAX)

| Column | Expression | Purpose |
|---|---|---|
| Month No | `MONTH ( DATE ( 1899, 12, 30 ) + HR_Data[Snapshot_Month] )` | Sort key for `Month` |
| Year Month | `FORMAT ( DATE ( 1899, 12, 30 ) + HR_Data[Snapshot_Month], "mmm yy" )` | Trend axis label, sorted by `Snapshot_Month` |
| Year Quarter No | `HR_Data[Year] * 10 + ROUNDUP ( HR_Data[Month No] / 3, 0 )` | Sort key for `Year Quarter` |
| Year Quarter | `HR_Data[Year] & " Q" & ROUNDUP ( HR_Data[Month No] / 3, 0 )` | Drill level above `Year Month` |
| Job Level Order | `SWITCH ( HR_Data[Job_Level], "Entry", 1, … "Director", 5, 99 )` | Sort key |
| Job Level | `HR_Data[Job_Level]` | Display copy sorted by `Job Level Order` |
| Age Band Order | `SWITCH ( HR_Data[Age_Band], "<25", 1, … "55+", 5, 99 )` | Sort key |
| Age Band | `HR_Data[Age_Band]` | Display copy sorted by `Age Band Order` |
| Rating Label | `"1 · Low"`, `"2"`, `"3 · Meets"`, `"4"`, `"5 · High"` | Rating axis label, sorted by `Performance_Rating` |

> **Why the copy columns?** Sorting `Job_Level` by a calculated column that is itself derived from `Job_Level` creates a circular dependency. The display copies (`Job Level`, `Age Band`) carry the sort instead, and the original columns stay unsorted.

## Parameter

| Name | Type | Purpose |
|---|---|---|
| Source File Path | Text (Power Query parameter) | Full path to `HR_Dashboard_Mock_Data.xlsx`. Change it in **Transform data → Manage parameters** after cloning. |
