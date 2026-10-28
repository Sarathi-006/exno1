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
### Data Cleaning Process Using Python
```
import pandas as pd

df = pd.read_csv("Data_set (1).csv")
print(df)

df.info()
print(df.describe())
print(df.head())
print(df.shape)
print(df.columns)

print(df.isnull().sum())

print(df.isnull().sum(axis=1))

df_drop = df.dropna()
print(df_drop)

df_zero = df.fillna(0)
print(df_zero)

df_ffill = df.ffill()
print(df_ffill)

df_bfill = df.bfill()
print(df_bfill)

numeric_columns = df.select_dtypes(include="number").columns
df_mean = df.copy()
df_mean[numeric_columns] = df_mean[numeric_columns].fillna(
    df_mean[numeric_columns].mean()
)
print(df_mean)

df = df.dropna()
print(df)

df.to_csv("Cleaned_Data.csv", index=False)
print("Cleaned data saved successfully.")
```
### Outlier Detection and Removal Using IQR
```
import pandas as pd
import matplotlib.pyplot as plt

age = [1, 3, 28, 27, 25, 92, 30, 39, 40, 50, 26, 24, 29, 94]
af = pd.DataFrame(age, columns=["Age"])

af.boxplot(column="Age")
plt.title("Boxplot Before IQR Outlier Removal")
plt.show()

Q1 = af["Age"].quantile(0.25)
Q3 = af["Age"].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

print("Outlier values:")
print(af[(af["Age"] < lower_bound) | (af["Age"] > upper_bound)])

af_clean = af[
    (af["Age"] >= lower_bound) & (af["Age"] <= upper_bound)
]
print("Data after removing outliers:")
print(af_clean)

af_clean.boxplot(column="Age")
plt.title("Boxplot After IQR Outlier Removal")
plt.show()
```
### Outlier Detection and Removal Using Z-Score
```
import pandas as pd
import matplotlib.pyplot as plt
from scipy import stats

data = [
    1, 12, 15, 18, 21, 24, 27, 30, 33, 36, 39, 42, 45, 48, 51, 54,
    57, 60, 63, 66, 69, 72, 75, 78, 81, 84, 87, 90, 93, 96, 99, 158
]

zdf = pd.DataFrame(data, columns=["Value"])

zdf.boxplot(column="Value")
plt.title("Boxplot Before Z-Score Outlier Removal")
plt.show()

z_scores = stats.zscore(zdf["Value"])

print("Outlier values:")
print(zdf[abs(z_scores) > 3])

zdf_clean = zdf[abs(z_scores) <= 3]
print("Data after removing outliers:")
print(zdf_clean)

zdf_clean.boxplot(column="Value")
plt.title("Boxplot After Z-Score Outlier Removal")
plt.show()
```
# Result
          <<include your Result here>>
