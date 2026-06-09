# Southwestern Michigan College — Internship Technical Assessment

Python analysis of institutional enrollment data to evaluate data quality, student success (DFW), enrollment drivers, and a course-level seat planning framework for senior leadership.

---

## Project overview

This repository contains a technical assessment built around SMC enrollment records. The work moves from **raw data inspection** through **cleaning and validation**, **exploratory analysis**, and **actionable planning recommendations** for enrollment management.

**Primary deliverable:** `Python Technical Assessment.ipynb`

**Source data:** `Internship_Test.csv` (~9,603 enrollment records, 26 original columns)

**Cleaned output:** `data_clean` (33 columns, ~9,599 rows after deduplication)

---

## Repository contents

| File | Description |
|---|---|
| `Python Technical Assessment.ipynb` | Main analysis notebook — full assessment workflow |
| `Internship_Test.csv` | Raw enrollment dataset (not tracked in git by default) |
| `Technical_Assessment_Data_Dictionary.docx` | Official data dictionary for the raw export |
| `SMC_Cleaned_Data_Dictionary.docx` | Data dictionary for the cleaned dataset (Word) |
| `SMC_Cleaned_Data_Dictionary.csv` | Same dictionary in CSV format |
| `R Technical Assessment.Rmd` | Optional R version of the assessment template |
| `README.md` | This file |

---

## Requirements

- **Python 3.10+** (tested on 3.12)
- **Jupyter Notebook** or **VS Code / Cursor** with Jupyter support

### Python packages

```bash
pip install pandas numpy matplotlib seaborn jupyter python-docx
```

| Package | Used for |
|---|---|
| `pandas` | Data loading, cleaning, aggregation |
| `numpy` | Numeric calculations and flags |
| `matplotlib` / `seaborn` | Charts and visualizations |
| `python-docx` | Optional — exports data dictionary to Word |

---

## How to run

1. Open the project folder:
   ```bash
   cd "/Users/tonia/Desktop/SMC assessment"
   ```

2. Place `Internship_Test.csv` in this folder (if not already present).

3. Launch Jupyter and open the notebook:
   ```bash
   jupyter notebook "Python Technical Assessment.ipynb"
   ```
   Or open the `.ipynb` file directly in Cursor / VS Code.

4. **Run cells in order from top to bottom.** Later sections depend on earlier ones:
   - Data loading and summary
   - Data quality fixes
   - `clean_enrollment_data()` → creates `data_clean`
   - `df = data_clean.copy()` → used for all analysis sections

5. For **Internship 2 only**, you may skip to **Create a Data Dictionary** (noted in the notebook).

---

## Notebook structure

| Section | What it covers |
|---|---|
| **Dataset summary** | Row/column counts, missing values, descriptive statistics |
| **Data quality issues** | 6 issues identified and fixed (grades, modes, capacity, course names, etc.) |
| **Duplicate checks** | Exact and logical duplicate detection and removal |
| **Cleaning strategy & pipeline** | `clean_enrollment_data()` reusable function |
| **What else?** | Additional variables to collect for richer analysis |
| **Exploratory analysis** | Fill rates, top courses, instructional mode, student populations |
| **DFW analysis** | D/F/W rates by course, gateway flag, mode, and student type |
| **Enrollment drivers** | What factors explain section enrollment |
| **Enrollment planning framework** | 85% target fill rate; Expand / Maintain / Consolidate actions |
| **Scenario analysis** | +10% capacity vs. cutting sections below 50% fill |
| **Executive recommendation** | Summary for senior leadership |
| **Data dictionary** | Documentation for all 33 cleaned fields |
| **Recommendations** | Source-system fixes to prevent future data quality issues |

---

## Key findings (summary)

### Data quality
- 12 duplicate records removed (4 exact + 8 logical)
- 28 missing grades, inconsistent instructional modes, 16 invalid grade codes, and 128 over-capacity sections corrected
- Course names standardized (e.g., `aCCO 203` → `ACCO 203`)

### Enrollment
- ~3,833 sections across ~333 courses and ~2,303 students
- Top demand: **ENGL 103**, **EDUC 120**, **PSYC 101**, **SPEE 102**
- Instructional mode split: ~50% Regular, ~27% Online, ~22% Hybrid
- Main populations: returning students (~69%) and high school guest students

### DFW (student success)
- Overall DFW rate: **~21–22%** (grades D, D+, D-, F, W)
- Highest DFW courses: math, science, nursing (e.g., MATH 102, BIOL 215)
- Instructional mode has **little effect** on DFW; course content and student type matter more

### Planning framework
- **~58 courses** → Expand / Protect (≥85% fill)
- **~242 courses** → Maintain (50–85% fill)
- **~30 courses** → Consolidate (<50% fill)
- Blanket +10% capacity helps overcrowding but wastes seats; cutting all sections below 50% fill would displace ~2,400 students

---

## Cleaning pipeline

The function `clean_enrollment_data(raw_df)` performs:

1. Deduplication (exact + student/term/CRN logical duplicates)
2. Course name standardization
3. `Subject` and `Course_Number` extraction
4. `Fill_Rate` calculation
5. Instructional mode mapping from `SSBSECT_INSM_CODE`
6. Missing grade imputation
7. Quality flags: `over_capacity_flag`, `high_credit_load_flag`, `grade_missing_flag`

**Primary key for enrollment records:** `STUDENT_KEY` + `SFRSTCA_TERM_CODE` + `SFRSTCA_CRN`

---

## Outputs generated by the notebook

When you run the data dictionary cell, these files are created/updated:

- `SMC_Cleaned_Data_Dictionary.csv`
- `SMC_Cleaned_Data_Dictionary.docx`

---

## Notes

- `Internship_Test.csv` is listed in `.gitignore` and is not committed to version control.
- Run the **Enrollment Planning** cell before **Scenario Analysis** — scenario code uses `planning_sections` and `enrollment_plan`.
- Pandas **2.1.x** is supported; avoid `groupby().apply(..., include_groups=False)` (requires pandas 2.2+).

---

## Author

Southwestern Michigan College — Internship Technical Assessment
