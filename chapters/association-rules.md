# Association Rules
## Motivation
Originated in the context of Market Basket Analysis:
- Data consists of set of items bought by costumers, referred to as transactions;
- Find unexpected associations between sets of items using the frequency of sets of items;
- Discovered sets of items are referred to as frequent itemsets or frequent patterns.

## Actionable Knowledge
### Shop layout:
Possible actions from rule {A1, A4} $\to$ {A6}:
- Sell the A1, A4, A6 together (pack);
- Place article A6 next to A1 and A4;
- Offer discount coupon for A6 in articles A1, A4;
- Place a competitor of A6 next to A1, A4 (brand protection).

### Cross selling:
- Client puts article A in basket;
- Shop knows A $\to$ B;
- Rule has enough confidence (> 20%);
- Shop tells client he may be interested in B;
- Client decides whether to buy B or not.

### Text mining:
- Each document is treated as a bag of terms and keywords;
- Goal: identify co-occurring terms and keywords;
- Example:
    - Student, School $\to$ Education;
    - Game $\to$ Sport.

### Health:
- Rules obtained from patient's records allow sooner prevention;
- Record observations for each visit from a patient (symptoms and exam results);
- A set of observations may fire a rule;
- Not necessarily causal.

### Web usage analysis:
- Usage patterns:
    - Most visited pages;
    - Frequent page sets (site structure);
    - Pages associated to users (personalisation);
    - Seasonal effects (operations, campaigns);
    - Cross-preferences (cross-selling).

## Association rules basic concepts
- **Support:** measures the importance of a set (percentage/number of transactions t containing the set S);
- **Confidence:** measures the strength of a rule (percentage of transactions t that having the set A also have B);

## Mining association rules
- Given:
    - Dataset of transactions D;
    - Minimal support minsup;
    - Minimal confidence minconf.
- Obtain:
    - All association rules X $\to$ Y such that sup $\ge$ minsup and conf $\ge$ minconf.

### Apriori algorithm:
1. Frequent itemset generation (itemsets with sup $\ge$ minsup);
2. Rule generation (generate all confident association rules from the frequent itemsets, i.e. rules with conf $\ge$ minconf).
- Problem: there is a large number of candidate frequent itemsets;
- Downward closure property: every subset of a frequent itemset must also be frequent, thus every superset of an infrequent itemset is also infrequent;
- Apriori pruning principle: if an itemset is below the minimal support, discard all its supersets.

### Step 1 - Identifying frequent itemsets:
- Candidate generation (self-join step): generates new candidate k-itemsets based on the frequent (k-1)-itemsets found in the previous iteration;
- Candidate pruning (prune step): eliminates some of the candidate k-itemsets using support-based pruning.

### Step 2 - Rule generation:
- Generate all non-empty subsets s of each frequent itemset I;
- For each subset s, compute the confidence of the rule (I-s) $\to$ s;
- Select rules with conf $\ge$ minconf;
- **Note:** moving items from the antecedent to the consequent never changes support and never increases confidence.

Number of DB scans is n if the size of the largest frequent set is n or n-1.

### Compact representation of itemsets:
- The number of frequent itemsets can be very large;
- It is useful to identify a small representative set of itemsets from which all other frequent itemsets can be derived:
    - Maximal;
        - **Maximal frequent itemset:** frequent itemset for which none of its supersets is frequent.
        - Can derive all frequent itemsets by computing all non-empty intersections;
    - Closed.
        - **Closed frequent itemset:** frequent itemset that has no frequent supersets with the same support.
        - Preserve the knowledge about the support values of all frequent itemsets.

### Rule number reduction:
- Change parameters (minsup, minconf);
- Restrict items (which items are relevant);
- Summarisation techniques (represent subsets of rules by a single representative rule);
- Filter rules (improvement, measures of interest).

### Improvement:
Minimum difference between its confidence and the confidence of any of its immediate simplifications.

### Interesting rule:
- Unexpected (surprising to the user - measure: deviation from expected);
- Useful (actionable - measure: estimated benefit);
- Subjective measures (based on user's belief in the data);
- Objective measures (based on facts, statistics and structures of patterns, independent of domain);
- Typically, A $\to$ B is interesting if A and B are not statistically independent (may have high sup and conf and still not be interesting).

### Lift:
Lift is the ratio between confidence of the rule and support of the itemset appearing in the consequent,measures deviation from a rule regarding the statistical independence between antecedent and consequent:
- lift = 1: A and B are independent;
- lift < 1: A and B are negatively correlated;
- lift > 1: A and B are positively correlated.

### Conviction:
Lift measures co-occurrence only, not implication. Conviction tackles that, being sensitive to rule direction. Conviction of a rule A $\to$ B is the ratio between the expected frequency that A occurs without B, if independent, and the observed frequency that the rule makes of incorrect predictions.
- High conviction means that the consequent depends strongly on the antecedent.

### Improving Apriori
- Challenges of frequent pattern mining:
    - multiple scans of transaction database;
    - huge number of candidates;
    - tedious workload of support counting for candidates.
- Ideas:
    - Reduce number of database scans and candidates;
    - Facilitate support counting of candidates.
- Some methods that improve Apriori's efficiency:
    - Partitioning;
    - Sampling;
    - Dynamic Itemset Counting;
    - Frequent Pattern Projection and Growth.

### [< Go back](/README.md)