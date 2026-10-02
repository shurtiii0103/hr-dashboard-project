# DAX Measure Catalogue

All 51 measures live in the `_measures` table and calculate over the single flat table `HR_Data` (no relationships, no dimension tables).

Generated from `HR Dashboard.SemanticModel/definition/tables/_measures.tmdl`.

## Key patterns

- **Headcount is end-of-period**: rows are monthly snapshots, so headcount counts rows in the latest `Snapshot_Month` in context (not a distinct count across months).
- **Attrition Rate** = Exits ÷ average monthly headcount over the period.
- **Previous Year (PY)**: `Snapshot_Month` is an Excel date serial (Int64). PY measures shift each month in context back 12 months with `EDATE`, convert back to a serial, clear all date-column filters with `REMOVEFILTERS` and re-apply the shifted months with `TREATAS`. No date table needed.
- **KPI card labels**: every KPI has `PY Label` (caption text), `Change Label` (▲/▼ % vs PY) and a hidden `Change Color` (green favourable / red unfavourable — for Attrition and Absence, lower is better).
- **Formatting measures** return hex colours or text and drive conditional formatting / dynamic subtitles in the report.

## Summary

| Folder | Measure | Format | Description |
|---|---|---|---|
| 1. Workforce | Headcount | `#,##0` | Active employees in the latest month of the selected period (end-of-period headcount). |
| 1. Workforce | New Hires | `#,##0` | Employees who joined during the selected period. |
| 1. Workforce | Exits | `#,##0` | Employees who left during the selected period. |
| 1. Workforce | Net Change | `+#,##0;-#,##0;0` | New hires minus exits. |
| 1. Workforce | Avg Monthly Headcount | `#,##0` | Average monthly headcount across the months in the selected period. |
| 1. Workforce | Attrition Rate | `0.0%` | Exits divided by average monthly headcount for the selected period. |
| 1. Workforce | Avg Absence Days | `0.00` | Average unplanned absence days per employee per month. |
| 1. Workforce | Avg Engagement Score | `0.00` | Average monthly engagement score (1-5). |
| 1. Workforce | Attrition Rate Company Avg | `0.0%` | Attrition across all departments, other filters kept. Reference line on the department chart. |
| 2. Pay & Performance | Avg Monthly Salary | `"MYR" #,##0` | Average base monthly salary in MYR. |
| 2. Pay & Performance | Avg Performance Rating | `0.00` | Average performance rating (1-5). |
| 2. Pay & Performance | Avg Training Hours | `0.00` | Average training hours per employee per month. |
| 2. Pay & Performance | Avg Overtime Hours | `0.00` | Average overtime hours per employee per month. |
| 2. Pay & Performance | Employees % of Total | `0.0%` | Share of end-of-period headcount in each performance rating. |
| 1. Workforce\Previous Year | Headcount PY | `#,##0` | Headcount for the same months one year earlier. |
| 1. Workforce\Previous Year | Attrition Rate PY | `0.0%` | Attrition Rate for the same months one year earlier. |
| 1. Workforce\Previous Year | Avg Absence Days PY | `0.00` | Avg Absence Days for the same months one year earlier. |
| 1. Workforce\Previous Year | Avg Engagement Score PY | `0.00` | Avg Engagement Score for the same months one year earlier. |
| 1. Workforce\KPI Labels | Headcount PY Label | `—` | KPI card caption: previous-year value for Headcount. |
| 1. Workforce\KPI Labels | Headcount Change Label | `—` | KPI card delta vs previous year for Headcount. |
| 1. Workforce\KPI Labels | Headcount Change Color *(hidden)* | `—` | Green when the change is favourable, red when not. |
| 1. Workforce\KPI Labels | Attrition Rate PY Label | `—` | KPI card caption: previous-year value for Attrition Rate. |
| 1. Workforce\KPI Labels | Attrition Rate Change Label | `—` | KPI card delta vs previous year for Attrition Rate. |
| 1. Workforce\KPI Labels | Attrition Rate Change Color *(hidden)* | `—` | Green when the change is favourable, red when not (lower is better). |
| 1. Workforce\KPI Labels | Avg Absence Days PY Label | `—` | KPI card caption: previous-year value for Avg Absence Days. |
| 1. Workforce\KPI Labels | Avg Absence Days Change Label | `—` | KPI card delta vs previous year for Avg Absence Days. |
| 1. Workforce\KPI Labels | Avg Absence Days Change Color *(hidden)* | `—` | Green when the change is favourable, red when not (lower is better). |
| 1. Workforce\KPI Labels | Avg Engagement Score PY Label | `—` | KPI card caption: previous-year value for Avg Engagement Score. |
| 1. Workforce\KPI Labels | Avg Engagement Score Change Label | `—` | KPI card delta vs previous year for Avg Engagement Score. |
| 1. Workforce\KPI Labels | Avg Engagement Score Change Color *(hidden)* | `—` | Green when the change is favourable, red when not. |
| 2. Pay & Performance\Previous Year | Avg Monthly Salary PY | `"MYR" #,##0` | Avg Monthly Salary for the same months one year earlier. |
| 2. Pay & Performance\Previous Year | Avg Performance Rating PY | `0.00` | Avg Performance Rating for the same months one year earlier. |
| 2. Pay & Performance\Previous Year | Avg Training Hours PY | `0.00` | Avg Training Hours for the same months one year earlier. |
| 2. Pay & Performance\Previous Year | Avg Overtime Hours PY | `0.00` | Avg Overtime Hours for the same months one year earlier. |
| 2. Pay & Performance\KPI Labels | Avg Monthly Salary PY Label | `—` | KPI card caption: previous-year value for Avg Monthly Salary. |
| 2. Pay & Performance\KPI Labels | Avg Monthly Salary Change Label | `—` | KPI card delta vs previous year for Avg Monthly Salary. |
| 2. Pay & Performance\KPI Labels | Avg Monthly Salary Change Color *(hidden)* | `—` | Green when the change is favourable, red when not. |
| 2. Pay & Performance\KPI Labels | Avg Performance Rating PY Label | `—` | KPI card caption: previous-year value for Avg Performance Rating. |
| 2. Pay & Performance\KPI Labels | Avg Performance Rating Change Label | `—` | KPI card delta vs previous year for Avg Performance Rating. |
| 2. Pay & Performance\KPI Labels | Avg Performance Rating Change Color *(hidden)* | `—` | Green when the change is favourable, red when not. |
| 2. Pay & Performance\KPI Labels | Avg Training Hours PY Label | `—` | KPI card caption: previous-year value for Avg Training Hours. |
| 2. Pay & Performance\KPI Labels | Avg Training Hours Change Label | `—` | KPI card delta vs previous year for Avg Training Hours. |
| 2. Pay & Performance\KPI Labels | Avg Training Hours Change Color *(hidden)* | `—` | Green when the change is favourable, red when not. |
| 2. Pay & Performance\KPI Labels | Avg Overtime Hours PY Label | `—` | KPI card caption: previous-year value for Avg Overtime Hours. |
| 2. Pay & Performance\KPI Labels | Avg Overtime Hours Change Label | `—` | KPI card delta vs previous year for Avg Overtime Hours. |
| 2. Pay & Performance\KPI Labels | Avg Overtime Hours Change Color *(hidden)* | `—` | Green when the change is favourable, red when not (lower is better). |
| 1. Workforce\Formatting | Attrition Bar Color *(hidden)* | `—` | Red above company average, green otherwise. |
| 1. Workforce\Formatting | Exit Type Summary | `—` | Subtitle for the exit reasons chart. |
| 1. Workforce\Formatting | Gender Subtitle | `—` | Subtitle for the gender split chart. |
| 2. Pay & Performance\Formatting | Rating Subtitle | `—` | Subtitle for the rating distribution chart. |
| 2. Pay & Performance\Formatting | Rating Bar Color *(hidden)* | `—` | Red for ratings 1-2, grey for 3, green for 4-5. |

