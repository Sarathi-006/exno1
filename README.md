# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
```
import pandas as pd
import numpy as np
from scipy import stats
import matplotlib.pyplot as plt
```
```
df = pd.read_csv("Data_set.csv")

print(df.head())
print(df.info())
print(df.isnull().sum())

for col in df.select_dtypes(include="number").columns:
    df[col] = df[col].fillna(df[col].median())

for col in df.select_dtypes(include=["object", "string"]).columns:
    if df[col].isnull().any() and not df[col].mode().empty:
        df[col] = df[col].fillna(df[col].mode()[0])

print("\nAfter cleaning:\n", df.isnull().sum())
df.to_csv("cleaned_Data_set.csv", index=False)
print("Saved successfully!")
```
<img width="596" height="788" alt="image" src="https://github.com/user-attachments/assets/a4869392-4c37-4830-a1b7-59329ba56fdd" />

```
df = pd.read_csv("SAMPLEIDS.csv")

print(df.head())
print("Missing values:\n", df.isnull().sum())
print("Duplicate rows:", df.duplicated().sum())

df = df.drop_duplicates()

# Inspect categorical inconsistencies
for col in df.select_dtypes(include=["object", "string"]).columns:
    print(f"\n{col}:", df[col].value_counts(dropna=False))

# Standardize text
for col in df.select_dtypes(include=["object", "string"]).columns:
    df[col] = df[col].str.strip().str.upper()

# Fill missing values
for col in df.select_dtypes(include="number").columns:
    df[col] = df[col].fillna(df[col].median())

for col in df.select_dtypes(include=["object", "string"]).columns:
    if df[col].isnull().any() and not df[col].mode().empty:
        df[col] = df[col].fillna(df[col].mode()[0])

print("\nRemaining missing values:\n", df.isnull().sum())
df.to_csv("cleaned_SAMPLEIDS.csv", index=False)
print("Saved successfully!")
```
<img width="597" height="786" alt="image" src="https://github.com/user-attachments/assets/f1762e28-72e6-4361-9999-4151878a866b" />
<img width="595" height="481" alt="image" src="https://github.com/user-attachments/assets/8228d5d3-26c9-4a88-9e7a-ed14202a7506" />


# Summary
The given Python code performs data cleaning on two datasets, Data_set.csv and SAMPLEIDS.csv, using the Pandas library. First, it loads the datasets and examines the first few rows, data types, missing values, and duplicate records.

For Data_set.csv, missing numerical values are replaced with the median, while missing categorical values are filled with the mode. The cleaned dataset is saved as cleaned_Data_set.csv.

For SAMPLEIDS.csv, duplicate rows are removed, categorical values are inspected and standardized by removing extra spaces and converting text to uppercase. Missing numerical and categorical values are then filled using the median and mode, respectively. Finally, the cleaned dataset is saved as cleaned_SAMPLEIDS.csv.

# Result
Thus the given data successfully performed data cleaning and saved the cleaned data to a file.
