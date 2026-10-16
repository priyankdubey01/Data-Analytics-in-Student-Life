# 🎓 Data Analytics in Student Life

## Project Overview

**Data Analytics in Student Life** is a beginner-friendly Python data analytics and machine learning project that investigates which student characteristics and academic indicators are associated with final Mathematics grades.

The project uses the **Student Performance** dataset and follows a practical data science workflow: load data, inspect and clean it, explore patterns through statistics and visualizations, examine correlations, and train linear regression models to estimate final grades.

> **Important:** This is an educational analysis. Correlations do not prove causation, and model predictions should be used to support students—not to label or penalize them.

## Objectives

- Explore student academic performance using real-world tabular data.
- Practice data inspection and basic data-quality checks.
- Visualize the relationship between grades and study time, previous failures, absences, internet access, educational aspirations, social activity, and family education.
- Understand correlation and the difference between association and causation.
- Compare simple linear regression models using different sets of features.
- Demonstrate how early academic results can support an educational early-warning process.

## Dataset

The notebook uses the **Student Performance – Mathematics (`student-mat.csv`)** dataset, described in the notebook as containing records for **395 students**. The dataset includes demographic, family, social, study-habit, attendance, and grade information.

The notebook first attempts to load the CSV from an online URL. If that fails, it tries to load `student-mat.csv` from the current working directory.

### Important columns

| Column | Description |
|---|---|
| `age` | Student age |
| `sex` | Student sex |
| `studytime` | Weekly study-time category (1 = under 2 hours; 2 = 2–5 hours; 3 = 5–10 hours; 4 = over 10 hours) |
| `failures` | Number of past class failures |
| `absences` | Number of recorded absences |
| `Medu`, `Fedu` | Mother's and father's education levels |
| `goout` | Frequency of going out with friends |
| `Walc` | Weekend alcohol-consumption category |
| `higher` | Whether the student wants to pursue higher education |
| `internet` | Whether the student has internet access at home |
| `G1` | First-period grade |
| `G2` | Second-period grade |
| `G3` | Final grade, on a 0–20 scale |

The notebook creates additional fields such as `result` (Pass when `G3 >= 10`, otherwise Fail), `study_band` (readable study-time labels), and numeric versions of selected yes/no variables for machine learning.

## Technologies and Libraries

- **Python** — programming language
- **Pandas** — data loading, tabular manipulation, grouping, and summaries
- **NumPy** — numerical operations and derived columns
- **Matplotlib** — chart creation
- **Seaborn** — statistical visualizations
- **scikit-learn** — train/test splitting, linear regression, and model evaluation
- **Jupyter Notebook** — interactive environment for running the analysis

## Project Workflow

### 1. Import libraries
Loads the Python libraries required for analysis, visualization, and predictive modelling.

### 2. Load the dataset
Reads the semicolon-separated CSV file (`sep=";"`) from the configured online source or local file.

### 3. Inspect the data
Displays sample rows, column information, and descriptive statistics for important numeric fields.

### 4. Check and prepare the data
Checks missing values and duplicate rows, then creates helpful derived columns for analysis and modelling.

### 5. Exploratory Data Analysis (EDA)
The notebook explores several questions using summary statistics and charts:

1. **Final-grade distribution:** examines the spread of `G3`, the pass threshold of 10, and students with a final grade of zero.
2. **Study time:** compares average final grades across weekly study-time categories.
3. **Previous failures:** compares grades by the number of past class failures.
4. **Absences:** compares the relationship between absences and final grades, including a separate analysis excluding records with `G3 == 0`.
5. **Education aspirations and access:** examines higher-education aspirations, home internet access, and relationship status.
6. **Social and family context:** explores going-out frequency and mother's education level.
7. **Correlation heatmap:** visualizes relationships among selected numeric variables, including `G1`, `G2`, and `G3`.

### 6. Predictive analytics
Uses **Linear Regression** to predict the final grade (`G3`). It compares three feature scenarios:

- **Scenario A — Habits and background:** uses study time, failures, absences, parents' education, social activity, higher-education aspiration, internet access, age, and weekend alcohol category.
- **Scenario B — Scenario A + `G1`:** adds the first-period grade.
- **Scenario C — Scenario A + `G1` and `G2`:** adds both earlier-period grades.

