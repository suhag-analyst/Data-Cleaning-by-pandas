# Financial Transaction Data Cleaning and Exploratory Data Analysis

## 📌 Project Overview

This project focuses on cleaning, preprocessing, validating, and exploring a financial transaction dataset using Python and Pandas.

The dataset contains information about financial transactions, including transaction IDs, dates, account information, transaction types, transaction amounts, currencies, exchange rates, balances, merchants, categories, locations, and fraud indicators.

The main objective of this project is to transform raw and potentially inconsistent data into a clean, structured, and analysis-ready dataset.

---

## 🎯 Project Objectives

The main objectives of this project are:

- Inspect the structure and quality of the dataset
- Check and handle missing values
- Detect and remove duplicate records
- Check and correct data types
- Standardize date formats
- Clean text and string values
- Remove unnecessary characters and spaces
- Replace incorrect or inconsistent values
- Detect potential outliers
- Drop unnecessary columns
- Perform data validation
- Filter data based on specific conditions
- Perform GroupBy analysis
- Create Pivot Tables
- Validate the final cleaned dataset
- Export the cleaned dataset for further analysis

---

## 🛠️ Tools and Technologies

The following tools and libraries were used:

- Python
- Jupyter Notebook
- Pandas
- NumPy


---

## 📂 Dataset Information

The dataset contains financial transaction records.

### Main Columns

The dataset includes the following columns:

- `transactionid`
- `date`
- `accountid`
- `accountname`
- `transactiontype`
- `amount`
- `currency`
- `exchangerate`
- `balance`
- `merchant`
- `merchantphone`
- `merchantemail`
- `category`
- `subcategory`
- `country`
- `city`
- `postalcode`
- `cardnumber`
- `email`
- `phone`
- `isfraud`
- `notes`
- `customersince`

---

# 🔍 Data Cleaning Process

## 1. Initial Data Inspection

The dataset was initially inspected using Pandas functions such as:

- `head()`
- `tail()`
- `shape`
- `columns`
- `info()`
- `dtypes`

These functions were used to understand the structure, size, columns, and data types of the dataset.

---

## 2. Checking the First and Last Records

The first few records were inspected using:

