# National Power Outages Severity Analysis

---

## Contributors
- **Arya Verma**
- **Deepal Deleena**

---

## Introduction

### Dataset Overview
This project focuses on the **Power Outages** dataset, which contains information about major power outages in the U.S. spanning from January 2000 to July 2016. The dataset captures details about outage duration, causes, customer impact, and associated economic and demographic factors, making it a comprehensive resource for analysis.

### Research Question
What are the characteristics of the most severe power outages, and which factors (e.g., location, climate, outage cause) are most commonly associated with higher severity? Furthermore, can we develop predictive models to better understand and forecast these severe events?

### Why This Dataset Matters
Power outages significantly disrupt daily life, economic activities, and critical infrastructure. By analyzing historical data:
- Utility companies can better understand outage patterns.
- Policymakers can identify areas needing infrastructural improvements.
- Predictive models can help mitigate the impact of future outages.

This analysis contributes to improving grid resilience and ensuring equitable energy distribution.

### Dataset Summary
- **Total Rows**: 1,534  
- **Key Features**:
  - `OUTAGE.DURATION`: Duration of the power outage (in minutes).  
  - `DEMAND.LOSS.MW`: Power demand loss (in megawatts).  
  - `CAUSE.CATEGORY`: General category of the outage cause (e.g., Severe Weather, Equipment Fault).  
  - `NERC.REGION`: The regional electrical reliability organization.  
  - `CUSTOMERS.AFFECTED`: Number of customers impacted by each outage.  

---

## Data Cleaning and Exploratory Data Analysis (EDA)

## Data Cleaning

To prepare the dataset for analysis, several preprocessing steps were performed:

1. **Combining Date and Time Columns**:
   - Unified the `OUTAGE.START.DATE` and `OUTAGE.START.TIME` columns into a single `OUTAGE.START.DATE` column.
   - Similarly, combined `OUTAGE.RESTORATION.DATE` and `OUTAGE.RESTORATION.TIME` into `OUTAGE.RESTORATION.DATE`.
   - Dropped the original time columns after merging.

2. **Feature Engineering**:
   - Created a new column, `MEGAWATT.HOURS`, to measure the total energy impact of outages by multiplying `OUTAGE.DURATION` (in hours) with `DEMAND.LOSS.MW`.
   - Converted outage duration from minutes to hours for easier interpretation.

3. **Standardizing Month Information**:
   - Mapped month names to numerical values using a dictionary to facilitate sorting and filtering.

4. **Removing Unnecessary Columns**:
   - Dropped irrelevant columns like `OUTAGE.START.TIME` and `OUTAGE.RESTORATION.TIME` after processing.

### Key Improvements
The cleaned dataset now:
- Includes unified timestamp columns for outage start and restoration times.
- Features new metrics like `MEGAWATT.HOURS` for a better understanding of energy impact.
- Has a consistent structure, enabling more effective analysis.

This cleaned dataset serves as the foundation for the exploratory and predictive analysis in subsequent sections.

Glimpse of few rows and columns of the cleaned dataset:

| NERC.REGION | CAUSE.CATEGORY.DETAIL | CUSTOMERS.AFFECTED | OUTAGE.DURATION | DEMAND.LOSS.MW |
|-------------|------------------------|--------------------|-----------------|----------------|
| MRO         | vandalism             | NaN                | 135.0           | NaN            |
| RFC         | thunderstorm          | 48000.0            | 3000.0          | 10.0           |
| MRO         | NaN                   | 7000.0             | 32.0            | 15.0           |
| RFC         | Coal                  | NaN                | 108653.0        | NaN            |
| MRO         | Coal                  | NaN                | 8468.0          | NaN            |

---

## Exploratory Data Analysis (EDA)

### Univariate Analysis: Outages by NERC Region

This bar plot displays the distribution of power outages across various NERC (North American Electric Reliability Corporation) regions. The plot highlights the total number of outages reported in each region, showcasing regional differences in grid reliability and vulnerability.

