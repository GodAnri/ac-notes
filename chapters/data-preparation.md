# Data Preparation
The majority of time taken by any DM project is spent in data preparation.

## Data
Data is a collection of data objects (cases) and their attributes (features).

- **Attribute:** a property or characteristic of an object;
- **Object:** a collection of attributes;

It can be structured (e.g. data table) or non-structured (e.g. text).

It can have dependency or non-dependency between objects (e.g. time, space).
- Dependency-oriented data: implicit or explicit relationship between cases (e.g. time series, discrete sequences)
- Non-dependency-oriented data: no dependencies between cases (e.g. simple data tables, text)

### Types of Attributes:
- Categorical/qualitative
    - Nominal: there is no relationship between the values (e.g. name, gender, patient id);
    - Ordinal: there is an order, but no mathematical operations can be performed (e.g. size $\in$ {small, medium, large});
- Numeric/quantitative
    - Discrete: finite or countably infinite set of values for which differences are meaningful (e.g. temperatures, calendar dates);
    - Continuous: infinite set of values that represent the absolute numbers (e.g. number of visits to the hospital, distance, income).

### Data Characteristics:
- Dimensionality (number of attributes): high dimensional data brings several challenges;
- Sparsity: presence attributes;
- Resolution: patterns depend on the scale;
- Size: type of analysis may depend on it.

## Data Preparation
Tipically, data analysis tasks use datasets in tabular format (bidimensional structure).

### Data Wrangling:
Process of transforming and mapping "raw" data into a format appropriate for analytics.

Steps: discovering, structuring, cleaning, enriching, validating, publishing.

Goal: attain quality and useful data.

## Data Quality
The raw format of real data is usually widely variable as values may be missing, inconsistent across different data sources or erroneous, which poses several challenges to the effective data analysis.

Example: a classification model for predicting a client's loan risks is built using poor data.
- Credit-worthy candidates are denied loans;
- Loans are given to individuals that default.

### Data Quality Problems:
- **Noise:** irrelevant or useless information, that can be caused by incorrect or distorted measurements or variability of the domain;
- **Outliers:** data objects with considerably different characteristics from most of the others in the data sets - can be the goal of our analysis (e.g. intrusion detection, credit card fraud);
- **Missing values:**
    - Missing completely at random (MCAR): independent of observed and unobserved data, nothing systematic about it (e.g. a lab value because a lab sample was processed improperly);
    - Missing at random (MAR): related to observed data, not to unobserved, there may be something systematic about it (e.g. missing income value depending on age);
    - Missing not at random (MNAR): related to unobserved data of the variable itself, informative/non-ignorable missingness (e.g. someone did not enter their weight in a survey);
    - **Solutions:**
        - remove observations with missing values (critical if there are meaningful observations with missing values);
        - ignore missing values in the analytical phase (use methods that are inherently designed to work robustly despite missing values);
        - make estimates to fill the missing values - **imputation** (the most common value (e.g. mean, mode), based on other attributes, more sophisticated methods, etc.) - it might introduce bias in data and affect the results.
- **Duplicates:** data objects with the same data or almost the same data (e.g. same person with multiple email addresses), major issue when merging data from heterogeneous sources, it is necessary to deal with duplicate data (deleting it or not);
- **Inconsistent or incorrect data:** hardest issue to detect, may depend on expert domain knowledge (e.g. 4/11/2000 - 4 Nov. or 11 Apr., city called Shanghai in the United States).

### [< Go back](/)