## Definitions

### 1. Workforce

#### Headcount

Active employees in the latest month of the selected period (end-of-period headcount).

```dax
Headcount =
VAR _lastMonth = MAX ( HR_Data[Snapshot_Month] )
RETURN
    CALCULATE ( COUNTROWS ( HR_Data ), HR_Data[Snapshot_Month] = _lastMonth )
```

#### New Hires

Employees who joined during the selected period.

```dax
New Hires =
CALCULATE ( COUNTROWS ( HR_Data ), HR_Data[New_Hire_Flag] = 1 )
```

#### Exits

Employees who left during the selected period.

```dax
Exits =
CALCULATE ( COUNTROWS ( HR_Data ), HR_Data[Exit_Flag] = 1 )
```

#### Net Change

New hires minus exits.

```dax
Net Change =
[New Hires] - [Exits]
```

#### Avg Monthly Headcount

Average monthly headcount across the months in the selected period.

```dax
Avg Monthly Headcount =
AVERAGEX ( VALUES ( HR_Data[Snapshot_Month] ), CALCULATE ( COUNTROWS ( HR_Data ) ) )
```

#### Attrition Rate

Exits divided by average monthly headcount for the selected period.

```dax
Attrition Rate =
DIVIDE ( [Exits], [Avg Monthly Headcount] )
```

