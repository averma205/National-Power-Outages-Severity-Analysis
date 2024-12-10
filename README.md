# National Power Outages Severity Analysis

## Contributors
- **Arya Verma**
- **Deepal Deleena**
---

## Introduction

### Dataset Overview
This project focuses on the **Power Outages** dataset. The dataset contains information about major power outages in the U.S. from January 2000 to July 2016, including details about the outage duration, cause, customer impact, and associated economic and demographic data.

### Research Question
What are the characteristics of the most severe power outages, and which factors (location, climate, outage cause, etc.) are most commonly associated with higher severity?

### Why This Dataset Matters
Understanding the patterns and causes of severe power outages can help energy companies improve infrastructure planning, manage risks effectively, and reduce the impact on customers. The dataset is vital for building predictive models that forecast outage severity based on historical patterns.

### Dataset Summary
- **Total Rows**: 1,534  
- **Relevant Columns**:  
  - `OUTAGE.DURATION`: Duration of the power outage (in minutes).  
  - `DEMAND.LOSS.MW`: Power demand loss (in megawatts).  
  - `CAUSE.CATEGORY`: General category of the outage cause.  
  - `NERC.REGION`: Regional electrical reliability organization.  
  - `CUSTOMERS.AFFECTED`: Number of customers impacted.  

---

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning
The dataset required significant preprocessing to ensure accuracy:
1. Replaced missing values in columns like `OUTAGE.DURATION` and `DEMAND.LOSS.MW` with `NaN`.
2. Combined date and time columns into unified timestamp columns for outage start and restoration.
3. Removed irrelevant columns like `variables` and rows with excessive missingness.

#### Head of Cleaned DataFrame
```plaintext
| OUTAGE.DURATION | DEMAND.LOSS.MW | CAUSE.CATEGORY | NERC.REGION | CUSTOMERS.AFFECTED |
|-----------------|----------------|----------------|-------------|--------------------|
| 1000           | 500            | Severe Weather | MRO         | 10000             |
| 600            | 300            | Equipment Fault| ERCOT       | 5000              |

<iframe
  src="assets/statewide_avg_price_vs_electricity_consumed.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>