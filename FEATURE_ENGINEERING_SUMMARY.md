# HR Dashboard - Feature Engineering Summary

## Overview
Both data cleaning notebooks (`01a_data_cleaning_compensation.ipynb` and `01b_data_cleaning_employee.ipynb`) now include comprehensive feature engineering as part of **Step 6: Check for Some More Transformations**.

---

## 📊 Compensation_History Features (01a_data_cleaning_compensation.ipynb)

### Original Columns (6)
- changeid, employeeid, changedate, oldsalary, newsalary, reason

### New Features Created (19+)

#### 1. **Date Features**
- `change_year` - Year of compensation change
- `change_month` - Month of compensation change
- `change_quarter` - Quarter of compensation change

#### 2. **Salary Calculations**
- `salary_change` - Absolute salary change amount
- `salary_change_pct` - Percentage salary change

#### 3. **Salary Direction**
- `salary_direction` - Categorical: Increase, Decrease, No Change, Unknown

#### 4. **Change Magnitude**
- `change_magnitude` - Categorical: Small (≤5%), Medium (5-10%), Large (10-15%), Very Large (>15%)

#### 5. **Time-Based Features**
- `prev_change_date` - Previous compensation change date
- `days_since_last_change` - Days between compensation changes
- `months_since_last_change` - Months between compensation changes

#### 6. **Employee-Level Features**
- `change_number` - Sequence number of changes per employee
- `total_changes` - Total compensation changes per employee

#### 7. **Cumulative Growth Features**
- `first_salary` - Employee's first recorded salary
- `current_salary` - Employee's most recent salary
- `total_salary_growth` - Total salary growth amount
- `total_growth_pct` - Total salary growth percentage

#### 8. **Reason-Based Features**
- `is_promotion` - Binary flag (1 if promotion, 0 otherwise)
- `is_merit` - Binary flag (1 if merit increase, 0 otherwise)
- `total_promotions` - Cumulative promotions per employee
- `total_merit_increases` - Cumulative merit increases per employee

#### 9. **Outlier Detection**
- IQR method applied to identify salary outliers

---

## 👥 Employee_Master Features (01b_data_cleaning_employee.ipynb)

### Original Columns (12)
- employeeid, fullname, department, jobtitle, email, gender, hiredate, terminationdate, salary, managerid, performancerating, status

### New Features Created (23+)

#### 1. **Date Features**
- `hire_year`, `hire_month`, `hire_quarter` - Hire date components
- `termination_year`, `termination_month`, `termination_quarter` - Termination date components

#### 2. **Tenure Features**
- `tenure_days` - Days of service
- `tenure_years` - Years of service
- `tenure_band` - Categorical: 0-1 years, 1-3 years, 3-5 years, 5-10 years, 10+ years

#### 3. **Salary Features**
- `salary_band` - Categorical: <60K, 60K-80K, 80K-100K, 100K-150K, 150K+
- `dept_avg_salary` - Average salary in employee's department
- `job_avg_salary` - Average salary for employee's job title
- `salary_vs_dept_avg` - Percentage difference from department average
- `salary_vs_job_avg` - Percentage difference from job average

#### 4. **Performance Features**
- `performance_category` - Categorical: Below Average, Average, Good, Excellent

#### 5. **Department Metrics**
- `department_size` - Number of employees in department

#### 6. **Manager Metrics**
- `manager_span_of_control` - Number of direct reports per manager

#### 7. **Binary Flags**
- `is_active` - 1 if active, 0 otherwise
- `is_terminated` - 1 if terminated, 0 otherwise
- `has_manager` - 1 if has manager, 0 otherwise
- `has_performance_rating` - 1 if rated, 0 otherwise

#### 8. **Seniority Features**
- `seniority_level` - Categorical: Junior, Mid-Level, Senior, Executive (based on tenure)

#### 9. **Attrition Features**
- `tenure_at_termination` - Years of service at termination
- `early_attrition` - Binary flag (1 if left within first year)

#### 10. **Data Validation**
- Automated fixes for status/termination date inconsistencies

---

## 📈 Headcount Features (01c_data_cleaning_headcount.ipynb)

### Original Columns (7)
- recordid, monthend, department, headcount, hires, terminations, attritionrate

### New Features Created (23+)

#### 1. Date Features
- `year`, `month`, `quarter`, `month_name`

#### 2. Calculated Metrics
- `net_change` = hires - terminations
- `growth_rate`, `turnover_rate`, `hire_rate`

#### 3. Time-Based Features
- 3-month rolling averages: `headcount_3m_avg`, `hires_3m_avg`, `terminations_3m_avg`
- Month-over-month changes: `headcount_mom_change`, `headcount_mom_change_pct`

#### 4. Department-Level Metrics
- `dept_avg_headcount`

#### 5. Categories and Flags
- `headcount_category`, `attrition_risk`
- `has_hires`, `has_terminations`, `is_growing`, `is_shrinking`

---

## 🏖️ Leave_Attendance Features (01d_data_cleaning_leave.ipynb)

### Original Columns (6)
- leaveid, employeeid, leavetype, startdate, enddate, days

### New Features Created (29+)