#### Avg Absence Days

Average unplanned absence days per employee per month.

```dax
Avg Absence Days =
AVERAGE ( HR_Data[Absence_Days] )
```

#### Avg Engagement Score

Average monthly engagement score (1-5).

```dax
Avg Engagement Score =
AVERAGE ( HR_Data[Engagement_Score] )
```

#### Attrition Rate Company Avg

Attrition across all departments, other filters kept. Reference line on the department chart.

```dax
Attrition Rate Company Avg =
CALCULATE ( [Attrition Rate], REMOVEFILTERS ( HR_Data[Department] ) )
```

### 2. Pay & Performance

#### Avg Monthly Salary

Average base monthly salary in MYR.

```dax
Avg Monthly Salary =
AVERAGE ( HR_Data[Monthly_Salary_MYR] )
```

#### Avg Performance Rating

Average performance rating (1-5).

```dax
Avg Performance Rating =
AVERAGE ( HR_Data[Performance_Rating] )
```

#### Avg Training Hours

Average training hours per employee per month.

```dax
Avg Training Hours =
AVERAGE ( HR_Data[Training_Hours] )
```

#### Avg Overtime Hours

Average overtime hours per employee per month.

```dax
Avg Overtime Hours =
AVERAGE ( HR_Data[Overtime_Hours] )
```

#### Employees % of Total

Share of end-of-period headcount in each performance rating.

```dax
Employees % of Total =
DIVIDE ( [Headcount], CALCULATE ( [Headcount], REMOVEFILTERS ( HR_Data[Performance_Rating], HR_Data[Rating Label] ) ) )
```

### 1. Workforce\Previous Year

#### Headcount PY

Headcount for the same months one year earlier.

```dax
Headcount PY =
VAR _pyMonths =
    SELECTCOLUMNS (
        VALUES ( HR_Data[Snapshot_Month] ),
        "PY Month", INT ( EDATE ( DATE ( 1899, 12, 30 ) + HR_Data[Snapshot_Month], -12 ) - DATE ( 1899, 12, 30 ) )
    )
RETURN
    CALCULATE (
        [Headcount],
        REMOVEFILTERS ( HR_Data[Year], HR_Data[Month], HR_Data[Month No], HR_Data[Snapshot_Month], HR_Data[Year Month], HR_Data[Year Quarter], HR_Data[Year Quarter No] ),
        TREATAS ( _pyMonths, HR_Data[Snapshot_Month] )
    )
```

#### Attrition Rate PY

Attrition Rate for the same months one year earlier.

```dax
Attrition Rate PY =
VAR _pyMonths =
    SELECTCOLUMNS (
        VALUES ( HR_Data[Snapshot_Month] ),
        "PY Month", INT ( EDATE ( DATE ( 1899, 12, 30 ) + HR_Data[Snapshot_Month], -12 ) - DATE ( 1899, 12, 30 ) )
    )
RETURN
    CALCULATE (
        [Attrition Rate],
        REMOVEFILTERS ( HR_Data[Year], HR_Data[Month], HR_Data[Month No], HR_Data[Snapshot_Month], HR_Data[Year Month], HR_Data[Year Quarter], HR_Data[Year Quarter No] ),
        TREATAS ( _pyMonths, HR_Data[Snapshot_Month] )
    )
```

#### Avg Absence Days PY

Avg Absence Days for the same months one year earlier.

```dax
Avg Absence Days PY =
VAR _pyMonths =
    SELECTCOLUMNS (
        VALUES ( HR_Data[Snapshot_Month] ),
        "PY Month", INT ( EDATE ( DATE ( 1899, 12, 30 ) + HR_Data[Snapshot_Month], -12 ) - DATE ( 1899, 12, 30 ) )
    )
RETURN
    CALCULATE (
        [Avg Absence Days],
        REMOVEFILTERS ( HR_Data[Year], HR_Data[Month], HR_Data[Month No], HR_Data[Snapshot_Month], HR_Data[Year Month], HR_Data[Year Quarter], HR_Data[Year Quarter No] ),
        TREATAS ( _pyMonths, HR_Data[Snapshot_Month] )
    )
```

