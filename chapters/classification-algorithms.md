# Classification: Algorithms
## Linear Classifier
- Uses a linear function to divide each set into two subsets;
- For 3+ classes: fit N-1 lines (N classes).

## Nearest Neighbour Classifier
- If the nearest instance to the previously unseen one is of class A, its class is also A, otherwise it is B.
- Decision surface of a NN classifier (also called Theissen regions) are implicit and divide the space into regions "belonging" to each instance and corresponding class.

### KNN Algorithm:
- Generalisation of the nearest neighbour algorithm;
- Find k NN, each representing a vote;
- An odd number is usually chosen for k;
- Most voted is the class of the instance.

### Sensitivity to Irrelevant Attributes:
- Using more attributes can sometimes lead to getting the wrong classification for an instance, when using less gave the right one;
- Nevertheless, using some subsets can also lead to wrong classifications.

### Advantages:
- Simple implementation;
- Handling of correlated features (arbitrary class shapes);
- Defined for any distance measure;
- Trivial handling of streaming data.

### Disadvantages:
- Very sensitive to irrelevant attributes;
- Slow classification for large datasets;
- Works best for real-valued datasets.

## Decision Trees
### Avoid overfitting:
- Prepruning: halt tree construction early (don't split node if this results in the goodness measure falling below a threshold);
- Postpruning: get a sequence of progressively pruned trees and use a set of data different from the training data to decide which is the "best pruned tree".

### Advantages:
- Easy to understand;
- Easy to generate rules.

### Disadvantages:
- Overfitting;
- Does not handle correlated features very well (rectangular partitioning);
- Can be quite large (pruning is necessary).

## Bayes Classifiers
Bayesian classifiers use Bayes Theorem, which says that:
- The probability of an instance being in a certain class is the probability of that instance being generated by that class times the probability of occurence of that class, divided by the probability of that instance existing.
- Assuming independent distributions, the probability of a certain class generating the instance is the multiplication of the probability of that class generating the observed value for each of the features of that instance.

### Advantages:
- Fast to train and classify;
- Not sensitive to irrelevant features;
- Handles real and discrete data;
- Handles streaming data well.

### Disadvantages:
- Assumes independence of features.

## Neural Network Learning
- Set of connected neurons (input and output) with weights;
- Supervised learning adjusts weights to ensure outputs are the expected ones to give inputs;
- Predicting: feed input values, collect outputs.

### Advantages:
- Fits any continuous activation function;
- Output may be one or more discrete and real values;
- Application and learning are intertwined;
- Robust to errors and noisy data;
- Fast application to new examples;
- Parallel.

### Disadvantages:
- Slow training;
- Low usability, empirical parameter tuning and network topology and learning rate;
- Low interpretability of the weights;
- Low adaptability to domain knowledge.

## Support Vector Machines (SVM)
- Linear learning machines with maximisation of margin (better separation between classes);
    - Hyperplane farthest from both classes has less risk of overfitting.
- Higher robustness to the curse of dimensionality;
- For non-linear functions, map attributes to space where linear discrimination is possible.

### SVM for Regression:
- Minimise the tube "around" the data;
- Instead of maximising the distance to closest examples from each class.