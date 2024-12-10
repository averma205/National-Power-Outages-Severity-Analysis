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

### Exploratory Data Analysis (EDA)

## Univariate Analysis: Outages by NERC Region
This bar plot displays the distribution of power outages across various NERC (North American Electric Reliability Corporation) regions. The plot highlights the total number of outages reported in each region, showcasing regional differences in grid reliability and vulnerability.

---

## Key Observations:

1. **High Outage Counts in Specific Regions**:
   - The **WECC (Western Electricity Coordinating Council)** and **RFC (ReliabilityFirst Corporation)** regions report the highest number of outages, exceeding 400 incidents each. These regions cover vast areas with diverse climates and populations, likely contributing to the higher counts.

2. **Regional Variability**:
   - Moderate numbers of outages are observed in regions like **MRO (Midwest Reliability Organization)** and **SERC (Southeastern Electric Reliability Council)**.
   - Regions like **ASCC (Alaska Systems Coordinating Council)** and **FRCC (Florida Reliability Coordinating Council)** report relatively fewer outages, possibly due to smaller geographic coverage or effective mitigation efforts.

3. **Anomalies**:
   - Some regions, such as **HI (Hawaii)**, report negligible outages. This may reflect differences in infrastructure, unique geographic conditions, or limited reporting.

---

## Interpretation:

The uneven distribution of outages across regions suggests that certain geographic and climatic conditions, combined with infrastructural factors, may contribute to the reliability of the power grid. Further analysis could investigate the relationship between outages and factors like population density, weather patterns, or grid infrastructure quality.
<iframe
  src="assets/NERC.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Bivariate Analysis: Statewide Average Prices vs. Electricity Consumed

This scatter plot shows the relationship between **average monthly electricity prices (in cents per kilowatt-hour)** and **statewide electricity consumption (in megawatt-hours)**. Each point represents a state's electricity pricing and consumption data.

---

## Key Observations:
1. **Negative Association**:
   - The plot suggests a negative association between price and consumption. States with lower electricity prices tend to consume higher amounts of electricity, while higher electricity prices correspond to lower consumption.

2. **Clustered Consumption**:
   - Most states have electricity consumption below 20 million megawatt-hours, regardless of pricing.
   - A smaller subset of states exhibits exceptionally high consumption levels (above 30 million megawatt-hours), which are primarily observed at lower price points (below 10 cents per kWh).

3. **Outliers**:
   - A few points represent states with significantly high prices (above 20 cents per kWh) and very low consumption, possibly due to smaller populations or specific pricing policies.

---

## Interpretation
This analysis indicates that lower electricity prices may encourage higher consumption, aligning with economic principles of supply and demand. However, additional factors like state population, industrial presence, and climate likely contribute to this relationship. Further investigation through hypothesis testing or regression modeling could quantify these effects and identify causation.

<iframe
  src="assets/statewide_avg_price_vs_electricity_consumed.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


### Grouped Analysis: Outage Duration by Climate Category and State

This pivot table displays the **average power outage duration (in hours)** across U.S. states, categorized by climate conditions (`cold`, `normal`, `warm`).

---

## Key Insights:
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


