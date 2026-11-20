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
import pandas as pd  
import numpy as np  

df = pd.read_csv('heartdisease.csv')  
df.head()  

print("Dataset Shape (Rows, Columns):", df.shape)  
print("\nColumn Names:\n", df.columns.tolist())  

print("\n--- Dataset Info ---")  
df.info()  

print("\n--- Data Types of All Columns ---")  
print(df.dtypes)  

print("\nData Type of 'age' column:", df['age'].dtype)  

print("\n--- Missing Values per Column ---")  
print(df.isnull().sum())  

print("\nTotal Duplicate Rows:", df.duplicated().sum())  

df_cleaned = df.copy()  

# Fill missing numeric values with their respective column means  
df_cleaned = df_cleaned.fillna(df_cleaned.mean(numeric_only=True))  

# Remove any remaining rows containing missing values  
df_cleaned = df_cleaned.dropna()  

# Remove duplicate rows  
df_cleaned = df_cleaned.drop_duplicates()  

print("Shape after removing duplicates and nulls:", df_cleaned.shape)  

print("\n--- Statistical Summary ---")  
display(df_cleaned.describe())  

print("\n--- Mean of Numeric Columns ---")  
print(df_cleaned.mean(numeric_only=True))  

print("\n--- First 5 Records ---")  
display(df_cleaned.head())  

print("\n--- Last 5 Records ---")  
display(df_cleaned.tail())  

df_sorted = df_cleaned.sort_values(by='age', ascending=True)  

print("\n--- Top 5 Records Sorted by Age ---")  
display(df_sorted[['age', 'sex', 'cp', 'chol', 'target']].head())  

grouped = df_cleaned.groupby('target')  

print("\n--- Groupby Sum ---")  
display(grouped[['age', 'chol']].sum())  

print("\n--- Groupby Mean ---")  
display(grouped[['age', 'trestbps', 'chol']].mean())  

print("\n--- Groupby Median ---")  
display(grouped[['age', 'trestbps', 'chol']].median())  

print("\n--- Groupby Max ---")  
display(grouped[['age', 'chol']].max())  

print("\n--- Groupby Min ---")  
display(grouped[['age', 'chol']].min())  

df_cleaned = df_cleaned.rename(columns={  
    'cp': 'chest_pain_type',  
    'trestbps': 'resting_bp',  
    'chol': 'cholesterol',  
    'thalach': 'max_heart_rate'  
})  

print("\n--- Updated Column Names ---")  
print(df_cleaned.columns.tolist())  

df_cleaned.to_csv('heartdisease_cleaned.csv', index=False)  
print("Cleaned dataset successfully saved as 'heartdisease_cleaned.csv'.")  

## Result
The heartdisease.csv dataset was successfully loaded, explored, cleaned, and preprocessed using Python and Pandas in Jupyter Notebook. Missing values and duplicate records were identified and removed, statistical summaries and group-level aggregations were computed, columns were renamed for clarity, and the final preprocessed dataset was exported to heartdisease_cleaned.csv ready for further analysis

