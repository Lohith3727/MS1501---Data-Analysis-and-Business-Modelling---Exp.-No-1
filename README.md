# Experiment No. 1: Data Cleaning and Preprocessing

## Aim

To perform data cleaning and preprocessing on a business dataset using Python libraries for better data quality and analysis readiness.

## Dataset

The dataset used for this experiment is `heartdisease.csv`. It contains
medical and demographic information related to heart disease patients.

The dataset is opened and analyzed using Jupyter Notebook to study its
data structure, identify data types, and perform basic statistical
analysis for data-cleaning and preprocessing purposes.

## Algorithm

1.  Import essential Python libraries.
2.  Load the dataset using Pandas.
3.  View the dataset structure, data types, and memory usage.
4.  Check for missing values and duplicates.
5.  Perform data summary statistics using `describe()`.
6.  View initial and final records using `head()` and `tail()`.
7.  Sort and group the data based on key attributes.
8.  Rename columns or modify data where necessary.
9.  Save the cleaned dataset for further analysis.

## Functions and Methods Used in the Experiment

### 1. Data Loading and Basic Exploration

  Function / Method      Description  
  ---------------------- ------------------------------------------------------\
  `pd.read_csv()`        Reads a CSV file into a Pandas DataFrame.\
  `df.info()`            Displays column names, data types, and memory usage.\
  `df.dtypes`            Returns the data types of all columns.\
  `df['column'].dtype`   Returns the data type of a specific column.\
  `df.describe()`        Provides summary statistics for numerical columns.\
  `df.head()`            Displays the first 5 rows of the DataFrame.\
  `df.tail()`            Displays the last 5 rows of the DataFrame.\

### 2. Sorting and Grouping

  Function / Method    Description  
  -------------------- ---------------------------------------------  
  `df.sort_values()`   Sorts the DataFrame by one or more columns.  
  `df.groupby()`       Groups data based on one or more columns.  
  `groupby.sum()`      Returns the sum for each group.  
  `groupby.mean()`     Returns the mean for each group.  
  `groupby.median()`   Returns the median for each group.  
  `groupby.max()`      Returns the maximum value in each group.  
  `groupby.min()`      Returns the minimum value in each group.  

### 3. Data Summary and Manipulation  

  Function / Method   Description  
  ------------------- ----------------------------------------------  
  `df.mean()`         Calculates the mean for all numeric columns.  
  `df.rename()`       Renames columns in the DataFrame.  

### 4. Optional Additions  

  Function / Method         Description  
  ------------------------- ----------------------------------------------  
  `df.isnull().sum()`       Checks for missing values in each column.  
  `df.duplicated().sum()`   Counts duplicate rows.  
  `df.dropna()`             Removes rows containing missing values.  
  `df.fillna()`             Fills missing values with a specified value.  
  `df.drop_duplicates()`    Removes duplicate rows.  
  `df.shape`                Returns the number of rows and columns.  
  `df.columns`              Lists column names in the DataFrame.  

## Program 
# 1. Import essential Python libraries
import pandas as pd
import numpy as np

# 2. Load the dataset using Pandas
df = pd.read_csv('heartdisease.csv')

# 3. View dataset structure, shape, columns, data types, and memory usage
print("Dataset Shape (Rows, Columns):", df.shape)
print("\nColumn Names:\n", df.columns.tolist())

print("\n--- Dataset Info ---")
df.info()

print("\n--- Data Types of All Columns ---")
print(df.dtypes)
print("\nData Type of 'age' column:", df['age'].dtype)

# 4. Check for missing values and duplicates
print("\n--- Missing Values per Column ---")
print(df.isnull().sum())

print("\nTotal Duplicate Rows:", df.duplicated().sum())

# Handling missing values and duplicates
# Fill missing numeric values with column mean (if any) and drop remaining nulls/duplicates
df_cleaned = df.fillna(df.mean(numeric_only=True))
df_cleaned = df_cleaned.dropna()
df_cleaned = df_cleaned.drop_duplicates()

print("Shape after removing duplicates and nulls:", df_cleaned.shape)

# 5. Perform data summary statistics using describe() and mean()
print("\n--- Statistical Summary ---")
print(df_cleaned.describe())