#### Avg Engagement Score PY

Avg Engagement Score for the same months one year earlier.

```dax
Avg Engagement Score PY =
VAR _pyMonths =
    SELECTCOLUMNS (
        VALUES ( HR_Data[Snapshot_Month] ),
        "PY Month", INT ( EDATE ( DATE ( 1899, 12, 30 ) + HR_Data[Snapshot_Month], -12 ) - DATE ( 1899, 12, 30 ) )
    )
RETURN
    CALCULATE (
        [Avg Engagement Score],
        REMOVEFILTERS ( HR_Data[Year], HR_Data[Month], HR_Data[Month No], HR_Data[Snapshot_Month], HR_Data[Year Month], HR_Data[Year Quarter], HR_Data[Year Quarter No] ),
        TREATAS ( _pyMonths, HR_Data[Snapshot_Month] )
    )
```

### 1. Workforce\KPI Labels

#### Headcount PY Label

KPI card caption: previous-year value for Headcount.

```dax
Headcount PY Label =
VAR _py = [Headcount PY]
RETURN
    "As of " & FORMAT ( DATE ( 1899, 12, 30 ) + MAX ( HR_Data[Snapshot_Month] ), "mmm yyyy" ) & " · " & "Previous Year: " & IF ( ISBLANK ( _py ), "n/a", FORMAT ( _py, "#,##0" ) )
```

#### Headcount Change Label

KPI card delta vs previous year for Headcount.

```dax
Headcount Change Label =
VAR _cur = [Headcount]
VAR _py = [Headcount PY]
VAR _chg = DIVIDE ( _cur - _py, _py )
RETURN
    IF ( ISBLANK ( _py ) || ISBLANK ( _cur ), BLANK (), IF ( _chg > 0, "▲ ", IF ( _chg < 0, "▼ ", "■ " ) ) & FORMAT ( ABS ( _chg ), "0.0%" ) )
```

#### Headcount Change Color

Green when the change is favourable, red when not.

```dax
Headcount Change Color =
VAR _cur = [Headcount]
VAR _py = [Headcount PY]
RETURN
    IF ( ISBLANK ( _py ) || ISBLANK ( _cur ), "#8C8C8C", IF ( _cur >= _py, "#008E60", "#D8211D" ) )
```

#### Attrition Rate PY Label

KPI card caption: previous-year value for Attrition Rate.

```dax
Attrition Rate PY Label =
VAR _py = [Attrition Rate PY]
RETURN
    "Previous Year: " & IF ( ISBLANK ( _py ), "n/a", FORMAT ( _py, "0.0%" ) )
```

#### Attrition Rate Change Label

KPI card delta vs previous year for Attrition Rate.

```dax
Attrition Rate Change Label =
VAR _cur = [Attrition Rate]
VAR _py = [Attrition Rate PY]
VAR _chg = ( _cur - _py ) * 100
RETURN
    IF ( ISBLANK ( _py ) || ISBLANK ( _cur ), BLANK (), IF ( _chg > 0, "▲ ", IF ( _chg < 0, "▼ ", "■ " ) ) & FORMAT ( ABS ( _chg ), "0.0" ) & " pts" )
```

#### Attrition Rate Change Color

Green when the change is favourable, red when not (lower is better).

```dax
Attrition Rate Change Color =
VAR _cur = [Attrition Rate]
VAR _py = [Attrition Rate PY]
RETURN
    IF ( ISBLANK ( _py ) || ISBLANK ( _cur ), "#8C8C8C", IF ( _cur <= _py, "#008E60", "#D8211D" ) )
```

#### Avg Absence Days PY Label

KPI card caption: previous-year value for Avg Absence Days.

```dax
Avg Absence Days PY Label =
VAR _py = [Avg Absence Days PY]
RETURN
    "Previous Year: " & IF ( ISBLANK ( _py ), "n/a", FORMAT ( _py, "0.00" ) )
```

#### Avg Absence Days Change Label

KPI card delta vs previous year for Avg Absence Days.

