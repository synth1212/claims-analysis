# Claim Analysis 

## Project Overview

This project analyzes healthcare claims data using Python and Pandas. The goal is to explore claim-level, service-line-level, and diagnosis-level information to uncover insights about providers, payers, utilization patterns, and billing complexity. All analyses are performed in claims_analysis.ipynb

## Data Source Information 

The notebook uses 3 CSV files, each defining a diffrent part of the claims dataset:

[Code](data/STONYBRK_20240531_CODE.csv) - Lists of diagnosis codes for each claim

[Header](data/STONYBRK_20240531_HEADER.csv) - Lists claim information 

[Line](data/STONYBRK_20240531_LINE.csv) - Lists of service line details 

## Summary of Key Findings
1. Claims Overview
    * The dataset contains 388 unique claims.
    * Date range spans September 2023 – May 2024.
    * Each claim averages 1.34 service lines.
    * Each claim includes ~4 diagnosis codes on average.
2. Payer Insights
    * Medicare accounts for the highest total charges (~131k) and has the most claims processed.
    * Healthfirst FFS, HIP Medicaid, and Fidelis plans also contribute significantly.
    * Average charge per claim varies widely across payers (e.g., Aetna & Magnacare > $1,100 per claim).
3. Provider Billing Patterns
    * Certain providers bill large volumes of critical care procedures (HCPCS 99291).
    * Provider-level analysis shows some bill more complex claims, reflected by higher diagnosis code counts.
4. Common Procedures & Diagnoses
    * The most frequent procedure in the dataset is CPT 99291 (critical care, first hour).
    * Top diagnosis codes include neurologic and systemic conditions (G90.8, N17.9, etc.).
5. High-Complexity Claims
    * Several claims have 5 or more service lines, typically associated with higher total charges and more severe clinical encounters.

## Required Libraries
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

---
## Instructions

### Part 1: Data Loading and Exploration
Complete the following tasks in a Google Colab or Jupyter notebook:

1. **Load the three CSV files** into pandas DataFrames
   - Use appropriate variable names: `df_header`, `df_line`, `df_code`

2. **Explore each file** by displaying:
   - Shape (number of rows and columns)
   - First 5 rows
   - Column names and data types
   - Missing value counts
   - Basic descriptive statistics for numeric columns

3. **Document your observations** about:
   - How many unique claims are in the dataset?
   - What is the date range of the claims?
   - How many service lines are there on average per claim?
   - How many diagnosis codes are there on average per claim?

### Part 2: Relational Data Analysis
Answer the following questions using pandas operations (merge, groupby, value_counts, etc.):

**Question 1: Provider Analysis**
- Who are the top 5 billing providers by number of claims?
- Display: Provider name, NPI, and claim count
- Create a simple bar chart showing the top 5 providers

**Question 2: Payer Mix Analysis**
- What are the top 5 primary payers by claim volume?
- Calculate the percentage of total claims for each payer
- Create a bar chart or pie chart showing payer distribution

**Question 3: Common Diagnoses**
- What are the 10 most frequently appearing diagnosis codes (CodeValue)?
- Display: ICD-10 code and frequency count
- Note: You may want to look up what these codes mean online (icd10data.com)

**Question 4: Common Procedures**
- What are the 10 most frequently billed procedure codes (HCPCS)?
- Display: HCPCS code, description (if available in data), and frequency
- Create a bar chart showing the top 10 procedures

**Question 5: Service Location Analysis**
- How many claims were submitted for each PlaceOfService?
- What percentage of claims are for "INPATIENT" vs "DOCTOR'S OFFICE"?

### Part 3: Advanced Analysis with Joins

**Question 6: Claims with High Service Line Counts**
- Merge the HEADER and LINE files
- Calculate the total number of service lines per claim
- Identify claims with 5 or more service lines
- Display: ClaimId, Provider name, number of lines, and total charges

**Question 7: Diagnosis-Procedure Combinations**
- Create a merged dataset linking claims to both procedures and diagnoses
- Find the most common diagnosis code (CodeValue) associated with CPT code 99291
- Hint: You'll need to merge all three files together

**Question 8: Charges by Payer**
- Merge HEADER and LINE files
- Calculate total charges (sum of all line charges) per claim
- Group by PrimaryPayerName and calculate:
  - Total charges
  - Average charges per claim
  - Number of claims
- Sort by total charges descending and display top 10 payers

### Part 4: Creative Analysis  

**Question 9: Your Own Analysis**
Develop and answer your own analytical question using the claims data. Your question should:
- Require merging at least two of the three files
- Use groupby or aggregation
- Provide meaningful insight about the data
- Include at least one visualization

Examples of questions you could explore:
- Which providers bill for the most complex cases (highest number of diagnosis codes)?
- What is the relationship between place of service and average charges?
- Are there seasonal patterns in claim submissions?
- Which diagnosis codes are most commonly paired together?

---