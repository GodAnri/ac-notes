# Advanced Issues in Data Preparation and Modelling
## Data Reduction
Obtain a reduced representation of the data set that is much smaller in volume, but:
- Produces (almost) the same analytical results;
- Improves visualisation of data;
- Creates more interpretable models;
- Achieves higher efficiency.

### Dimensionality:
- When dimensionality increases, data becomes more sparse;
- Density and distance between points, which is critical for clustering and outlier analysis, becomes less meaningful;
- Possible combinations of subspaces grow exponentially;
- Number of data points required for robust patterns grows exponentially with the number of attributes.

### Attribute aggregation:
- Principal Component Analysis (PCA):
    - n new features;
    - Linear combinations of existing n attributes orthogonal to each other;
    - k << n (a much smaller number of attributes) explains most of the variance in the data.
- Independent Component Analysis (ICA) vs. PCA:
    - Both create linear combinations of the attributes;
    - ICA assumes the original attributes are statistically independent, reduces higher order statistics (e.g. kurtosis) and does not rank components.
- Multidimensional scaling:
    - Linear projection of a data set;
    - Uses the distances between pairs of objects (not the values of the attributes);
    - Particularly suitable when it is difficult to extract relevant features to represent the objects.

### Feature selection
- Eliminate:
    - Redundant attributes (duplicate information from one or more other attributes);
    - Irrelevant attributes (contain no useful information).
- Filter methods:
    - 2 attributes: remove redundant attributes;
    - 1 attribute vs. target: identify relevant variables.

## Modelling
### Dealing with unbalanced classes:
- Collect more data (difficult in many domains);
- Resample existing data (delete data from the majority class and duplicate from the minority);
    - Possible loss of information (from deletion);
    - Possible fixed boundaries;
    - Danger of overfitting.
- Create synthetic data (e.g. SMOTE - Synthetic Minority Oversampling Technique);
    - Possible inadequate boundaries (e.g. if minority observations are too far apart);
    - Danger of overfitting.
- Adapt learning algorithm (e.g. cost sensitive learning).

### Cost of errors:
False Positive and False Negative errors often incur different costs depending on the domain, but ML methods still usually minimise FP + FN. Misclassification costs can be set, so that FP can have more influence than FN, or vice-versa (e.g. unnecessary suffering from an undiagnosed illness should have a higher misclassification cost than unnecessary exams).

### Cost-sensitive learning:
- Simple methods:
    - Resampling according to costs;
    - Weighting according to costs.
- Complex methods:
    - **Metacost** (independent of algorithm):
        - Create bootstrap replicates of training data;
        - Learn model from each replicate;
        - Relabel examples;
        - Learn model on relabelled data.

## Data quality: multidimensional view
- Accuracy: correct or wrong, accurate or not;
- Completeness: not recorded, unavailable;
- Consistency: some modified but some not, dangling;
- Timeliness: timely update;
- Believability: trustable data/sources;
- Interpretability: understandable data.

### "Clean" data:
- Data warehouse:
    - DWs are tipically built with a descriptive, aggregated data purpose.
- IS revamp:
    - How far was analytics taken into account?
- Major data cleanup:
    - How was project success measured?
- Automatic data collection:
    - Machines can break.
- Human-error proof:
    - Data errors always find a way.
- Everything that you need:
    - If anything goes wrong it's the data scientists' fault.

### Improvements
- Human resources;
- Analytics at the core of IS development;
    - Requirements analysis includes analytics;
    - Analytics components built in the same process as the rest of the functionalities;
- Data quality is a continuous process.
    - Discrepancy detection;
    - Migration and integration.

### [< Go back](/README.md)