```dax
Avg Absence Days Change Label =
VAR _cur = [Avg Absence Days]
VAR _py = [Avg Absence Days PY]
VAR _chg = DIVIDE ( _cur - _py, _py )
RETURN
    IF ( ISBLANK ( _py ) || ISBLANK ( _cur ), BLANK (), IF ( _chg > 0, "▲ ", IF ( _chg < 0, "▼ ", "■ " ) ) & FORMAT ( ABS ( _chg ), "0.0%" ) )
```

#### Avg Absence Days Change Color

Green when the change is favourable, red when not (lower is better).

```dax
Avg Absence Days Change Color =
VAR _cur = [Avg Absence Days]
VAR _py = [Avg Absence Days PY]
RETURN
    IF ( ISBLANK ( _py ) || ISBLANK ( _cur ), "#8C8C8C", IF ( _cur <= _py, "#008E60", "#D8211D" ) )
```

#### Avg Engagement Score PY Label

KPI card caption: previous-year value for Avg Engagement Score.

```dax
Avg Engagement Score PY Label =
VAR _py = [Avg Engagement Score PY]
RETURN
    "Previous Year: " & IF ( ISBLANK ( _py ), "n/a", FORMAT ( _py, "0.00" ) )
```

#### Avg Engagement Score Change Label

KPI card delta vs previous year for Avg Engagement Score.

```dax
Avg Engagement Score Change Label =
VAR _cur = [Avg Engagement Score]
VAR _py = [Avg Engagement Score PY]
VAR _chg = DIVIDE ( _cur - _py, _py )
RETURN
    IF ( ISBLANK ( _py ) || ISBLANK ( _cur ), BLANK (), IF ( _chg > 0, "▲ ", IF ( _chg < 0, "▼ ", "■ " ) ) & FORMAT ( ABS ( _chg ), "0.0%" ) )
```

#### Avg Engagement Score Change Color

Green when the change is favourable, red when not.

```dax
Avg Engagement Score Change Color =
VAR _cur = [Avg Engagement Score]
VAR _py = [Avg Engagement Score PY]
RETURN
    IF ( ISBLANK ( _py ) || ISBLANK ( _cur ), "#8C8C8C", IF ( _cur >= _py, "#008E60", "#D8211D" ) )
```

### 2. Pay & Performance\Previous Year

#### Avg Monthly Salary PY

Avg Monthly Salary for the same months one year earlier.

```dax
Avg Monthly Salary PY =
VAR _pyMonths =
    SELECTCOLUMNS (
        VALUES ( HR_Data[Snapshot_Month] ),
        "PY Month", INT ( EDATE ( DATE ( 1899, 12, 30 ) + HR_Data[Snapshot_Month], -12 ) - DATE ( 1899, 12, 30 ) )
    )
RETURN
    CALCULATE (
        [Avg Monthly Salary],
        REMOVEFILTERS ( HR_Data[Year], HR_Data[Month], HR_Data[Month No], HR_Data[Snapshot_Month], HR_Data[Year Month], HR_Data[Year Quarter], HR_Data[Year Quarter No] ),
        TREATAS ( _pyMonths, HR_Data[Snapshot_Month] )
    )
```

#### Avg Performance Rating PY

Avg Performance Rating for the same months one year earlier.

```dax
Avg Performance Rating PY =
VAR _pyMonths =
    SELECTCOLUMNS (
        VALUES ( HR_Data[Snapshot_Month] ),
        "PY Month", INT ( EDATE ( DATE ( 1899, 12, 30 ) + HR_Data[Snapshot_Month], -12 ) - DATE ( 1899, 12, 30 ) )
    )
RETURN
    CALCULATE (
        [Avg Performance Rating],
        REMOVEFILTERS ( HR_Data[Year], HR_Data[Month], HR_Data[Month No], HR_Data[Snapshot_Month], HR_Data[Year Month], HR_Data[Year Quarter], HR_Data[Year Quarter No] ),
        TREATAS ( _pyMonths, HR_Data[Snapshot_Month] )
    )
```

#### Avg Training Hours PY

Avg Training Hours for the same months one year earlier.

```dax
Avg Training Hours PY =
VAR _pyMonths =
    SELECTCOLUMNS (
        VALUES ( HR_Data[Snapshot_Month] ),
        "PY Month", INT ( EDATE ( DATE ( 1899, 12, 30 ) + HR_Data[Snapshot_Month], -12 ) - DATE ( 1899, 12, 30 ) )
    )
RETURN
    CALCULATE (
        [Avg Training Hours],
        REMOVEFILTERS ( HR_Data[Year], HR_Data[Month], HR_Data[Month No], HR_Data[Snapshot_Month], HR_Data[Year Month], HR_Data[Year Quarter], HR_Data[Year Quarter No] ),
        TREATAS ( _pyMonths, HR_Data[Snapshot_Month] )
    )
```