#### 1. Date Features
- `leave_year`, `leave_month`, `leave_quarter`, `leave_day_of_week`, `leave_month_name`

#### 2. Duration & Validation
- `calculated_days` (used to fill missing `days`)
- `leave_duration_category` (Single Day → Extended 15+)

#### 3. Leave Type Flags
- `is_sick_leave`, `is_vacation`, `is_personal`, `is_maternity_paternity`

#### 4. Employee Aggregations
- `total_leave_days`, `leave_count`, `avg_leave_duration`
- Per-type counts: `sick_leave_count`, `vacation_count`, `personal_leave_count`, `maternity_paternity_count`

#### 5. Time & Seasonality
- `days_since_last_leave`, `leave_sequence`, `season`
- `starts_on_weekend`, `starts_on_monday`, `starts_on_friday`

---

## 🧲 Recruitment_Funnel Features (01e_data_cleaning_recruitment.ipynb)

### Original Columns (7)
- candidateid, positionid, jobtitle, applicationdate, source, stage, dateatstage

### New Features Created (33+)

#### 1. Date Features
- `application_year`, `application_month`, `application_quarter`, `application_month_name`, `application_day_of_week`

#### 2. Stage & Source
- `stage_number` (ordered), stage flags: `is_applied`, `is_screened`, `is_interview1`, `is_interview2`, `is_offer`, `is_hired`, `is_rejected`
- Source flags: `is_linkedin`, `is_indeed`, `is_referral`, `is_company_website`, `is_job_fair`

#### 3. Process Timing
- `days_in_process` (dateatstage - applicationdate)

#### 4. Aggregations & Conversion
- Position metrics: `applications_per_position`, `hires_per_position`, `rejections_per_position`
- Conversion rates per position: `screening_rate`, `interview1_rate`, `hire_rate`
- Source effectiveness: `hire_rate`, `rejection_rate`

#### 5. Candidate Journey & Outcome
- `stage_count`, `furthest_stage`
- `application_season`
- `recruitment_outcome` (Hired, Rejected, Offer Stage, In Progress - Early/Advanced, Unknown)

---

## 🎯 Benefits of Feature Engineering

### For Analysis
- **Time-series analysis**: Track compensation changes over time
- **Employee segmentation**: Group by tenure, salary bands, performance
- **Trend identification**: Identify promotion patterns, salary growth trends
- **Comparative analysis**: Compare employees to department/job averages

### For Power BI Dashboard
- **Ready-to-use categories**: Tenure bands, salary bands, performance categories
- **KPI calculations**: Average salary growth, promotion rates, attrition metrics
- **Filtering dimensions**: Department size, seniority level, change magnitude
- **Relationship building**: Employee-level aggregations for cross-dataset analysis

### For Machine Learning (Future)
- **Predictive features**: Tenure, salary growth, promotion history
- **Attrition prediction**: Early attrition flags, tenure patterns
- **Compensation modeling**: Salary vs peers, growth trajectories

---

## 📁 Output Files

### Cleaned Data with Features
- `data/processed/Compensation_History_cleaned.csv` - 3,302 records, 25+ columns
- `data/processed/Employee_Master_cleaned.csv` - ~1,400+ records, 35+ columns
- `data/processed/Headcount_cleaned.csv` - 846 records, 30+ columns
- `data/processed/Leave_Attendance_cleaned.csv` - 9,200+ records, 35+ columns
- `data/processed/Recruitment_Funnel_cleaned.csv` - 20,500+ records, 40+ columns

### Notebooks
- `notebooks/01a_data_cleaning_compensation.ipynb` - Compensation History cleaning & feature engineering
- `notebooks/01b_data_cleaning_employee.ipynb` - Employee Master cleaning & feature engineering
- `notebooks/01c_data_cleaning_headcount.ipynb` - Headcount cleaning & feature engineering
- `notebooks/01d_data_cleaning_leave.ipynb` - Leave & Attendance cleaning & feature engineering
- `notebooks/01e_data_cleaning_recruitment.ipynb` - Recruitment Funnel cleaning & feature engineering

---

## ✅ Next Steps

1. **Create feature engineering notebook** (optional):
   - `02_feature_engineering.ipynb` for advanced/cross-dataset features
   - Merge Employee + Compensation for holistic salary timelines

2. **Analysis notebook**:
   - `03_analysis_or_modeling.ipynb` for EDA and insights
   - Visualize KPIs using engineered features

3. **Power BI Dashboard**:
   - Import all cleaned CSV files in `data/processed/`
   - Build relationships between datasets
   - Create visuals for headcount trends, leave patterns, funnel conversion, and compensation growth

---

## 📝 Notes

- **Missing values are intentional** in some columns:
  - `oldsalary` / `newsalary`: Valid for new hires or incomplete records
  - `terminationdate`: Valid for active employees
  - `managerid`: Valid for executives
  - `performancerating`: Valid for new/unrated employees

- **Feature engineering is integrated** into the cleaning notebooks (Step 6) rather than in a separate notebook for simplicity and efficiency.

- All features are **analysis-ready** and can be directly used in Power BI or further analysis.
