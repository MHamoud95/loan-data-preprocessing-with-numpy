# Loan Data Preprocessing Project

This project is a comprehensive data preprocessing pipeline designed to clean and transform loan datasets for analysis. The dataset contains both numeric and categorical data, including loan status, amounts, interest rates, and more. The goal is to handle missing values, encode categorical variables, and perform data transformations to produce a clean dataset ready for statistical or machine learning tasks.

---

## Description of the Process

### 1. Importing Data and Configuration
We start by importing the required libraries, primarily `numpy`, and configuring it to:
- Suppress scientific notation for better readability.
- Extend line width and set precision to display numbers cleanly.

The raw data is loaded using `numpy.genfromtxt` with necessary parameters to handle delimiters, encoding, and missing values.

---

### 2. Handling Missing Data
A key step in preprocessing is managing missing values:
- **Detection:** Missing values are identified using `np.isnan` and summarized for analysis.
- **Temporary Fillers:** Missing values are temporarily replaced with `max + 1` to ensure they don't overlap with valid data.
- **Imputation:** Depending on the context, missing values are filled with:
  - Mean values for numerical columns.
  - Maximum values for risk-related features like loan amount and interest rate.

---

### 3. Separating String and Numeric Columns
To handle mixed data types:
- **String Columns:** Extracted separately for operations like encoding, stripping unwanted text, and categorization.
- **Numeric Columns:** Processed for imputation, normalization, and restructuring.

---

### 4. Manipulating String Columns
Several transformations are applied:
- **Issue Date:** Months are converted into numeric values, and missing dates are handled appropriately.
- **Loan Status:** Categorized into binary values: `0` for bad loans (e.g., default, late) and `1` for good loans.
- **Term:** Text like "36 months" is stripped to numeric values.
- **Subgrades:** Missing subgrades are inferred from grades, and the grade column is removed as it's redundant.
- **State Address:** States are grouped into regions (West, South, Midwest, East) based on census data.

---

### 5. Manipulating Numeric Columns
Numeric columns undergo:
- **Imputation:** Missing values are filled using statistics derived from the data.
- **Currency Conversion:** Exchange rates are applied to convert USD amounts into EUR. This involves:
  - Reading exchange rates from an external file.
  - Mapping rates to each loan based on the issue date.
  - Adding new columns for EUR values while preserving original USD values.
- **Interest Rate Adjustment:** Converted from percentage form (e.g., 13%) into decimals (e.g., 0.13).

---

### 6. Merging and Sorting the Dataset
Once both string and numeric datasets are processed:
- They are merged into a single unified dataset.
- The dataset is sorted by the loan ID column to ensure consistency.

---

### 7. Storing the Preprocessed Dataset
The final dataset, along with its headers, is saved as a `.csv` file named `loan-data-preprocessed.csv`. This file is ready for use in further analysis, modeling, or reporting.

---

## Key Features
- Comprehensive handling of missing values using domain-relevant techniques.
- Efficient encoding of categorical data for machine learning compatibility.
- Integration of external exchange rate data to enhance dataset value.
- Modular design with checkpointing for debugging and intermediate validation.

---

## How to Use
1. Place the raw dataset (`loan-data.csv`) and the exchange rate file (`EUR-USD.csv`) in the project directory.
2. Run the script in a Python environment:
   ```bash
   python preprocessing.py

  add link 
