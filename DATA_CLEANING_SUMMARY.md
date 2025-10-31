# HR Dashboard - Complete Data Cleaning & Feature Engineering Summary

## 📁 All Notebooks Created

### ✅ Completed Notebooks (5 Total)

1. **01a_data_cleaning_compensation.ipynb** - Compensation History
2. **01b_data_cleaning_employee.ipynb** - Employee Master
3. **01c_data_cleaning_headcount.ipynb** - Headcount (NEW)
4. **01d_data_cleaning_leave.ipynb** - Leave & Attendance (NEW)
5. **01e_data_cleaning_recruitment.ipynb** - Recruitment Funnel (NEW)

---

## 📊 Dataset 1: Compensation History

**Notebook:** `01a_data_cleaning_compensation.ipynb`

### Original Data
- **Rows:** 4,359
- **Columns:** 6 (ChangeID, EmployeeID, ChangeDate, OldSalary, NewSalary, Reason)

### Cleaned Data
- **Rows:** ~3,302
- **Columns:** 25+

### Key Features Created
- Date features (year, month, quarter)
- Salary calculations (change amount, percentage)
- Salary direction (increase/decrease/no change)
- Change magnitude categories
- Time between changes
- Employee-level aggregations
- Cumulative growth tracking
- Promotion/merit flags and counts

---

## 👥 Dataset 2: Employee Master

**Notebook:** `01b_data_cleaning_employee.ipynb`

### Original Data
- **Rows:** 2,000
- **Columns:** 12 (EmployeeID, FullName, Department, JobTitle, Email, Gender, HireDate, TerminationDate, Salary, ManagerID, PerformanceRating, Status)

### Cleaned Data
- **Rows:** ~1,400+
- **Columns:** 35+

### Key Features Created
- Date features (hire/termination year, month, quarter)
- Tenure calculations (days, years, bands)
- Salary features (bands, department/job averages, vs peers)
- Performance categories
- Department size metrics
- Manager span of control
- Binary flags (is_active, is_terminated, etc.)
- Seniority levels
- Attrition indicators

---

## 📈 Dataset 3: Headcount (NEW)

**Notebook:** `01c_data_cleaning_headcount.ipynb`

### Original Data
- **Rows:** 846
- **Columns:** 7 (RecordID, MonthEnd, Department, Headcount, Hires, Terminations, AttritionRate)
- **No missing values!**

### Cleaned Data
- **Rows:** 846
- **Columns:** 30+

### Key Features Created
- **Date features**: year, month, quarter, month_name
- **Calculated metrics**: 
  - net_change (hires - terminations)
  - growth_rate
  - turnover_rate
  - hire_rate
- **Time-based features**:
  - 3-month rolling averages (headcount, hires, terminations)
  - Month-over-month changes and percentages
- **Department-level**: average headcount
- **Categories**:
  - headcount_category (Small, Medium, Large, Very Large)
  - attrition_risk (Low, Medium, High, Critical)
- **Binary flags**: has_hires, has_terminations, is_growing, is_shrinking

---

## 🏖️ Dataset 4: Leave & Attendance (NEW)

**Notebook:** `01d_data_cleaning_leave.ipynb`

### Original Data
- **Rows:** 10,000
- **Columns:** 6 (LeaveID, EmployeeID, LeaveType, StartDate, EndDate, Days)
- **Issues:** 300 duplicates, ~3-4% missing values, whitespace in LeaveType

### Cleaned Data
- **Rows:** ~9,200+
- **Columns:** 35+

### Key Features Created
- **Date features**: year, month, quarter, day_of_week, month_name
- **Duration categories**: Single Day, Short, Medium, Long, Extended (15+ days)
- **Leave type flags**: is_sick_leave, is_vacation, is_personal, is_maternity_paternity
- **Employee aggregations**:
  - total_leave_days
  - leave_count
  - avg_leave_duration
  - Leave type counts per employee
- **Time-based**: days_since_last_leave, leave_sequence
- **Seasonal**: season classification (Winter, Spring, Summer, Fall)
- **Pattern flags**: starts_on_weekend, starts_on_monday, starts_on_friday
- **Calculated days**: Validated and filled missing values

---

## 🎯 Dataset 5: Recruitment Funnel (NEW)

**Notebook:** `01e_data_cleaning_recruitment.ipynb`

### Original Data
- **Rows:** 24,008
- **Columns:** 7 (CandidateID, PositionID, JobTitle, ApplicationDate, Source, Stage, DateatStage)
- **Issues:** 376 duplicates, ~11% missing values, whitespace in Source/Stage

### Cleaned Data
- **Rows:** ~20,500+
- **Columns:** 40+

