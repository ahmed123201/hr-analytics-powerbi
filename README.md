# HR Analytics Dashboard (Power BI)

A 4-page Power BI report analyzing workforce composition, demographics,
performance trends, and attrition drivers, built on a star-schema data model.

## Data model

**Star schema**, 5 tables:

| Table | Type | Role | Key fields |
|---|---|---|---|
| `DimEmployee` | Dimension | Core employee attributes | Department, JobRole, Gender, Ethnicity, MaritalStatus, BusinessTravel, OverTime, YearsAtCompany, HireDate, Attrition, AgeBins |
| `DimDate` | Dimension | Date/time hierarchy | Year, Quarter, Month, Day |
| `DimRatingLevel` | Dimension | Rating scale lookup | RatingID, RatingLevel |
| `DimSatisfiedLevel` | Dimension | Satisfaction scale lookup | SatisfactionID, SatisfactionLevel |
| `_Measures` | Measures table | Holds all DAX measures | 15 measures — kept separate from data tables for a clean, easy-to-navigate model |

## Measures (DAX)

- `TotalEmployees`, `TotalEmployeesDate`, `ActiveEmployees`, `InactiveEmployees`
- `% Attrition Rate`, `% Attrition Rate Date`
- `AverageSalary`
- `JobSatisfaction`, `EnvironmentSatisfaction`, `RelationshipSatisfaction`,
  `ManagerRating`, `SelfRating`, `WorkLifeBalance`
- `LastReviewDate`, `NextReviewDate`

## Pages

### 1. Overview
KPI cards, employee hiring trends over time (by year/quarter/month/day,
split by attrition status), active headcount by department, and a treemap
of department × job role.

### 2. Demographics
Youngest/oldest employee, age distribution, age × gender split (100%
stacked column), marital status breakdown, and ethnicity vs. average
salary — the latter specifically surfaces potential pay-disparity patterns
across groups.

### 3. Performance Tracker
The most detailed page: start date / last review / next review cards,
plus six parallel line charts tracking satisfaction and rating trends —
job satisfaction, relationship satisfaction, self-rating, work-life
balance, manager rating, and environment satisfaction — alongside two
detail tables. Includes a slicer for filtering by employee/department.

### 4. Attrition
Attrition by hire-date cohort, by business travel frequency, by overtime
requirement, and by tenure — testing the classic HR churn drivers
(travel burden, overtime load, tenure stage) against actual attrition
rates.

## Design notes

- Consistent one-page-one-theme structure: each page answers a single
  question rather than mixing topics.
- Measures isolated in a dedicated `_Measures` table rather than scattered
  across dimension tables — keeps the model clean and measures easy to
  find/reuse.
- Rating and satisfaction scales modeled as separate lookup dimensions
  (`DimRatingLevel`, `DimSatisfiedLevel`) rather than hardcoded values —
  supports consistent formatting and potential drill-through.
