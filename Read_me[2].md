# Financial Transaction Data Cleaning & EDA

## 📌 Project Overview

This project focuses on cleaning, preprocessing, validating, and exploring a financial transaction dataset using **Python, Pandas, and Jupyter Notebook**.

The main objective is to transform raw financial transaction data into a clean, consistent, and analysis-ready dataset.

---

## 📂 Dataset Columns

The dataset contains the following columns:

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

# 🧹 Data Cleaning Process

The following data-cleaning and preprocessing techniques were applied.

## 1. Initial Data Inspection

The dataset was inspected using:

- `head()`
- `tail()`
- `shape`
- `columns`
- `info()`
- `dtypes`

## 2. Missing Value Handling

Missing values were identified using:

```python
df.isnull().sum()
```

Appropriate methods were used to handle missing values, including:

- Mean
- Median
- Mode

Examples:

```python
df['column'].fillna(df['column'].mean())
df['column'].fillna(df['column'].median())
df['column'].fillna(df['column'].mode()[0])
```

### Final Result

**No missing values remain in the final cleaned dataset.**

---

## 3. Duplicate Detection and Removal

Duplicate records were checked using:

```python
df.duplicated().sum()
```

Duplicates were removed using:

```python
df.drop_duplicates(inplace=True)
```

### Final Result

**Duplicate records = 0**

---

## 4. Data Type Checking and Correction

Data types were checked using:

```python
df.dtypes
```

Incorrect data types were converted into appropriate formats.

For example:

```python
df['amount'] = pd.to_numeric(df['amount'], errors='coerce')
df['exchangerate'] = pd.to_numeric(df['exchangerate'], errors='coerce')
df['balance'] = pd.to_numeric(df['balance'], errors='coerce')
```

---

## 5. Date Format Correction

The date column was converted into a proper datetime format:

```python
df['date'] = pd.to_datetime(df['date'], errors='coerce')
```

The `customersince` column was also checked and corrected where necessary.

---

## 6. String Cleaning

String values were cleaned using Pandas string functions.

### Removing Extra Spaces

```python
df['column'] = df['column'].str.strip()
```

### Standardizing Text

```python
df['currency'] = df['currency'].str.upper()
```

### Replacing Inconsistent Values

```python
df['column'] = df['column'].replace({
    'old_value': 'new_value'
})
```

---

## 7. Currency Cleaning

Currency values were standardized so that inconsistent values such as different capitalization or incorrect representations could be handled consistently.

Example:

```python
curr = {
    'USD': 'USD',
    'irn': 'INR',
    'IRNr': 'INR',
    'gbp': 'GBP',
    'aed': 'AED',
    'GBP': 'GBP',
    'AED': 'AED',
    'INR': 'INR'
}

df['currency'] = df['currency'].map(curr)
```

The exchange-rate values were preserved according to the transaction records.

---

## 8. Outlier Detection

Potential outliers were checked for important numerical variables such as:

- `amount`
- `exchangerate`
- `balance`

The **Interquartile Range (IQR)** method was used.

### Formula

```text
IQR = Q3 - Q1

Lower Bound = Q1 - 1.5 × IQR

Upper Bound = Q3 + 1.5 × IQR
```

Outliers were reviewed carefully instead of automatically deleting every extreme value because an unusually large financial transaction can be legitimate.

---

## 9. Data Validation

Several validation checks were performed:

- Missing values
- Duplicate records
- Data types
- Date formats
- Numerical values
- Categorical values
- Currency consistency
- Transaction values
- Unique identifiers

Final validation included:

```python
df.info()
df.isnull().sum()
df.duplicated().sum()
df.describe()
```

---

## 10. Dropping Unnecessary Columns

Columns that were not required for the intended analysis were removed where appropriate using:

```python
df.drop(columns=['column_name'], inplace=True)
```

---

# 🔎 Exploratory Data Analysis

After cleaning the data, several analysis techniques were applied.

## Filtering Data

Examples:

