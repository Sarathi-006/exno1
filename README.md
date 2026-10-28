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
# Output
<img width="490" height="553" alt="Screenshot 2026-10-28 134134" src="https://github.com/user-attachments/assets/9b96a693-e38c-4809-871b-3b1d497d17c3" />
<img width="611" height="657" alt="Screenshot 2026-10-28 134011" src="https://github.com/user-attachments/assets/a499c8f9-6be9-4e0a-b0c2-ad174eca02a9" />
<img width="603" height="831" alt="Screenshot 2026-10-28 134035" src="https://github.com/user-attachments/assets/e201e3fc-89ea-40d5-8d58-416fbdf9ebca" />
<img width="528" height="552" alt="Screenshot 2026-10-28 134109" src="https://github.com/user-attachments/assets/b1fa14c2-dd9d-4327-a2a7-201de0706106" />
<img width="497" height="552" alt="Screenshot 2026-10-28 134115" src="https://github.com/user-attachments/assets/1b2eb7e7-efda-4771-b01b-cd0ecfa0abc9" />
<img width="485" height="557" alt="Screenshot 2026-10-28 134122" src="https://github.com/user-attachments/assets/fe4b4f26-e250-42ee-a7c5-1626b1807c6a" />
<img width="516" height="555" alt="Screenshot 2026-10-28 134127" src="https://github.com/user-attachments/assets/9484b390-51e6-4125-91d1-e685a002c02a" />


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
# Output
<img width="545" height="397" alt="Screenshot 2026-10-28 134331" src="https://github.com/user-attachments/assets/bad96181-9be0-4808-a105-f6c03a1ff700" />
<img width="912" height="365" alt="Screenshot 2026-10-28 134403" src="https://github.com/user-attachments/assets/757f3954-f12f-4ab2-aa8d-c72aa267985e" />
<img width="668" height="742" alt="Screenshot 2026-10-28 134409" src="https://github.com/user-attachments/assets/678b55e5-37a1-45c6-91bc-80f97048de57" />
<img width="588" height="556" alt="Screenshot 2026-10-28 134416" src="https://github.com/user-attachments/assets/ff6c3d41-4011-4a60-a3c3-21e7ce3b4d8b" />
<img width="853" height="363" alt="Screenshot 2026-10-28 134445" src="https://github.com/user-attachments/assets/f00f4f9c-b953-4d29-91f9-d7cca8277b72" />

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
# Output
<img width="448" height="447" alt="Screenshot 2026-10-28 134601" src="https://github.com/user-attachments/assets/d8da35d3-c7b9-443f-9065-50f6ecfa1357" />
<img width="817" height="362" alt="Screenshot 2026-10-28 134607" src="https://github.com/user-attachments/assets/0e83ba1b-6e91-4218-b225-2e818c087977" />

# Result
Thus the data cleaning process on the given dataset is executed successfully.
