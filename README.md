# sql


🧹 SQL Data Cleaning Project — Layoffs 2022 Dataset
This project is focused on cleaning and preparing the Layoffs 2022 dataset for analysis. The data was cleaned using SQL, following a methodical, step-by-step process to ensure it's accurate, consistent, and ready for deeper analysis or visualization.

The dataset tracks tech layoffs around the world, including details like company name, location, industry, total laid off, percentage laid off, funding raised, and more.

🗂️ Project Goals
Create a clean and reliable version of the raw layoffs dataset
Handle duplicate records
Standardize inconsistent values
Address missing data logically

Format and transform data types for better usability

🛠️ Tools Used
SQL (MySQL)

MySQL Workbench for queries and exploration

Dataset source: Kaggle - Layoffs 2022

🧹 Step-by-Step Cleaning Process
1. Created a Staging Table
To avoid modifying the original data directly, a staging table (layoffs_staging2) was created as a working copy. This provides a safe space to experiment and clean without risking the raw dataset.

2. Removed Duplicate Records
Duplicates were identified using ROW_NUMBER() combined with PARTITION BY over key fields like company, industry, location, date, etc. This helped pinpoint rows that were exact or near-exact duplicates.

We then added a row_num column and deleted all rows where row_num > 1, effectively keeping only the first unique instance of each duplicate group.

3. Standardized Text Fields
Industry:
Replaced empty strings with NULL to unify missing values.
Filled in missing industries by matching other rows with the same company name that had a known industry.
Standardized inconsistent variations (e.g., "Crypto Currency", "CryptoCurrency") to a single value: "Crypto".

Country:
Identified issues like "United States." (with a period) and standardized them using TRIM() to ensure consistency.

4. Formatted the Date Column
The date column was initially stored as text. Using STR_TO_DATE(), the text was converted into proper DATE format and the column type was updated accordingly. This allows for time-based filtering, sorting, and aggregations during analysis.

5. Handled Null Values Thoughtfully
We kept nulls in fields like total_laid_off, percentage_laid_off, and funds_raised_millions since they might reflect missing real-world data.
However, we removed rows where both total_laid_off and percentage_laid_off were null — these rows didn’t offer any meaningful insight and would skew the analysis.

6. Final Cleanup
After cleaning:
Removed the helper row_num column used for tracking duplicates
Confirmed all transformations were successfully applied
The resulting dataset in layoffs_staging2 is now clean and ready for exploratory analysis

✅ Final Result
We now have a high-quality version of the layoffs dataset, free from:

Duplicates
Formatting inconsistencies
Invalid or placeholder entries
Unusable null records
This cleaned dataset provides a solid foundation for any analytical tasks such as identifying layoff trends, comparing across industries or countries, and time-based reporting.


🧠 Key Takeaways
Data cleaning is just as important as the analysis itself — and often takes more time
Using SQL window functions like ROW_NUMBER() helps efficiently detect duplicates
Standardization of text fields makes grouping and filtering more accurate
Thoughtful null handling ensures data integrity is preserved