---
### Key Observations:
1. **High Outage Counts in Specific Regions**:
   - The **WECC (Western Electricity Coordinating Council)** and **RFC (ReliabilityFirst Corporation)** regions report the highest number of outages, exceeding 400 incidents each. These regions cover vast areas with diverse climates and populations, likely contributing to the higher counts.

2. **Regional Variability**:
   - Moderate numbers of outages are observed in regions like **MRO (Midwest Reliability Organization)** and **SERC (Southeastern Electric Reliability Council)**.
   - Regions like **ASCC (Alaska Systems Coordinating Council)** and **FRCC (Florida Reliability Coordinating Council)** report relatively fewer outages, possibly due to smaller geographic coverage or effective mitigation efforts.

3. **Anomalies**:
   - Some regions, such as **HI (Hawaii)**, report negligible outages. This may reflect differences in infrastructure, unique geographic conditions, or limited reporting.

---

### Interpretation:
The uneven distribution of outages across regions suggests that certain geographic and climatic conditions, combined with infrastructural factors, may contribute to the reliability of the power grid. Further analysis could investigate the relationship between outages and factors like population density, weather patterns, or grid infrastructure quality.
<iframe
  src="assets/NERC.html"
  width="800"
  height="450"
  frameborder="0"
></iframe>

### Bivariate Analysis: Statewide Average Prices vs. Electricity Consumed

This scatter plot shows the relationship between **average monthly electricity prices (in cents per kilowatt-hour)** and **statewide electricity consumption (in megawatt-hours)**. Each point represents a state's electricity pricing and consumption data.

---

### Key Observations:
1. **Negative Association**:
   - The plot suggests a negative association between price and consumption. States with lower electricity prices tend to consume higher amounts of electricity, while higher electricity prices correspond to lower consumption.

2. **Clustered Consumption**:
   - Most states have electricity consumption below 20 million megawatt-hours, regardless of pricing.
   - A smaller subset of states exhibits exceptionally high consumption levels (above 30 million megawatt-hours), which are primarily observed at lower price points (below 10 cents per kWh).

3. **Outliers**:
   - A few points represent states with significantly high prices (above 20 cents per kWh) and very low consumption, possibly due to smaller populations or specific pricing policies.

---

### Interpretation
This analysis indicates that lower electricity prices may encourage higher consumption, aligning with economic principles of supply and demand. However, additional factors like state population, industrial presence, and climate likely contribute to this relationship. Further investigation through hypothesis testing or regression modeling could quantify these effects and identify causation.

<iframe
  src="assets/statewide_avg_price_vs_electricity_consumed.html"
  width="800"
  height="450"
  frameborder="0"
></iframe>


### Grouped Analysis: Outage Duration by Climate Category and State

This pivot table displays the **average power outage duration (in hours)** across U.S. states, categorized by climate conditions (`cold`, `normal`, `warm`).

---

### Key Insights:
1. **Cold Climates Lead to Longer Outages**:
   - States like **Arkansas** and **District of Columbia** show significantly higher outage durations in colder conditions, highlighting infrastructure vulnerabilities during extreme weather.

2. **Warm Climates Have Unique Challenges**:
   - **Arizona** exhibits very high outage durations under warm conditions, likely due to heat waves and increased energy demand.

3. **State-Specific Trends**:
   - States like **Florida** experience relatively higher outage durations under normal conditions compared to others.

| **CLIMATE.CATEGORY**     | **Cold**   | **Normal** | **Warm**    |
|--------------------------|-----------:|-----------:|------------:|
| **U.S. State**           |            |            |             |
| **Alabama**              | 2247.00    | 233.50     | 803.00      |
| **Arizona**              | 74.00      | 789.54     | 14741.29    |
| **Arkansas**             | 2538.14    | 556.20     | 3916.33     |
| **California**           | 1787.67    | 1273.50    | 2117.45     |
| **Colorado**             | 860.67     | 151.29     | 2243.50     |
| **Connecticut**          | 316.00     | 1193.80    | 4592.50     |
| **Delaware**             | 50.91      | 27.12      | 1510.67     |
| **District of Columbia** | 2076.80    | 5691.50    | 9886.00     |
| **Florida**              | 494.30     | 6109.00    | 3952.88     |
| **Georgia**              | 2256.00    | 1152.71    | 963.17      |