#### Avg Overtime Hours PY

Avg Overtime Hours for the same months one year earlier.

```dax
Avg Overtime Hours PY =
VAR _pyMonths =
    SELECTCOLUMNS (
        VALUES ( HR_Data[Snapshot_Month] ),
        "PY Month", INT ( EDATE ( DATE ( 1899, 12, 30 ) + HR_Data[Snapshot_Month], -12 ) - DATE ( 1899, 12, 30 ) )
    )
RETURN
    CALCULATE (
        [Avg Overtime Hours],
        REMOVEFILTERS ( HR_Data[Year], HR_Data[Month], HR_Data[Month No], HR_Data[Snapshot_Month], HR_Data[Year Month], HR_Data[Year Quarter], HR_Data[Year Quarter No] ),
        TREATAS ( _pyMonths, HR_Data[Snapshot_Month] )
    )
```

### 2. Pay & Performance\KPI Labels

#### Avg Monthly Salary PY Label

KPI card caption: previous-year value for Avg Monthly Salary.

```dax
Avg Monthly Salary PY Label =
VAR _py = [Avg Monthly Salary PY]
RETURN
    "Previous Year: " & IF ( ISBLANK ( _py ), "n/a", FORMAT ( _py, """MYR"" #,##0" ) )
```

#### Avg Monthly Salary Change Label

KPI card delta vs previous year for Avg Monthly Salary.

```dax
Avg Monthly Salary Change Label =
VAR _cur = [Avg Monthly Salary]
VAR _py = [Avg Monthly Salary PY]
VAR _chg = DIVIDE ( _cur - _py, _py )
RETURN
    IF ( ISBLANK ( _py ) || ISBLANK ( _cur ), BLANK (), IF ( _chg > 0, "▲ ", IF ( _chg < 0, "▼ ", "■ " ) ) & FORMAT ( ABS ( _chg ), "0.0%" ) )
```

#### Avg Monthly Salary Change Color

Green when the change is favourable, red when not.

```dax
Avg Monthly Salary Change Color =
VAR _cur = [Avg Monthly Salary]
VAR _py = [Avg Monthly Salary PY]
RETURN
    IF ( ISBLANK ( _py ) || ISBLANK ( _cur ), "#8C8C8C", IF ( _cur >= _py, "#008E60", "#D8211D" ) )
```

#### Avg Performance Rating PY Label

KPI card caption: previous-year value for Avg Performance Rating.

```dax
Avg Performance Rating PY Label =
VAR _py = [Avg Performance Rating PY]
RETURN
    "Previous Year: " & IF ( ISBLANK ( _py ), "n/a", FORMAT ( _py, "0.00" ) )
```

#### Avg Performance Rating Change Label

KPI card delta vs previous year for Avg Performance Rating.

```dax
Avg Performance Rating Change Label =
VAR _cur = [Avg Performance Rating]
VAR _py = [Avg Performance Rating PY]
VAR _chg = DIVIDE ( _cur - _py, _py )
RETURN
    IF ( ISBLANK ( _py ) || ISBLANK ( _cur ), BLANK (), IF ( _chg > 0, "▲ ", IF ( _chg < 0, "▼ ", "■ " ) ) & FORMAT ( ABS ( _chg ), "0.0%" ) )
```

#### Avg Performance Rating Change Color

Green when the change is favourable, red when not.

```dax
Avg Performance Rating Change Color =
VAR _cur = [Avg Performance Rating]
VAR _py = [Avg Performance Rating PY]
RETURN
    IF ( ISBLANK ( _py ) || ISBLANK ( _cur ), "#8C8C8C", IF ( _cur >= _py, "#008E60", "#D8211D" ) )
```

#### Avg Training Hours PY Label

KPI card caption: previous-year value for Avg Training Hours.

```dax
Avg Training Hours PY Label =
VAR _py = [Avg Training Hours PY]
RETURN
    "Per employee per month · " & "Previous Year: " & IF ( ISBLANK ( _py ), "n/a", FORMAT ( _py, "0.00" ) )
```