```python
df.head()The last few records were inspected using:

df.tail()

This helped identify potential formatting and data-entry problems.

3. Checking Dataset Dimensions

The number of rows and columns was checked using:

df.shape

This was used to monitor the dataset before and after the cleaning process.

4. Checking Column Names

The column names were examined using:

df.columns

Column names were standardized where necessary to make them easier to use in Python.

5. Missing Value Analysis

Missing values were checked using:

df.isnull().sum()

The dataset was carefully examined for missing values.

Different methods were considered for handling missing numerical and categorical values.

Mean

For appropriate numerical variables:

df['column'].fillna(df['column'].mean(), inplace=True)
Median

For numerical variables where median was more appropriate:

df['column'].fillna(df['column'].median(), inplace=True)
Mode

For categorical variables:

df['column'].fillna(df['column'].mode()[0], inplace=True)

After cleaning, the final dataset contains no missing values.

6. Duplicate Value Detection

Duplicate records were checked using:

df.duplicated().sum()

Duplicate records were removed when necessary using:

df.drop_duplicates(inplace=True)
Final Result
Duplicate records = 0

Therefore, the final dataset contains no duplicate records.

🧹 7. String Cleaning

String and categorical columns were cleaned using Pandas string functions.

Removing Leading and Trailing Spaces
df['column'] = df['column'].str.strip()

This removes unnecessary spaces from text values.

Converting Text to a Standard Format

For example:

df['currency'] = df['currency'].str.upper()

This helps standardize values such as:

usd → USD
gbp → GBP
aed → AED
Replacing Incorrect Values

Inconsistent or incorrect categorical values were standardized using:

df['column'] = df['column'].replace({
    'old_value': 'new_value'
})
💰 8. Currency Data Cleaning

The currency column was checked for inconsistent values and standardized

df['currency'] = df['currency'].map(curr)

Currency values were standardized while preserving the corresponding transaction exchange rates.

🔢 9. Data Type Checking and Correction

Data types were checked using:

df.dtypes

Incorrect data types were converted into appropriate formats.

Numerical Variables
df['amount'] = pd.to_numeric(df['amount'], errors='coerce')
df['exchangerate'] = pd.to_numeric(df['exchangerate'], errors='coerce')
df['balance'] = pd.to_numeric(df['balance'], errors='coerce')
Date Variables

The date column was converted into a proper datetime format:

df['date'] = pd.to_datetime(df['date'], errors='coerce')

The customersince column was also converted where appropriate.

📅 10. Date Format Correction

Date values were checked and standardized using Pandas:

df['date'] = pd.to_datetime(
    df['date'],
    errors='coerce'
)

This ensures that the date column is stored in a proper datetime format and can be used for time-based analysis.

For example:

YYYY-MM-DD
📊 11. Outlier Detection

Potential outliers were detected for important numerical variables such as:

amount
exchangerate
balance

The Interquartile Range (IQR) method was used.

IQR Formula
IQR = Q3 - Q1

Lower Bound = Q1 - 1.5 × IQR

Upper Bound = Q3 + 1.5 × IQR

Example:

Q1 = df['amount'].quantile(0.25)
Q3 = df['amount'].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

outliers = df[
    (df['amount'] < lower) |
    (df['amount'] > upper)
]

Potential outliers were reviewed carefully rather than automatically removing every extreme observation, because unusually large financial transactions may represent legitimate transactions.

🗑️ 12. Dropping Unnecessary Columns

Columns that were unnecessary for the intended analysis were removed where appropriate.

Example:

df.drop(columns=['column_name'], inplace=True)

Only columns that were not required for the final analysis were removed.

✅ 13. Data Validation

Several validation checks were performed to ensure the quality of the cleaned dataset.

The following were checked:

Missing values
Duplicate records
Data types
Date formats
Numerical values
Categorical values
Currency consistency
Transaction values
Invalid values
Unique identifiers

Example:

df.info()
df.isnull().sum()
df.duplicated().sum()
df.describe()
🔎 14. Filtering Data

Filtering was performed to investigate specific subsets of the dataset.

Example:

df[df['amount'] > 1000]

Fraudulent transactions:

df[df['isfraud'] == True]

Specific currency:

df[df['currency'] == 'USD']

Filtering helped investigate unusual and important observations.

📈 15. GroupBy Analysis

GroupBy operations were performed to summarize the transaction data.

Transaction Type Analysis
df.groupby('transactiontype')['amount'].agg(
    ['count', 'sum', 'mean']
)
Category Analysis
df.groupby('category')['amount'].agg(
    ['count', 'sum', 'mean']
)
Country Analysis
df.groupby('country')['amount'].agg(
    ['count', 'sum', 'mean']
)
Currency Analysis
df.groupby('currency')['amount'].agg(
    ['count', 'sum', 'mean']
)

GroupBy analysis helped identify patterns and differences across transaction categories, currencies, countries, and transaction types.

📋 16. Pivot Table Analysis

Pivot tables were created to summarize the cleaned data from different perspectives.

Category vs Transaction Type
pd.pivot_table(
    df,
    values='amount',
    index='category',
    columns='transactiontype',
    aggfunc='sum',
    fill_value=0
)
Country vs Currency
pd.pivot_table(
    df,
    values='amount',
    index='country',
    columns='currency',
    aggfunc='sum',
    fill_value=0
)

Pivot tables were used to compare transaction amounts across multiple categories and dimensions.

🔁 17. Final Dataset Validation

After completing all cleaning operations, the dataset was checked again.

Final Shape
df.shape
Final Columns
df.columns
Final Head
df.head()
Final Tail
df.tail()
Final Missing Values
df.isnull().sum()
Final Duplicate Check
df.duplicated().sum()
📌 Final Data Quality Result

After completing the data cleaning process:

✅ Data types were checked and corrected
✅ Date formats were standardized
✅ Missing values were handled
✅ No missing values remain in the final dataset
✅ Duplicate records were checked and removed
✅ Final duplicate count = 0
✅ String values were cleaned
✅ Inconsistent values were standardized
✅ Potential outliers were identified
✅ Unnecessary columns were removed where required
✅ Data validation was performed
✅ Filtering was performed
✅ GroupBy analysis was performed
✅ Pivot Table analysis was performed
✅ Final dataset is ready for further analysi

This project demonstrates practical skills in:

Python Programming
Pandas
Data Cleaning
Data Preprocessing
Missing Value Handling
Duplicate Detection
Data Type Conversion
DateTime Processing
String Manipulation
Data Validation
Outlier Detection
Data Filtering
GroupBy
Pivot Table
Financial Data Analysis
🚀 Conclusion

This project demonstrates a complete data cleaning workflow using Python and Pandas.

The raw financial transaction data was inspected, cleaned, transformed, validated, and prepared for further analysis.

The final dataset contains no missing values and no duplicate records, and the data types and date formats have been standardized.

GroupBy and Pivot Table techniques were also applied to summarize and understand transaction patterns.

The cleaned dataset can now be used for further:

Exploratory Data Analysis (EDA)
Data Visualization
Statistical Analysis
Fraud Analysis
Financial Analysis

Tools Used

Python | Pandas | Jupyter Notebook

⭐ If you find this project useful, feel free to explore the notebook and cleaned dataset.