The data is split into training and test sets using an 80/20 split and `random_state=42`. Models are evaluated using **R²** and **Mean Absolute Error (MAE)**. The notebook also demonstrates a prediction for an example student using Scenario B.

### 7. Summarize findings
Concludes with practical takeaways for students, teachers, mentors, and institutions, with an emphasis on early academic support.

## Key Insights Discussed in the Notebook

The notebook's interpretation highlights the following patterns in this dataset:

- Previous class failures are associated with lower final grades.
- Higher weekly study-time categories show a modest positive association with grades.
- After records with a final grade of zero are examined separately, more absences are associated with lower grades in the remaining records.
- Higher-education aspirations and home internet access are associated with higher average grades in this sample.
- Very frequent social outings are associated with lower average grades than some moderate levels of going out.
- Earlier-period grades (`G1` and especially `G2`) are strongly associated with the final grade and improve regression predictions.

These are **dataset-specific associations**, not universal rules. Group sizes and other unmeasured factors matter, and the results should not be interpreted as proof that any single habit causes a grade outcome.

## Repository Structure

Keep the notebook and dataset together in the same directory:

```text
student-life-data-analytics/
├── student_life_data_analytics(1).ipynb
├── student-mat.csv
└── README.md
```

If you rename the notebook, update the filename shown above accordingly.

## Installation

### 1. Install Python
Use Python 3.9 or later where possible.

### 2. Install dependencies

```bash
python -m pip install numpy pandas matplotlib seaborn scikit-learn jupyter
```

### 3. Download or place the dataset
Ensure `student-mat.csv` is in the same directory as the notebook if you want to use the local fallback or run without internet access.

**CSV format note:** The file is semicolon-separated. The notebook already reads it with `sep=";"`; do not change this to a comma unless the dataset format changes.

## Run the Project

From a terminal, move into the project directory and start Jupyter:

```bash
jupyter notebook
```

Open `student_life_data_analytics(1).ipynb`, then run the notebook cells from top to bottom.

You can also use JupyterLab:

```bash
jupyter lab
```

The notebook attempts an online dataset download first. For offline use, keep `student-mat.csv` in the notebook's working directory.

## Model Evaluation

The notebook compares regression models using:

- **R² score:** indicates how much of the variation in test-set grades is explained by the model. Higher is generally better.
- **Mean Absolute Error (MAE):** average absolute difference between predicted and actual grades, measured in grade points.

The notebook's split is reproducible through `random_state=42`, but results may vary if the dataset, features, or split changes. The example prediction is illustrative and is not a guaranteed outcome for a real student.

## Limitations and Responsible Use

- The dataset represents a specific school context and should not automatically be generalized to other schools, regions, or student populations.
- Correlation does not establish causation.
- A final grade of zero may represent an unusual record; the notebook investigates its effect on the absence analysis but does not establish the reason for every such record.
- Predictions are estimates and can be wrong, especially when only background and habit variables are available.
- Student data is sensitive. Follow institutional privacy rules, minimize identifiable data, and avoid publishing personal student records.
- Use analytics to offer tutoring, mentoring, and resources—not to stigmatize, punish, or make high-stakes decisions automatically.

## Possible Future Improvements

- Add cross-validation and compare Linear Regression with regularized models such as Ridge and Lasso.
- Compare regression metrics across multiple train/test splits.
- Add residual plots and error analysis.
- Investigate the zero-grade records with documented context before deciding how to handle them.
- Add a clear model pipeline for encoding categorical variables and validating inputs.
- Evaluate performance on an independent dataset before real-world use.
- Build a privacy-conscious dashboard for aggregate trends and supportive early-warning indicators.

## References and Attribution

The notebook identifies the dataset as the **Student Performance** dataset associated with Cortez and Silva (2008) and the UCI Machine Learning Repository. Please retain the dataset's original attribution and review the dataset's official terms and documentation before redistribution or reuse.

- UCI Machine Learning Repository: https://archive.ics.uci.edu/dataset/320/student+performance
- Dataset URL used by the notebook: https://raw.githubusercontent.com/Rohith04MVK/Student-Score-ML/main/student-mat.csv

## Author

Add your name, institution, contact details, and repository link here if you want to publish this project on GitHub.

---

⭐ If you find this educational project useful, consider starring the repository and sharing suggestions for improvement.