## Assessment of Missingness

---

#### NMAR Analysis

We hypothesize that the missingness in the `CAUSE.CATEGORY.DETAIL` column is **Not Missing At Random (NMAR)**. The missingness could result from inconsistent reporting practices by different utility companies or a lack of precise categorization for certain outage causes.

To confirm this, additional data, such as internal reporting standards or more detailed event logs from utility companies, would be needed. With this extra information, we could potentially conclude that the missingness is **Missing At Random (MAR)** if it's dependent on the reporting organization or another observable factor.

---

#### Missingness Dependency Analysis

We analyzed whether the missingness in the `CAUSE.CATEGORY.DETAIL` column depends on other variables in the dataset using permutation tests.

1. **Dependency on `CAUSE.CATEGORY`**:
   - The missingness in `CAUSE.CATEGORY.DETAIL` **does depend** on the `CAUSE.CATEGORY` column. The permutation test yielded a p-value of **0.0**, indicating a significant dependency. This relationship suggests that specific outage categories are more prone to missing details.

2. **No Dependency on `OUTAGE.DURATION`**:
   - The missingness in `CAUSE.CATEGORY.DETAIL` **does not depend** on the `OUTAGE.DURATION` column. The p-value of approximately **0.074** suggests no statistically significant relationship.

---

#### Key Results

1. **Empirical Distribution of Test Statistic**:
   - The observed test statistic for the dependency between `CAUSE.CATEGORY.DETAIL` and `CAUSE.CATEGORY` is **0.4**, which is more extreme than any randomly generated test statistics.
   - For `OUTAGE.DURATION`, the observed test statistic difference of means was approximately **-590.8**, with no significant deviation from the random distribution.

<iframe
  src="assets/mean.html"
  width="800"
  height="450"
  frameborder="0"
></iframe>


---

#### Interpretation

These results indicate that the missingness in `CAUSE.CATEGORY.DETAIL` is likely influenced by the `CAUSE.CATEGORY`, suggesting a **MAR mechanism**. However, no dependency was found with `OUTAGE.DURATION`. This exploration helps refine our understanding of missingness and guides further cleaning and analysis.

## Hypothesis Testing

**Question**: Does the average outage duration vary significantly across different NERC regions?

**Null Hypothesis (H₀)**: The average outage duration does not change based on the NERC region it occurs in.  
**Alternative Hypothesis (H₁)**: The average outage duration does change based on the NERC region it occurs in.

**Test Statistic**: Total Variation Distance (TVD), calculated as the absolute difference in mean outage duration across NERC regions.  
**Significance Level**: 0.05.

---

#### Results:

- The observed test statistic (TVD) was approximately **0.2254**.
- The resulting **p-value** was **0.223**, indicating that the observed difference in outage duration across NERC regions is not statistically significant at the 5% level.

---

#### Conclusion:

With a p-value of **0.223**, we fail to reject the null hypothesis. This suggests that there is insufficient evidence to conclude that outage duration varies significantly across NERC regions. However, further exploration with additional data might uncover more subtle trends.

---

## Framing a Prediction Problem

Our main goal is to **predict the severity of power outages** based on the `DEMAND.LOSS.MW` column of the dataset. The prediction problem we are addressing is a **classification problem**, specifically a **multiclass classification** task.

---

#### Problem Statement

We aim to classify the severity of power outages into discrete categories based on the magnitude of the `DEMAND.LOSS.MW` values. To achieve this:
1. The `DEMAND.LOSS.MW` column is divided into bins using `pd.qcut`, categorizing the values into **eight distinct levels of severity** (from 1 to 8).
2. Each bin represents a range of demand loss, allowing us to classify outages as "low severity" to "high severity" events.

