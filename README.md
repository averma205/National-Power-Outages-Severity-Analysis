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

### Data Cleaning
To prepare the dataset for analysis, we performed the following steps:
1. **Addressing Missing Values**: Replaced missing values in critical columns like `OUTAGE.DURATION` and `DEMAND.LOSS.MW` with `NaN` for accurate analysis.
2. **Standardizing Date and Time**: Unified date and time columns into `START.TIME` and `END.TIME` to enable calculations like outage duration.
3. **Removing Irrelevant Features**: Dropped unnecessary columns such as `variables` and any rows with excessive missing values or irrelevant data.
4. **Feature Engineering**: Created new features, including `OUTAGE.HOURS` (duration in hours) and `AFFECTED.PERCENTAGE` (percentage of customers affected in the region).

### Snapshot of Cleaned DataFrame
| OUTAGE.DURATION | DEMAND.LOSS.MW | CAUSE.CATEGORY | NERC.REGION | CUSTOMERS.AFFECTED | OUTAGE.HOURS | AFFECTED.PERCENTAGE |
|-----------------|----------------|----------------|-------------|--------------------|--------------|---------------------|
| 1000           | 500            | Severe Weather | MRO         | 10000             | 16.67        | 0.05%              |
| 600            | 300            | Equipment Fault| ERCOT       | 5000              | 10.00        | 0.02%              |

---

### Exploratory Data Analysis (EDA)

#### 1. Univariate Analysis
We analyzed the distribution of key variables:
- **Outage Duration**: Most outages lasted between 1 to 20 hours, with a few extreme cases extending beyond 100 hours.
- **Demand Loss (MW)**: Severe weather events resulted in the largest power demand losses.
- **Customer Impact**: Events affecting more than 1 million customers were predominantly caused by hurricanes or snowstorms.

#### Example Visualization: Distribution of Outage Durations
![Outage Duration Distribution](assets/outage_duration_histogram.png)

#### 2. Bivariate Analysis
We explored relationships between outage causes and their impacts:
- Severe weather events had the highest average outage durations and customer impact.
- Equipment faults were more frequent but generally caused shorter outages.

#### Visualization: Average Outage Duration by Cause
![Average Outage Duration by Cause](assets/avg_duration_by_cause.png)

#### 3. Regional Trends
Using geographical data, we identified regions most susceptible to severe outages:
- **Highest Duration**: MRO (Midwest Reliability Organization).
- **Most Customers Affected**: SERC (Southeastern Electric Reliability Council).

<iframe
  src="assets/statewide_avg_price_vs_electricity_consumed.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