```python
df[df['amount'] > 1000]
```

```python
df[df['currency'] == 'USD']
```

```python
df[df['isfraud'] == True]
```

---

## 📈 GroupBy Analysis

GroupBy was used to summarize transaction information.

Example:

```python
df.groupby('category')['amount'].agg(
    ['count', 'sum', 'mean']
)
```

Other analyses included:

- Transaction type
- Category
- Country
- Currency
- Fraud status

---

## 📊 Pivot Table Analysis

Pivot tables were created to compare different dimensions of the financial transactions.

Example:

```python
pd.pivot_table(
    df,
    values='amount',
    index='category',
    columns='transactiontype',
    aggfunc='sum',
    fill_value=0
)
```

---

# 📋 Final Data Validation

After completing the cleaning process, the dataset was checked again.

### Final Head

```python
df.head()
```

### Final Tail

```python
df.tail()
```

### Final Columns

```python
df.columns
```

### Final Shape

```python
df.shape
```

### Final Data Types

```python
df.dtypes
```

### Final Missing Value Check

```python
df.isnull().sum()
```

**Result: No missing values remain in the final cleaned dataset.**

### Final Duplicate Check

```python
df.duplicated().sum()
```

**Result: 0 duplicate records.**

---

# 📌 Final Data Quality Summary

| Data Quality Check | Status |
|---|---|
| Missing Values | ✅ 0 |
| Duplicate Records | ✅ 0 |
| Data Types | ✅ Checked & Corrected |
| Date Format | ✅ Corrected |
| String Values | ✅ Cleaned |
| Currency Values | ✅ Standardized |
| Outliers | ✅ Detected & Reviewed |
| Unnecessary Columns | ✅ Removed Where Required |
| Data Validation | ✅ Completed |
| Data Filtering | ✅ Completed |
| GroupBy Analysis | ✅ Completed |
| Pivot Table Analysis | ✅ Completed |

---

# 🛠️ Technologies Used

- **Python**
- **Pandas**
- **Jupyter Notebook**

---

# 🎯 Skills Demonstrated

- Data Inspection
- Data Cleaning
- Data Preprocessing
- Missing Value Handling
- Mean, Median, and Mode Imputation
- Duplicate Detection and Removal
- Data Type Checking and Conversion
- DateTime Processing
- Date Format Correction
- String Manipulation
- String Cleaning using `strip()`
- Value Replacement
- Currency Standardization
- Outlier Detection using IQR
- Data Validation
- Column Selection and Removal
- Data Filtering
- GroupBy Analysis
- Pivot Table Analysis

---

# 🚀 Conclusion

The financial transaction dataset was successfully cleaned, validated, and prepared for further analysis using **Python, Pandas, and Jupyter Notebook**.

During the cleaning process, the dataset was inspected for missing values, duplicate records, incorrect data types, inconsistent strings, incorrect date formats, and potential outliers.

Missing values were handled using appropriate methods such as **mean, median, and mode imputation**. Duplicate records were identified and removed. String values were cleaned using methods such as `strip()`, and inconsistent values were standardized.

Numerical variables were converted into appropriate data types, while date columns were converted into proper datetime formats. Potential outliers were detected using the **Interquartile Range (IQR)** method and reviewed carefully.

After cleaning, the dataset was validated again. The final dataset contains **no missing values and zero duplicate records**.

GroupBy and Pivot Table techniques were also applied to summarize and explore transaction patterns across categories, transaction types, countries, currencies, and fraud status.

The cleaned dataset is now ready for further:

- 📊 Exploratory Data Analysis (EDA)
- 📈 Data Visualization
- 📉 Statistical Analysis
- 🔎 Fraud Analysis
- 🤖 Machine Learning
- 💰 Financial Data Analysis

---

# 👨‍💻 Author

**Your Name**

### Project

**Financial Transaction Data Cleaning & EDA**

### Tools

`Python` | `Pandas` | `Jupyter Notebook`

---

⭐ **Thank you for visiting this project!**