print("\n--- Mean of Numeric Columns ---")
print(df_cleaned.mean(numeric_only=True))

# 6. View initial and final records using head() and tail()
print("\n--- First 5 Records ---")
print(df_cleaned.head())

print("\n--- Last 5 Records ---")
print(df_cleaned.tail())

# 7. Sort and group the data based on key attributes
df_sorted = df_cleaned.sort_values(by='age', ascending=True)
print("\n--- Top 5 Records Sorted by Age ---")
print(df_sorted[['age', 'sex', 'cp', 'chol', 'target']].head())

# Grouping by 'target' (0 = No Heart Disease, 1 = Heart Disease)
grouped = df_cleaned.groupby('target')

print("\n--- Groupby Sum ---")
print(grouped[['age', 'chol']].sum())

print("\n--- Groupby Mean ---")
print(grouped[['age', 'trestbps', 'chol']].mean())

print("\n--- Groupby Median ---")
print(grouped[['age', 'trestbps', 'chol']].median())

print("\n--- Groupby Max ---")
print(grouped[['age', 'chol']].max())

print("\n--- Groupby Min ---")
print(grouped[['age', 'chol']].min())

# 8. Rename columns or modify data where necessary
df_cleaned = df_cleaned.rename(columns={
    'cp': 'chest_pain_type',
    'trestbps': 'resting_bp',
    'chol': 'cholesterol',
    'thalach': 'max_heart_rate'
})
print("\n--- Updated Column Names ---")
print(df_cleaned.columns.tolist())

# 9. Save the cleaned dataset for further analysis
df_cleaned.to_csv('heartdisease_cleaned.csv', index=False)
print("\nCleaned dataset successfully saved as 'heartdisease_cleaned.csv'.")

# Output
Dataset Shape (Rows, Columns): (303, 14)

Column Names:
 ['age', 'sex', 'cp', 'trestbps', 'chol', 'fbs', 'restecg', 'thalach', 'exang', 'oldpeak', 'slope', 'ca', 'thal', 'target']

--- Dataset Info ---
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 303 entries, 0 to 302
Data columns (total 14 columns):
 #   Column    Non-Null Count  Dtype  
---  ------    --------------  -----  
 0   age       303 non-null    int64  
 1   sex       303 non-null    int64  
 2   cp        303 non-null    int64  
 3   trestbps  303 non-null    int64  
 4   chol      303 non-null    int64  
 ...
dtypes: float64(1), int64(13)
memory usage: 33.3 KB

--- Data Types of All Columns ---
age           int64
sex           int64
cp            int64
trestbps      int64
chol          int64
...
Data Type of 'age' column: int64

--- Missing Values per Column ---
age         0
sex         0
cp          0
trestbps    0
chol        0
...
Total Duplicate Rows: 1
Shape after removing duplicates and nulls: (302, 14)

--- Statistical Summary ---
              age         sex          cp    trestbps        chol  ...
count  302.000000  302.000000  302.000000  302.000000  302.000000  ...
mean    54.420530    0.682119    0.963576  131.602649  246.500000  ...
std      9.047970    0.466426    1.032044   17.563394   51.753489  ...
min     29.000000    0.000000    0.000000   94.000000  126.000000  ...
50%     55.500000    1.000000    1.000000  130.000000  240.500000  ...
max     77.000000    1.000000    3.000000  200.000000  564.000000  ...

--- Groupby Mean ---
              age    trestbps        chol
target                                   
0       56.601449  134.398551  251.086957
1       52.585366  129.250000  242.640244

--- Updated Column Names ---
['age', 'sex', 'chest_pain_type', 'resting_bp', 'cholesterol', 'fbs', 'restecg', 'max_heart_rate', 'exang', 'oldpeak', 'slope', 'ca', 'thal', 'target']

Cleaned dataset successfully saved as 'heartdisease_cleaned.csv'.
## Result
The heartdisease.csv dataset was successfully loaded, explored, cleaned, and preprocessed using Python and Pandas in Jupyter Notebook. Missing values and duplicate records were identified and removed, statistical summaries and group-level aggregations were computed, columns were renamed for clarity, and the final preprocessed dataset was exported to heartdisease_cleaned.csv ready for further analysis

