# Student Success Predictors: EDA, PCA & Clustering Analysis

[![Python: 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![Data Processing: Pandas](https://img.shields.io/badge/Data_Processing-Pandas-150458?logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Machine Learning: Scikit--Learn](https://img.shields.io/badge/ML-Scikit--Learn-F7931E?logo=scikitlearn&logoColor=white)](https://scikit-learn.org/)
[![Statistics: SciPy](https://img.shields.io/badge/Statistics-SciPy-8CAAE6?logo=scipy&logoColor=white)](https://scipy.org/)
[![Visualization: Seaborn](https://img.shields.io/badge/Visualization-Seaborn-3776AB?logo=seaborn&logoColor=white)](https://seaborn.pydata.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An end-to-end data science assignment exploring the relationships between student lifestyle habits, wellbeing metrics, background demographics, and academic performance ($N = 1,000$).

This repository includes data cleaning strategies, bivariate association tests, Principal Component Analysis (PCA), K-Means clustering, and statistical validation using ANOVA.

---

## Technical Overview & Methodology

### 1. Data Cleaning & Preprocessing
* **Missing Value Imputation:** Categorical variables (`diet_quality`, `parental_education_level`) with missing entries were assigned an `"Unknown"` category to preserve sample size ($N = 1,000$) and avoid distribution skewing.
* **Deduplication:** Identified and dropped duplicate student records.
* **Feature Scaling & Encoding:** Continuous numerical features were standardized using `StandardScaler` ($\mu = 0, \sigma = 1$), while categorical features were converted using `OneHotEncoder`. The `student_id` identifier was omitted prior to PCA.

### 2. Exploratory & Inferential Data Analysis
* **Univariate Analysis:** Generated histograms, boxplots, and frequency distributions for all lifestyle features (study hours, sleep, screen time, mental health, diet quality, etc.).
* **Bivariate Correlation:** Study hours exhibited the strongest positive linear correlation with exam scores ($r \approx 0.83$). Screen time metrics (Social Media, Netflix) showed negative trends.
* **Chi-Square Test ($\chi^2$) & Cramér’s V:** Applied to categorical feature pairs to evaluate independence. All tested pairs yielded $p > 0.05$ and Cramér’s $V < 0.10$, proving categorical variables were statistically independent.

### 3. Dimensionality Reduction & Clustering
* **Principal Component Analysis (PCA):** Reduced feature space while capturing $>80\%$ of total dataset variance.
  * **PC1 (Academic Engagement):** High positive loadings for `study_hours_per_day` and `exam_score`.
  * **PC2 (Lifestyle Balance):** Driven by `social_media_hours`, `exercise_frequency`, and `attendance_percentage`.
* **K-Means Clustering:** Evaluated cluster counts ($k = 2$ to $9$) using Inertia (Elbow Method) and Silhouette Scores. $k = 2$ was selected based on optimal cluster separation (Silhouette Score):
  * **Cluster 0 (Lower Engagement):** Avg. Study Hours ~1.4 hrs, Avg. Exam Score ~56, lower exercise/mental health ratings.
  * **Cluster 1 (Higher Engagement):** Avg. Study Hours ~5.7 hrs, Avg. Exam Score ~83, higher exercise/mental health ratings.

### 4. Statistical Validation (ANOVA)
One-way ANOVA ($F$-statistic and $p$-value) was conducted to evaluate the effect of various factors on final exam scores:
* **Diet Quality:** $F = 2.73, p = 0.042$ (Modest, statistically significant difference).
* **Parental Education:** $F = 0.65, p = 0.58$ (No significant difference).
* **K-Means Clusters:** $F = 1723.24, p < 0.001$ (Strong, decisive separation validating cluster quality).

---

## Technical Stack & Library Breakdown

| Technology / Library | Domain | Purpose & Role in Project |
| :--- | :--- | :--- |
| **Python 3** | Environment | Core programming language for data execution. |
| **Pandas** | Data Processing | Loading dataset (`.xlsx`), data manipulation, handling missing values, and generating frequency tables. |
| **NumPy** | Numerical Computing | Vectorized mathematical operations and array handling. |
| **Matplotlib** | Data Visualization | Rendering univariate boxplots, histograms, and multivariate PCA biplots. |
| **Seaborn** | Data Visualization | High-level statistical graphics, including correlation heatmaps and boxplot distributions. |
| **Scikit-Learn (`sklearn`)** | Machine Learning | Preprocessing (`StandardScaler`, `OneHotEncoder`, `ColumnTransformer`), dimensionality reduction (`PCA`), unsupervised learning (`KMeans`), and evaluation (`silhouette_score`). |
| **SciPy (`scipy.stats`)** | Inferential Statistics | Performing statistical test functions: `chi2_contingency` (Chi-Square) and `f_oneway` (ANOVA). |
| **Itertools** | Utility | Generating combinations of categorical columns for pairwise contingency tables. |

---

## Academic Context

* **Institution:** Università degli Studi di Napoli Federico II
* **Course:** Statistical Learning and Data Analysis (First Assignment)
* **Author:** Ammar Gharaf
* **Supervisors:** Prof. Roberta Siciliano & Prof. Emiliano Del Gobbo