---

#### Response Variable

- **Response Variable**: The severity level (from 1 to 8) based on the `DEMAND.LOSS.MW` column.
- **Reason for Choosing This Variable**: Predicting outage severity is crucial for prioritizing responses and allocating resources efficiently during power outages.

---

#### Evaluation Metric

- **Chosen Metric**: **Accuracy**  
  - **Reason**: Accuracy was selected as the metric since the goal is to evaluate how well the model predicts the correct severity class across all states. While alternative metrics like F1-score could handle class imbalances better, accuracy provides a straightforward measure of the model's overall performance in this context.

---

#### Justification for Features

- **Features Used for Prediction**:
  - `CAUSE.CATEGORY` (e.g., severe weather, equipment failure)
  - `NERC.REGION` (regional location of the outage)
  - `OUTAGE.DURATION` (duration of the outage in hours)
  - `CUSTOMERS.AFFECTED` (number of affected customers)

- **Justification**: These features are available at the **time of prediction** and are key indicators of the severity of an outage. No features that would be unavailable during the outage (e.g., post-event metrics) were used.

---

## Baseline Model

---

#### Model Description

For the baseline model, we built a **multiclass classification model** to predict the severity of power outages based on the `DEMAND.LOSS.MW` column, categorized into eight distinct levels of severity. The model was trained using a **Decision Tree Classifier** implemented in an **sklearn pipeline**.

---

#### Features Used

- **Quantitative Features**:
  - `OUTAGE.DURATION` (numerical)
  - `DEMAND.LOSS.MW` (numerical)
  - `MEGAWATT.HOURS` (numerical, derived feature)
  - `CUSTOMERS.AFFECTED` (numerical)

- **Categorical Features**:
  - `CLIMATE.REGION` (nominal, one-hot encoded)
  - `CAUSE.CATEGORY` (nominal, one-hot encoded)

- **Feature Engineering**:
  - One-hot encoding was applied to categorical columns (`CLIMATE.REGION`, `CAUSE.CATEGORY`) to transform them into numerical representations.
  - Quadratic combinations of numerical features were created to capture potential interactions between predictors.

---

#### Pipeline Implementation

All feature transformations (one-hot encoding, quadratic feature creation) and model training steps were implemented within an **sklearn pipeline** to ensure a seamless and reproducible workflow.

---

#### Model Performance

The performance of the baseline model was evaluated using **accuracy** as the metric on unseen test data. The accuracy score achieved by the baseline model was approximately **38.2%**.

- **Interpretation**:
  - While the model performs better than random guessing for this eight-class classification problem, there is significant room for improvement.
  - The baseline model serves as a foundation for identifying areas to refine feature selection, engineering, and model architecture in subsequent iterations.

---

#### Conclusion

This baseline model provides a starting point for the classification task. While its performance is modest, the systematic transformation of features and use of a pipeline lays the groundwork for a more robust and accurate final model in the next step.

---

## Final Model

---

#### Features Added and Their Relevance

In the final model, two new features were engineered in addition to the existing transformations from the baseline model:

- **Quadratic Interactions of Numerical Features**:
  - **Example**: Interaction terms like `IND.PRICE` × `COM.PRICE` were created to capture nonlinear relationships between numerical variables.
  - **Relevance**: These interactions allow the model to account for combined effects of multiple features that could influence power outage severity, such as the interplay between industrial and commercial energy pricing.

- **One-Hot Encoding of Additional Categorical Features**:
  - Features like `CLIMATE.CATEGORY` and `CAUSE.CATEGORY` were encoded to ensure their usability in the model.
  - **Relevance**: These categories provide critical information about the environment and causes of outages, which are directly tied to outage severity.

- **Quantile Transformation on `CUSTOMERS.AFFECTED`**:
  - This transformation normalized the distribution of `CUSTOMERS.AFFECTED` to reduce the influence of outliers.
  - **Relevance**: By normalizing, the model better captures patterns among typical outages, reducing noise caused by extreme values.