### Key Features Created
- **Date features**: application year, month, quarter, day_of_week, month_name
- **Stage hierarchy**: stage_number (1-7 ordering)
- **Stage flags**: is_applied, is_screened, is_interview1, is_interview2, is_offer, is_hired, is_rejected
- **Source flags**: is_linkedin, is_indeed, is_referral, is_company_website, is_job_fair
- **Time-based**: days_in_process (application to current stage)
- **Position metrics**:
  - applications_per_position
  - hires_per_position
  - rejections_per_position
- **Conversion rates**: screening_rate, interview1_rate, hire_rate
- **Source effectiveness**: hire_rate and rejection_rate by source
- **Candidate journey**: stage_count, furthest_stage
- **Seasonal**: application_season
- **Outcome categories**: Hired, Rejected, In Progress (Early/Advanced), Unknown

---

## 📊 Overall Statistics

### Total Features Created Across All Datasets

| Dataset | Original Columns | Final Columns | New Features |
|---------|-----------------|---------------|--------------|
| Compensation History | 6 | 25+ | 19+ |
| Employee Master | 12 | 35+ | 23+ |
| Headcount | 7 | 30+ | 23+ |
| Leave & Attendance | 6 | 35+ | 29+ |
| Recruitment Funnel | 7 | 40+ | 33+ |
| **TOTAL** | **38** | **165+** | **127+** |

---

## 🎯 Common Data Cleaning Steps (All Notebooks)

### Step 1: Delete Redundant Columns
- Verified all columns are relevant

### Step 2: Drop / Rename Columns
- Standardized to snake_case format

### Step 3: Remove Duplicates
- Removed duplicate rows
- Handled duplicate IDs appropriately

### Step 4: Remove NaN Values
- Removed rows with missing critical fields
- Filled missing values where appropriate
- Kept valid blanks (e.g., TerminationDate for active employees)

### Step 5: Clean Individual Columns
- Stripped whitespace
- Standardized categorical values
- Converted dates to datetime
- Validated numeric ranges
- Generated missing IDs

### Step 6: Feature Engineering & Transformations
- Created calculated metrics
- Built time-based features
- Developed categorical features
- Generated binary flags
- Calculated aggregations
- Sorted data appropriately

---

## 📂 Output Files

All cleaned datasets are saved to `data/processed/`:

1. ✅ `Compensation_History_cleaned.csv` (~3,302 records)
2. ✅ `Employee_Master_cleaned.csv` (~1,400+ records)
3. ✅ `Headcount_cleaned.csv` (846 records)
4. ✅ `Leave_Attendance_cleaned.csv` (~9,200+ records)
5. ✅ `Recruitment_Funnel_cleaned.csv` (~20,500+ records)

---

## 🚀 Next Steps

### 1. Data Analysis
- Create `03_analysis_or_modeling.ipynb` for exploratory data analysis
- Generate insights and visualizations
- Identify trends and patterns

### 2. Power BI Dashboard
- Import all cleaned CSV files
- Build relationships between datasets:
  - Employee_Master ↔ Compensation_History (EmployeeID)
  - Employee_Master ↔ Leave_Attendance (EmployeeID)
  - Employee_Master ↔ Headcount (Department)
  - Recruitment_Funnel ↔ Employee_Master (via JobTitle/Department)
- Create visualizations using engineered features

### 3. Advanced Analytics
- Attrition prediction models
- Salary benchmarking analysis
- Recruitment funnel optimization
- Leave pattern analysis
- Department performance metrics

---

## 💡 Key Insights Enabled by Feature Engineering

### Compensation Analysis
- Track salary growth trajectories
- Identify promotion patterns
- Compare salary changes by reason
- Analyze time between raises

### Employee Analytics
- Segment by tenure and seniority
- Compare salaries to department/job averages
- Identify high-performing employees
- Track attrition risks

### Headcount Planning
- Monitor department growth trends
- Identify attrition hotspots
- Forecast hiring needs
- Track month-over-month changes

### Leave Management
- Identify leave patterns by season
- Track frequent leave takers
- Analyze leave types by employee
- Monitor leave duration trends

### Recruitment Optimization
- Measure source effectiveness
- Track conversion rates by stage
- Identify bottlenecks in hiring
- Optimize time-to-hire
- Compare position performance

---

## 🎓 Best Practices Applied

1. **Consistent naming**: All columns in snake_case
2. **Data validation**: Removed invalid values (negative salaries, impossible dates)
3. **Missing value strategy**: Removed critical missing, filled non-critical
4. **Feature engineering**: Created actionable metrics for analysis
5. **Documentation**: Clear markdown sections explaining each step
6. **Reproducibility**: Simple, clean code that can be re-run
7. **Output management**: Saved cleaned data to processed folder

---

## ✅ All Datasets Ready for Analysis!

All five datasets have been:
- ✅ Cleaned
- ✅ Validated
- ✅ Feature-engineered
- ✅ Saved to processed folder
- ✅ Ready for Power BI dashboard
- ✅ Ready for advanced analytics

**Total processing:** 36,000+ raw records → 35,000+ cleaned records with 165+ features
