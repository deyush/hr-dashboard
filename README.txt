# HR Analytics Dashboard: Attrition, Compensation & Workforce Trends

## 📊 Project Overview

- **Objective:** Build an end-to-end HR analytics solution to explore employee trends, attrition patterns, compensation changes, recruitment funnel performance, headcount, and leave behavior.
- **Scope:** Synthetic HR data across multiple domains (Compensation, Employee Master, Headcount, Leave, Recruitment) from 2018–2025 with monthly and transactional granularity. No real employee data is used.
- **Approach:** Python (Jupyter + `pandas`, `numpy`, `matplotlib`) for cleaning and feature engineering. Power BI for dashboarding and reporting.

---

## 📁 Dataset Information

> ⚠️ **Note:** All datasets used in this project are synthetically generated for educational and demonstration purposes. They do not contain real employee or company data.

### 1. `Compensation_History.csv`

Tracks salary changes over time for each employee.

- **Columns:**  
  `ChangeID`, `EmployeeID`, `ChangeDate`, `OldSalary`, `NewSalary`, `Reason`

### 2. `Employee_Master.csv`

Core employee profile and status information.

- **Columns:**  
  `EmployeeID`, `FullName`, `Department`, `JobTitle`, `Email`, `Gender`, `HireDate`, `TerminationDate`, `Salary`, `ManagerID`, `PerformanceRating`, `Status`

### 3. `Headcount.csv`

Monthly department-level workforce metrics.

- **Columns:**  
  `RecordID`, `MonthEnd`, `Department`, `Headcount`, `Hires`, `Terminations`, `AttritionRate`

### 4. `Leave_Attendance.csv`

Tracks employee leave records and durations.

- **Columns:**  
  `LeaveID`, `EmployeeID`, `LeaveType`, `StartDate`, `EndDate`, `Days`

### 5. `Recruitment_Funnel.csv`

Monitors candidate progress through the hiring pipeline.

- **Columns:**  
  `CandidateID`, `PositionID`, `JobTitle`, `ApplicationDate`, `Source`, `Stage`, `DateatStage`

---

## 🎯 Project Goals

- Clean and preprocess all raw datasets.
- Perform exploratory data analysis to identify trends and anomalies.
- Build an interactive dashboard to surface actionable insights.
- Produce recommendations and an executive-ready report.

---

## 🛠️ Tools and Technologies

| Component         | Tool/Library Used                          |
|------------------|--------------------------------------------|
| **Python Libraries** | `pandas`, `numpy`, `matplotlib` |
| **BI Tool**          | Power BI                                   |
| **Notebooks**        | Jupyter Notebook                           |
| **Version Control**  | GitHub                                     |

---


## 📂 Folder Structure

``` 
HR_Dashboard / 
│ 
├── README.md 
├── data/ 
│ ├── raw/ 
│ └── processed/ 
├── notebooks/ 
│ ├── 01a_data_cleaning_compensation.ipynb 
│ ├── 01b_data_cleaning_employee.ipynb 
│ ├── 01c_data_cleaning_headcount.ipynb 
│ ├── 01d_data_cleaning_leave.ipynb 
│ └── 01e_data_cleaning_recruitment.ipynb 
├── powerbi/ 
│ ├── HR_Dashboard.pbix 
│ └── screenshots/ 
├── reports/ 
│ └── HR_Insights.pdf 
└── assets/

```
---

## 🔄 Project Steps

1. Open the notebooks in `notebooks/` (01a → 01e) and run all cells.
2. Each notebook loads its raw CSV from `data/raw/`, cleans and engineers features, then saves to `data/processed/`.
3. Import the processed CSVs into Power BI to build visuals and KPIs.
4. Document insights and decisions in `reports/`.

---

## 🧹 Data Cleaning and Preprocessing

- **Consistent schema:** Columns standardized to `snake_case` across datasets.
- **Critical nulls handled:** Dropped rows missing keys (e.g., `employeeid`, required dates). Valid blanks retained (e.g., `terminationdate` for active employees, missing `performancerating` for new hires).
- **Deduplication:** Row-level duplicates removed; ID-level duplicates resolved (keeping latest record where applicable).
- **Date parsing:** All date fields converted to datetime; invalid strings coerced and dropped when critical.
- **Category standardization:** Whitespace trimmed and values title-cased (e.g., `Status`, `Department`, `Reason`, `LeaveType`, `Source`, `Stage`).
- **ID generation:** Missing IDs created where sensible (e.g., `changeid`, `leaveid`).
- **Validations:** Salary and numeric fields checked for negative/zero outliers; removed or corrected.

