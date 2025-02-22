# EXP 2 : Cleaning the Dataset and handling the Outliers
This repository includes a collection of easy-to-follow scripts and instructions.It demonstrates a step-by-step approach to handle raw data, remove inconsistencies, handle missing values, normalize features, and produce a clean, well-structured dataset ready for exploration or modeling.

# Experiment Overview
# Steps:
**1. Loading the dataset :** *Importing the data from a CSV file into a DataFrame to facilitate data cleaning and analysis.*
<br>
**2. Checking for missing values :** *This involves identifying columns with null or missing data to understand the extent of data gaps in the dataset.*
<br>
**3. Checking for duplicated values :** *Identifying and counting any repeated rows in the dataset to ensure data integrity.*
<br>
**4. Removing duplicated values :** *Eliminating identical rows from the dataset to avoid redundancy and ensure accurate analysis.*
<br>
**5. Handling outliers :** *Identifying and removing data points that fall outside a specified range, ensuring the dataset's consistency and preventing skewed analysis.*
<br>
**6. Saving the cleaned data :** *Storing the processed dataset into a new file, ensuring the cleaned version is available for future use or analysis.*

# Key Concepts Applied:
**-Data Loading :** _Importing data from a CSV file into a Pandas DataFrame using pd.read_csv() for further analysis and processing._
<br>
**-Handling Missing Values :** _Checking for missing (null) values using isnull().sum() and notnull().sum() to help identify where data is incomplete._
<br>
**-Identifying and removing duplicates :** _Checking for duplicate rows using duplicated().sum() and removing them using drop_duplicates() to ensure data consistency._
<br>
**-Handling Outliers :** _The IQR method identifies outliers by calculating the first and third quartiles (Q1 and Q3), setting bounds, and removing data points outside these bounds to ensure accurate analysis._
<br>
**-Saving the cleaned data :** _After removing outliers, the cleaned dataset is saved as a new CSV file for further analysis._

# Action Plan
**1. Get started with Google Colab :**

 *~Launch Google Colab.*
 <br>
 *~Start a fresh notebook.*

 **2. Import necessary libraries :**

 *~Initialize the necessary libraries for the analysis.*
 ```
import pandas as pd
```

**3. Load the Dataset :**

*~Download the datasets from the UCI Machine Learning Repository and mount Google Drive to access them.*
```
df = pd.read_csv('/content/drive/MyDrive/Rotten Tomatoes Movies.csv')
print(df.columns)
```

**4. Check for missing values :**

*~Identify and count any missing values (null values) in the dataset.*
```
print("Checking for null values(is null)")
df.isnull().sum()

print("Checking for null values(not null)")
df.notnull().sum()
```

**5. Check for duplicates :**

*~Identify any duplicated rows in the dataset.*
```
print("Checking for duplicated values")
df.duplicated().sum()
```

**6. Remove duplicated rows :**

*~Remove any duplicated rows found in the dataset to avoid redundancy and ensure clean data.*
```
print("After dropping duplicated values")
df.drop_duplicates()
```

**7. Clean column names :**

*~Strip any leading or trailing spaces from the column names to avoid inconsistencies.*
```
df.columns = df.columns.str.strip()
print("Column Names:", df.columns)
```

**8. Handle Outliers using the IQR method :**
*~Identify and remove outliers using the Interquartile Range (IQR) method:*
```
q1 = df['audience_count'].quantile(0.25)
q3 = df['audience_count'].quantile(0.75)
iqr = q3 - q1

lower_bound = q1 - 1.5 * iqr
upper_bound = q3 + 1.5 * iqr

df_clean = df[(df['audience_count'] >= lower_bound) & (df['audience_count'] <= upper_bound)]
```

**9. Save the cleaned data :**
*~Save the cleaned dataset (after removing outliers and duplicates) into a new CSV file for future use.*
```
df_clean.to_csv("/content/drive/MyDrive/cleaned_movies.csv", index=False)
print("Outliers removed! Cleaned data saved as 'cleaned_movies.csv'.")
```
