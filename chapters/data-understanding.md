# Data Understanding
### CRISP-DM: Data Understanding:
- Collect initial data;
- Describe data;
- Explore data;
- Verify data quality.

### CRISP-DM: Data Preparation:
- Describe data set;
- Select data;
- Clean data;
- Construct data;
- Integrate data;
- Format data.

## Data Summarisation
### Motivation:
Data summaries provide overviews of key properties of big data sets, help selecting the most suitable tool for the analysis and describe important properties of the distribution of the values.

### Types of Summaries:
- What is the "most common value"?
- What is the "variability" in the values?
- Are there "strange"/unexpected values in the data set?

### Data set:
- Univariate data;
- Multivariate data.

### Variables:
- Categorical variables;
    - Mode: most frequent value;
    - Frequency Table: frequency of each value (absolute or relative);
    - Contingency Tables: cross-frequency of values for two variables;
- Numeric variables.
    - Statistics of location:
        - Mode: most frequent value;
        - Mean: sensitive to extreme values;
        - Median: 50<sup>th</sup>-percentile;
    - Statistics of variability or dispersion:
        - Range: max - min;
        - Variance: sensitive to extreme values;
        - Standard Deviation: sensitive to extreme values;
        - Inter-Quartile Range (IQR): difference between 3<sup>rd</sup> and 1<sup>st</sup> quartiles (Q<sub>3</sub> - Q<sub>1</sub>);
            - **Note:** for a numeric variable, an outlier can be an extreme value. In the presence of such values, median or mode are more robust as a central tendency statistic and IQR is more appropriate as variability statistic;
            - Boxplot definition: any value outside the interval [Q<sub>1</sub> - 1.5 IRQ, Q<sub>3</sub> + 1.5 IRQ];
    - Multivariate analysis of variability or dispersion:
        - Covariance Matrix: variance between every pair of numeric variables (the value depends on the magnitude of the variable);
        - Correlation Matrix: correlation between every pair of numeric variables (the influence of magnitude is removed);
        - Pearson Correlation Coefficient ($\rho$): measures linear correlation between two variables ($\rho$ = 0 if not correlated, 0 < |$\rho$| < 1, if correlated but not linear, |$\rho$| = 1 if linear correlation, negative or positive depends on the slope);
        - Spearman Rank-Order Correlation Coefficient: measures the strength and direction of monotonic association between two variables (relation can be non-linear but monotonic, this takes into consideration only the order, not the proportion).

## Data Visualisation
### Motivation:
Data visualisation methods by humans help detecting patterns and trends, as well as outliers and unusual patterns.

### Main types of graphs:
- Univariate graphs
    - Categorical variables
        - **Barplots:** set of values as heights of bars (e.g. frequency of occurrence of different values);
        - **Piecharts:** same purpose as barplots in the form of a pie, not as good for comparison.
    - Numeric variables
        - **Line plots:** evolution of values of a continuous variable, frequently used to deal with the notion of time (x-axis, with equal lag between observations);
        - **Histograms:** distribution of values of a continuous variable, divided into a set of bins;
            - May be misleading in small data sets, since its shape depends on the number of bins;
            - Some of the problems of histograms can be tackled by smoothing the estimates of the distribution (e.g. kernel density estimates - estimate of the distribution by smoothly averaging other neighbouring points).
        - **Cumulative Distribution Function (CDF):** cumulative distribution of a variable (F<sub>X</sub>(x) = P(X $\le$ x));
        - **QQ plots:** comparison of two distributions by different properties (e.g. location, scale, skewness), can be used to visually check the hypothesis that a variable follows a normal distribution (comparing it against the normal distribution);
        - **Boxplots:** summary of a variable distribution, show IQR and outliers (if any).
- Bivariate graphs
    - **Scatterplots:** the natural graph for showing the relationship between a pair of numeric variables;
- Multivariate graphs
    - **Scatterplots:** relationship between every pair of numeric variables and respective groups;
    - **Parallel coordinates plots:** attribute values for each case (represented as a line), the order can be important to help identifying groups;
    - **Correlogram:** chart of correlation statistics (e.g. Pearson) for each pair of variables;
- Conditioned graphs
    - Datasets frequently have categorical variables, which values can be used to create subgroups of the data (e.g. subroup of male clients of a company);
    - Conditioned plots allow the simultaneous presentation of these subgroup graphs to better allow finding eventual differences between the subgroups (e.g. conditioned histograms, conditioned boxplots)

## Data Preparation
Set of steps that may be necessary to carry out before any further analysis takes place on the available data.
- Data can come from different sources;
- Data sets may have unknown variable values;
- Many data mining methods are sensitive to variable scales and/or types;
- Data sets can be too large for some methods to be applicable;
- "Creating" new variables may be needed to achieve objectives;
    - Relative values (variations) may be more interesting than absolute;
    - Domain-specific mathematical relationship between variables may be important for the task.

### Feature extraction:
Extracting features from raw data on which analysis can be performed. It is very application-specific and a very crucial step (e.g. image data: very high-dimensional data that can be represented by pixels, color histograms, etc.).

### Data cleaning:
Data may be hard to read or require extra parsing efforts.
- **Handling missing values:**
    - Remove all cases in a data set;
    - Fill unknowns with imputation of the most common value (general or on the cases more "similar" to them);
    - Fill with linear interpolation of nearby values in time/space;
    - Explore eventual correlations between variables;
    - Do nothing if robust with missing values.
- **Handling incorrect values:**
    - Inconsistency detection;
    - Domain knowledge;
    - Data-centric methods.

### Data transformation:
Map entire set of values of a given attribute to a new set of replacement values such that each old value can be identified with one of the new value.
- Common strategies:
    - **Normalisation:**
        - Min-max scaling (range-based): transform into values in the range [0, 1] (not robust with outliers);
        - Standardization: values are rescaled based on the mean and standard deviation, usually lying in the range [-3, 3], under a normal distribution assumption;
    - **Case dependencies:** In time series it is common to use different techniques (e.g. adjust mean, variance, range, remove unwanted common signal);
    - **Binarisation/one-hot encoding:** some data mining methods can only handle numeric atributes;
        - Binarisation: if the attribute has only 2 possible nominal values, it can be transformed into a binary attribute;
        - One-hot encoding: if the attribute has k possible values, it can be transformed into k binary attributes.
    - **Discretisation:** conversion of a continuous attribute into ordinal attribute of numeric variables;
        - Equal-width: divides into equal-width ranges (may be affected by the presence of outliers);
        - Equal-frequency: divides to put the same number of values in each range (can generate very different amplitudes).

### Feature engineering:
Using domain knowledge to create features that can capture important information more efficiently than the original ones, to help solve the problem.
- Express known relationship between existing variables (e.g. create ratios/proportions like credit card sales per person);
- Overcome limitations of some data mining tools (some tools shuffle the cases or are unable to use the information about their dependencies; can be handled by constraining to tools that handle them or create variables that express the dependencies).

In time series, it's common to create features to represent relative values instead of absolute; other common technique is Time Delay Embedding.

Create variables whose values are the value of the same variable in previous time steps (if we have variables whose values are as such, standard tools will be able to model time relationships with these embeddings).

### Data and dimensionality reduction:
May be needed to make modelling possible.

### [< Go back](/README.md)