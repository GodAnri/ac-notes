# Descriptive Modelling
## Descriptive Analytics
Describing/summarising or finding structure on what's observed. Data summarisation and visualisation (e.g. PCA) can be seen as simple forms of descriptive analytics; however, descriptive modelling is most frequently associated with clustering.

### Similarity measures:
- The notion of similarity is strongly related with the notion of distance between observations;
- Similarity often falls in the range [0, 1], being higher the more alike two data objects are;
- Dissimilarity often has a lower bound at 0, but the upper limit varies;
- Similarity/dissimilarity can be expressed by a distance metric, so it follows the triangle inequality;
    - Euclidean distance;
    - Manhattan distance;
    - Generalisation: Minkowski distance (Manhattan for p=1, Euclidean for p=2, ..., Chebyschev - or supremum - distance for p = $\infin$: maximum difference between any of the attributes).
- Several problems may arise that may distort the notion of distance:
    - Different scales of variables;
    - Different importance of variables;
    - Different types of data (e.g. numeric and categorical).
- Heterogeneous Distance Functions: if categorical, 0 if equal, 1 otherwise; if numeric, normalised difference;
- General Coefficient of Similarity: weights for each attribute.

## Clustering
Obtaining "natural" grouping of a set of data, i.e. find some structure on that data set (using the notion of similarity) and providing some abstraction of the found groups, gaining novel insights of data.

### Applications:
- Biology (describe organism communities and group genes or proteins);
- Business and Marketing (describe market segments and group stocks with similar fluctuations);
- Web Mining (find groups of related documents, find communities in social networks and build recommender systems).

### Partitional clustering:
Divide in k partitions according to a criterion
- Issues:
    - The user needs to select number of groups;
    - The number of possible divisions can grow fast;
- Properties:
    - Compactness: how similar cases are within the same cluster;
    - Separation: how far clusters are from each other;

The goal is to minimise intra-cluster distance and maximise inter-cluster distance.

Centroid: median of all data objects; the goal is to minimise the distance of the objects in a cluster to its centroid;

Hard clustering: an object belongs to a single cluster.

Fuzzy clustering: each object has a probability to belong to each cluster;

- **K-means algorithm:**
    - Initialise the centers of the k groups to a set of randomly chosen observations;
    - Repeat, allocating each observation to the group whose center is nearest and recalculating the center of each group;
    - Stop when the groups are stable (no significant decrease or increase on the minimise criterion);
    - It uses the squared Euclidean distance as criterion and maximises inter-cluster dissimilarity;
    - Advantages: fast algorithm, scalable, tends to identify local minima;
    - Disadvantages: not optimal, solution depends on starting point, initial guess of k (number of clusters) may be far from optimal.

### Validation:
- **Supervised:** compare the obtained clustering with the external information that we have available;
- **Unsupervised:** try to measure the quality without any information on its "ideal" structure.
    - Cohesion coefficients: determine how compact/cohesive the members of a group are;
    - Separation coefficients: determine how different are the members of different groups.
    - Example: Silhouette coefficient
        - Incorporates both cohesion and separation;
        - Uses average distance to all objects in the same group and minimum value for all other groups of the average distance to the members of that group;
        - Takes values between -1 and 1, close to 1 = well clustered, 0 = between two clusters, <0 = probably wrong cluster.
- To choose the best k for k-means:
    - Start with $\sqrt(N/2)$ if no a-priori value is known;
    - Solution: Calculate the average silhouette coefficient value and choose k that yields the highest value.
    - Other solution (Elbow method): calculate within-cluster sum of squared errors (SSE), also called distortion, and choose the k so that adding another cluster doesn't yield a much smaller SSE.

### Other partitional clustering methods:
- PAM (Partitioning Around Medoids):
    - Works similarly to k-means;
    - More robust to outliers: instead of averages, it uses the original objects as centroids;
    - More robust measure of quality: based on absolute error instead of squared error.
- CLARA (Clustering Large Applications):
    - PAM's advantages come at the price of additional computational complexity (not very scalable);
    - CLARA samples instead of using the full set, to solve efficiency problems.
- DBSCAN (Density-Based Spatial Clustering of Applications with Noise):
    - "K-means-like" methods have a problem with outliers, noise, or clusters with different sizes, densities or non-globular shape;
    - The density of a single observation is estimated by the number of observations within a certain radius;
    - Core points (number of observations within its radius is above a certain threshold), border points (within the radius of a core point) and noise points (not close enough to any core point);
    - Does not require the user to specify the number of groups, but the radius and minimum number of points have to be specified;
    - Border points inside the radius of multiple core points are allocated to the group of the nearest one;
    - Can handle clusters with different shapes/sizes and is resistant to noise, but has varying densities and high-dimensional data.

### Hierarchical clustering:
Obtain a hierarchy of groups where each level represents a possible solution with x groups; can be visualised using a dendogram.
- Agglomerative methods (bottom-up): start with one group per case and, on each upper level, merge the pair of groups that are more similar;
    - Compute proximity matrix, merge closest clusters, update proximity matrix, repeat until only one cluster remains.
- Divisive methods (top-down): start with a single group and, on each level, split the group with smallest uniformity in two;
    - Compute proximity matrix, split cluster with largest diameter, select the data point with largest average dissimilarity to the other members in that cluster and reallocate the data to either the cluster of this selected point or the "old" cluster, repeat until each data point constitutes a cluster.
- Some measures for merging/splitting:
    - single link (shortest distance);
    - complete link (maximum distance);
    - average link;
    - distance between centroids;
    - Ward's method (uses SSE).
- Different measures yield different types of clusters:
    - single link: can handle non-elliptical shapes, uses a local merge criterion (distant parts of the clusters and their structure are not taken into account);
    - complete link: biased towards globular clusters, uses a non-local merge criterion, chooses most dissimilar members of the pair of clusters with smallest diameter, is sensitive to noise/outliers.