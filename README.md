# 🧹 SQL Data Cleaning – Layoffs Dataset
<img width="1653" height="706" alt="Image" src="https://github.com/user-attachments/assets/861ba266-488a-45a8-89f3-9910b6344f86" />
## 📘 Project Description

This project demonstrates a complete data cleaning pipeline using SQL (MySQL) on a real-world layoffs dataset. The dataset included inconsistencies, missing values, formatting issues, and duplicate rows. The goal was to transform it into an analysis-ready state suitable for dashboards, reporting, and deeper analysis.

By **Shoeb Md Ashraf**

---

## 🛠 Tools Used

- SQL (MySQL)
- Excel

---

## 🧾 Overview

The original dataset was messy and required extensive cleaning:
- Duplicate rows with no unique identifier
- Inconsistent industry and country values
- Trailing spaces and characters in text fields
- Improper date format stored as text
- Missing values in important fields

---

## ✅ Key Cleaning Steps

1. **Removed Duplicates**
   - Used `ROW_NUMBER()` with `PARTITION BY` to identify exact duplicate rows.
   - Retained only the first instance (`row_num = 1`) and deleted the rest.

2. **Standardized Text Fields**
   - Applied `TRIM()` to remove extra spaces.
   - Standardized categories (e.g., `Crypto` → `Cryptocurrency`).
   - Cleaned country names (`United States.` → `United States`).

3. **Handled Missing Values**
   - Deleted rows where both `total_laid_off` and `percentage_laid_off` were NULL.
   - Filled missing `industry` values using a `SELF JOIN` based on company name.

4. **Fixed Date Formatting**
   - Converted date strings (MM/DD/YYYY) to proper `DATE` format using `STR_TO_DATE()`.
   - Altered the column type from `TEXT` to `DATE`.

5. **Final Touches**
   - Dropped intermediate columns like `row_num`.
   - Verified structure and integrity of final dataset.

---

## 📈 Outcome

The cleaned dataset is ready for:
- Exploratory Data Analysis (EDA)
- Business dashboards (e.g., Power BI, Tableau)
- Reporting & time-series trend analysis

🔗 You can find the follow-up SQL EDA project using this dataset in my GitHub projects section.

---

## 📬 Contact

- 📧 Email: smashraf110@gmail.com   
- 💼 [LinkedIn – Shoeb Md Ashraf](https://www.linkedin.com/in/shoebmdashraf/)  
- 💻 [GitHub – smashraf110](https://github.com/smashraf110)

---

## 📂 File Structure

```bash
Layoffs-SQL-Cleaning/
├── layoffs_cleaning_script.sql
├── README.md
└── (Optional) sample_screenshots/
