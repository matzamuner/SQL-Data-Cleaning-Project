# World Layoffs Data Cleaning (SQL)

A comprehensive SQL data cleaning project on the [World Layoffs Dataset](https://www.kaggle.com/datasets/swaptr/layoffs-2022). This repository contains scripts that process raw layoff data through a structured data-cleaning pipeline using MySQL.

---

## Project Overview

Raw data often contains duplicate records, inconsistent formatting, missing values, and unhelpful entries. This project demonstrates how to transform uncleaned dataset entries into a structured, normalized SQL database ready for Exploratory Data Analysis (EDA).

---

## Data Cleaning Steps

The data cleaning process follows a four-step pipeline:

### 1. Staging & Removing Duplicates

* Created a staging table (`layoffs_staging`) to preserve the raw dataset.


* Utilized `ROW_NUMBER()` window functions partitioned across all key attributes to detect exact duplicate rows.


* Created `layoffs_staging2` with an added `row_num` column and deleted all entries where `row_num >= 2`.



### 2. Standardizing Data

* **Strings:** Trimmed trailing periods (e.g., standardizing `'United States.'` to `'United States'`).


* **Categories:** Consolidated variations in industry labels (e.g., updating `'Crypto Currency'` and `'CryptoCurrency'` to `'Crypto'`).


* **Dates:** Converted string dates to `DATE` type using `STR_TO_DATE()` and updated column schemas with `ALTER TABLE`.



### 3. Handling Null & Blank Values

* Converted empty string values (`''`) to `NULL` for consistency.


* Populated missing `industry` fields using self-joins (`JOIN`) on matching company names where valid industry data existed.



### 4. Removing Unnecessary Data

* Removed rows where both `total_laid_off` and `percentage_laid_off` were `NULL`.


* Dropped temporary helper columns (e.g., `row_num`) to finalize the clean dataset schema.



---

## Repository Structure

```text
├── layoffs.csv           # Raw dataset (source data)
├── data_cleaning.sql     # Main SQL script containing all cleaning queries
└── README.md             # Project documentation

```

---

##Requirements & Usage

1. **Database:** MySQL Server / MySQL Workbench
2. **Setup:**
* Import `layoffs.csv` into a database named `world_layoffs`.


* Run the queries in `data_cleaning.sql` sequentially to build and clean `layoffs_staging2`.