#### Avg Training Hours Change Label

KPI card delta vs previous year for Avg Training Hours.

```dax
Avg Training Hours Change Label =
VAR _cur = [Avg Training Hours]
VAR _py = [Avg Training Hours PY]
VAR _chg = DIVIDE ( _cur - _py, _py )
RETURN
    IF ( ISBLANK ( _py ) || ISBLANK ( _cur ), BLANK (), IF ( _chg > 0, "▲ ", IF ( _chg < 0, "▼ ", "■ " ) ) & FORMAT ( ABS ( _chg ), "0.0%" ) )
```

#### Avg Training Hours Change Color

Green when the change is favourable, red when not.

```dax
Avg Training Hours Change Color =
VAR _cur = [Avg Training Hours]
VAR _py = [Avg Training Hours PY]
RETURN
    IF ( ISBLANK ( _py ) || ISBLANK ( _cur ), "#8C8C8C", IF ( _cur >= _py, "#008E60", "#D8211D" ) )
```

#### Avg Overtime Hours PY Label

KPI card caption: previous-year value for Avg Overtime Hours.

```dax
Avg Overtime Hours PY Label =
VAR _py = [Avg Overtime Hours PY]
RETURN
    "Per employee per month · " & "Previous Year: " & IF ( ISBLANK ( _py ), "n/a", FORMAT ( _py, "0.00" ) )
```

#### Avg Overtime Hours Change Label

KPI card delta vs previous year for Avg Overtime Hours.

```dax
Avg Overtime Hours Change Label =
VAR _cur = [Avg Overtime Hours]
VAR _py = [Avg Overtime Hours PY]
VAR _chg = DIVIDE ( _cur - _py, _py )
RETURN
    IF ( ISBLANK ( _py ) || ISBLANK ( _cur ), BLANK (), IF ( _chg > 0, "▲ ", IF ( _chg < 0, "▼ ", "■ " ) ) & FORMAT ( ABS ( _chg ), "0.0%" ) )
```

#### Avg Overtime Hours Change Color

Green when the change is favourable, red when not (lower is better).

```dax
Avg Overtime Hours Change Color =
VAR _cur = [Avg Overtime Hours]
VAR _py = [Avg Overtime Hours PY]
RETURN
    IF ( ISBLANK ( _py ) || ISBLANK ( _cur ), "#8C8C8C", IF ( _cur <= _py, "#008E60", "#D8211D" ) )
```

### 1. Workforce\Formatting

#### Attrition Bar Color

Red above company average, green otherwise.

```dax
Attrition Bar Color =
IF ( [Attrition Rate] > [Attrition Rate Company Avg], "#D8211D", "#008E60" )
```

#### Exit Type Summary

Subtitle for the exit reasons chart.

```dax
Exit Type Summary =
VAR _vol = CALCULATE ( [Exits], HR_Data[Exit_Type] = "Voluntary" )
VAR _inv = CALCULATE ( [Exits], HR_Data[Exit_Type] = "Involuntary" )
VAR _tot = _vol + _inv
RETURN
    FORMAT ( _tot, "#,0" ) & " exits · Voluntary " & FORMAT ( _vol, "#,0" ) & " (" & FORMAT ( DIVIDE ( _vol, _tot ), "0%" ) & ") · Involuntary "
        & FORMAT ( _inv, "#,0" ) & " (" & FORMAT ( DIVIDE ( _inv, _tot ), "0%" ) & ")"
```

#### Gender Subtitle

Subtitle for the gender split chart.

```dax
Gender Subtitle =
"Active employees as of " & FORMAT ( DATE ( 1899, 12, 30 ) + MAX ( HR_Data[Snapshot_Month] ), "mmm yyyy" )
```

### 2. Pay & Performance\Formatting

#### Rating Subtitle

Subtitle for the rating distribution chart.

```dax
Rating Subtitle =
"% of active employees as of " & FORMAT ( DATE ( 1899, 12, 30 ) + MAX ( HR_Data[Snapshot_Month] ), "mmm yyyy" )
```

#### Rating Bar Color

Red for ratings 1-2, grey for 3, green for 4-5.

```dax
Rating Bar Color =
VAR _rating = SELECTEDVALUE ( HR_Data[Performance_Rating] )
RETURN
    SWITCH ( TRUE (), _rating <= 2, "#D8211D", _rating = 3, "#BFBFBF", "#008E60" )
```