---

#### Modeling Algorithm and Pipeline

The final model used a **Random Forest Classifier** as the predictive algorithm. All preprocessing steps, including feature engineering, were integrated into a unified **sklearn pipeline**. The pipeline included:
- One-hot encoding for categorical variables.
- Quadratic feature generation for numerical variables.
- Normalization of heavily skewed features like `CUSTOMERS.AFFECTED`.

This streamlined implementation ensured reproducibility and avoided data leakage during training and evaluation.

---

#### Hyperparameter Tuning

A **GridSearchCV** approach was employed to optimize hyperparameters for the Random Forest Classifier. The following hyperparameters were tuned:
- **Number of estimators (`n_estimators`)**: Explored values of 105, 115, and 125 to determine the best ensemble size.
- **Maximum depth (`max_depth`)**: Ranged from 2 to 20 to balance overfitting and underfitting.
- **Minimum samples split (`min_samples_split`)**: Ranged from 2 to 10 to evaluate splits for leaf nodes.
- **Criterion**: Tested Gini impurity, entropy, and log loss to identify the best splitting criteria.
- **Maximum features (`max_features`)**: Evaluated options like square root, log2, and None.

The best parameters identified were:
- `n_estimators`: **125**
- `max_depth`: **10**
- `min_samples_split`: **2**
- `criterion`: **entropy**
- `max_features`: **None**

---

#### Final Model Performance

The final model was evaluated on unseen test data using **accuracy** as the performance metric. The results showed:
- **Baseline Model Accuracy**: **38.2%**
- **Final Model Accuracy**: **44.6%**

This represents a significant improvement of approximately **6.4 percentage points**, showcasing the impact of feature engineering and hyperparameter tuning.

---

#### Explanation of Improvement

The improvement in accuracy is attributed to:
- **Enhanced Feature Representation**: The inclusion of quadratic terms captured nonlinear interactions, which were not accounted for in the baseline model.
- **Hyperparameter Optimization**: GridSearchCV ensured the model was fine-tuned for optimal performance, avoiding both underfitting and overfitting.
- **Categorical Data Encoding**: Proper encoding of categorical features allowed the model to leverage all available data effectively.

---

### Fairness Analysis

#### Group Definitions:
- **Group X:** Outages with higher severity (five, six, seven, eight).
- **Group Y:** Outages with lower severity (one, two, three, four).

#### Evaluation Metric:
- **Prediction accuracy (CORRECT.PERCENT)** at the severity level.

#### Hypotheses:
- **Null Hypothesis (H₀):** The model is fair. The prediction accuracy for outages with high and low severity is roughly the same, and any observed differences are due to random chance.
- **Alternative Hypothesis (H₁):** The model is unfair. The prediction accuracy for outages with high and low severity is significantly different.

#### Test Statistic:
- The difference in mean prediction accuracy (CORRECT.PERCENT) between Group X and Group Y.

#### Significance Level:
- **0.05**

#### Methodology:
1. **Grouping:** The outages were split into two groups based on the severity of outages (binned `DEMAND.LOSS.MW`).
2. **Permutation Test:** 
   - The test statistic was calculated as the absolute difference in mean accuracy (CORRECT.PERCENT) between Group X and Group Y.
   - The observed test statistic was compared to a distribution of test statistics generated by randomly shuffling the group labels (`DEMAND.LOSS.MEGAWATT`) 10,000 times.

#### Results:
- **Observed Test Statistic:** The observed difference in mean prediction accuracy between the two groups was approximately **0.08**.
- **p-value:** The permutation test yielded a p-value of **0.0081**.

#### Conclusion:
- **Decision:** Since the p-value (0.0081) is less than the significance level (0.05), we reject the null hypothesis.
- **Interpretation:** The model’s prediction accuracy is significantly different for high-severity outages (Group X) compared to low-severity outages (Group Y). This indicates potential unfairness in the model’s performance, with high-severity outages being at a disadvantage.