### Feature Engineering Highlights
- Compensation: salary deltas, percentage change, direction and magnitude, time since last change, growth since first salary, promotion/merit flags and counts.
- Employee Master: tenure days/years/bands, salary bands, dept/job averages and variance, performance categories, department size, manager span, seniority level, attrition indicators.
- Headcount: net change, growth/turnover/hire rates, rolling 3-month averages, MoM changes, headcount category, attrition risk.
- Leave: duration categories, type flags, employee-level totals and averages, seasonality, weekend flags, days since last leave.
- Recruitment: stage hierarchy and flags, source flags, days in process, conversion rates, source effectiveness, candidate journey and outcome.

---

## 📊 Dashboard Development

### Key Measures

**Headcount (9 measures)**
- Headcount As Of Last Date, Total Headcount, Headcount (Company Snapshot)
- Hires, Terminations, Turnover Rate %
- Average Attrition Rate %, Monthly Termination Rate %

**Compensation (4 measures)**
- Avg Salary Change %, Promotion Count, Merit Count, Promotion Rate

**Employee/Attrition (7 measures)**
- Active Employees, Early Attrition Count
- Average Tenure (Years), Average Tenure PrevMonth, Average Tenure MoM Change
- Average Performance, High Performers %

**Leave (2 measures)**
- Total Leave Days, Avg Leave Duration

**Recruitment (6 measures)**
- Applications, Hires (Req), Hire Rate %, Avg Days in Process
- Open Positions (Filtered), Open Positions Still Hiring, Best Source

### Suggested Visuals

- KPI panel for high-level metrics
- Line chart for attrition trend over time
- Stacked bar chart for attrition by department and gender
- Treemap for job roles
- Donut chart for leave type distribution
- Funnel chart for recruitment stages
- **Slicers:** department, tenure bucket, gender, attrition status, leave type, funnel stage

### Interactivity

- Drill-through to individual employee profiles and salary history
- Mobile-friendly layout with simplified KPI view

---

## 🔍 Insights and Recommendations

### Key Findings

- Compensation changes show a consistent, moderate typical increase per cycle, with both Merit and Promotion events contributing almost equally.
- Many employees follow an annual compensation review cadence (time-between-change features indicate ~12-month intervals for a large subset).
- Tenure features highlight early attrition risk within the first year for a portion of terminated employees.
- Salary positioning vs department/job averages surfaces pockets of below-average pay that may warrant review.
- Department headcount trends (rolling averages and MoM changes) reveal periods of growth and contraction at the team level.
- Leave patterns vary by season and weekday; weekend-adjacent leave (Fridays/Mondays) is common for short vacations.
- Recruitment funnel shows the highest candidate volumes from LinkedIn and Employee Referral; conversion rates vary across stages and sources.

### Business Implications

- Align compensation planning with annual cycles; define clear criteria for Merit vs Promotion adjustments.
- Target early-tenure retention with enhanced onboarding, mentorship, and 90-day check-ins.
- Conduct focused salary fairness reviews for roles/departments below peer averages to reduce pay-related attrition risk.
- Use headcount rolling averages and MoM changes to drive quarterly workforce planning and hiring pacing.
- Balance leave capacity by anticipating seasonal peaks and managing weekend-adjacent leave policies.
- Reallocate recruitment budget toward high-quality sources (e.g., referrals) and address stage drop-offs to improve time-to-hire.

### Next Steps

- Launch satisfaction surveys and targeted retention campaigns
- A/B test flexible work policies in high-risk departments
- Collect exit interview data for deeper qualitative insights
- Expand funnel tracking to include offer acceptance and onboarding

---

## ⚙️ Technical Notes

- **Challenges and Fixes:**  
  Handled mixed data types in satisfaction columns; standardized categorical labels; merged datasets using `EmployeeID`
- **Performance Tips:**  
  Pre-aggregated attrition metrics for faster dashboard load; used incremental refresh in Power BI
- **Version Control and Artifacts:**  
  GitHub repo with clear notebook naming, cleaned outputs, and dashboard artifacts

---

## 📦 Final Assets and Delivery

- **Deliverables:**
  - `powerbi/HR_Dashboard.pbix`
  - Cleaned datasets in `data/processed/`:
    - `Compensation_History_cleaned.csv`
    - `Employee_Master_cleaned.csv`
    - `Headcount_cleaned.csv`
    - `Leave_Attendance_cleaned.csv`
    - `Recruitment_Funnel_cleaned.csv`
  - Jupyter notebooks (cleaning + feature engineering):
    - `01a_data_cleaning_compensation.ipynb`
    - `01b_data_cleaning_employee.ipynb`
    - `01c_data_cleaning_headcount.ipynb`
    - `01d_data_cleaning_leave.ipynb`
    - `01e_data_cleaning_recruitment.ipynb`
  - Executive report: `reports/HR_Insights.pdf`
- **How to Run:**
  - Open the notebooks in order (01a → 01e) to reproduce the processed datasets.
  - Import the CSVs from `data/processed/` into Power BI for dashboard refresh.
- **Contact:**  
  **Andreia**, Data Analyst  
  Reach via GitHub or project README
