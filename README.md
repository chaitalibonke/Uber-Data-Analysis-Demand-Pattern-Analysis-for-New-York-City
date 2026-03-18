# Uber Data Analysis — Demand Pattern Analysis for New York City

## Overview
This project performs a comprehensive exploratory data analysis on
Uber pickup data from New York City covering the first six months of
2015. The analysis explores how time, weather, location, and holidays
influence Uber demand across NYC boroughs. Actionable insights and
business recommendations are provided to help Uber optimize fleet
allocation and improve service availability.

---

## Business Context
Ridesharing demand is highly dynamic and varies by time, location,
weather, and local events. This project analyzes Uber pickup data
from New York City to uncover demand patterns and generate
operational recommendations for fleet allocation and service
availability.

---

## Objective
- Identify the key variables that influence Uber pickups
- Determine which factor affects pickups the most and why
- Provide data-driven recommendations to Uber management to
  capitalize on fluctuating demand patterns

---

## Key Questions
- What are the different variables that influence pickups?
- Which factor affects pickups the most and what are the
  plausible reasons?
- What recommendations can help Uber management capitalize
  on fluctuating demand?

---

## Dataset

- **Source:** Uber NYC Pickup Dataset (publicly available / academic dataset)
- **File:** Uber.csv
- **Size:** 29,101 rows x 13 columns
- **Time Period:** January 1, 2015 to June 30, 2015
- **Granularity:** Hourly pickup counts per NYC borough
- **Note:** The dataset is not included in this repository

### Data Dictionary

| Column    | Type    | Description                                      |
|-----------|---------|--------------------------------------------------|
| pickup_dt | object  | Date and time of the pickup                      |
| borough   | object  | NYC borough where pickup occurred                |
| pickups   | int64   | Number of pickups in the hour                    |
| spd       | float64 | Wind speed in miles per hour                     |
| vsb       | float64 | Visibility in miles to the nearest tenth         |
| temp      | float64 | Temperature in Fahrenheit                        |
| dewp      | float64 | Dew point in Fahrenheit                          |
| slp       | float64 | Sea level pressure                               |
| pcp01     | float64 | 1-hour liquid precipitation                      |
| pcp06     | float64 | 6-hour liquid precipitation                      |
| pcp24     | float64 | 24-hour liquid precipitation                     |
| sd        | float64 | Snow depth in inches                             |
| hday      | object  | Holiday indicator (Y = holiday, N = not holiday) |

---

## Methodology

### 1. Data Understanding
- Load and inspect dataset structure and data types
- Convert pickup_dt from object to datetime format
- Extract date parts: year, month, hour, day, weekday

### 2. Data Cleaning
- Identify 3,043 missing values in the borough column
- Missing borough values were retained as Unknown to avoid
biased imputation. Note that EWR (Newark Liberty International
Airport) is included as a location category despite being
located in New Jersey, not within NYC's five official boroughs.
- Confirm no missing values in any other column

### 3. Univariate Analysis
- Histogram and boxplot combined plots for key numerical variables
- Distribution analysis for pickups, visibility, and snow depth
- Countplot with percentage annotations for holiday and borough

### 4. Multivariate Analysis
- Correlation heatmap for all numerical variables
- Pickups trend across months, days of month, and weekdays
- Pickups distribution across boroughs using boxplots
- Holiday vs non-holiday pickup comparison by borough
- Hourly pickup patterns by borough using line plots
- Log-scale hourly pickup visualization for low-volume boroughs
- Manhattan heatmap of pickups by hour and weekday

---

## Key Results

### Borough Distribution
| Borough       | Observations | Share  |
|---------------|--------------|--------|
| Bronx         | 4,343        | 14.92% |
| Brooklyn      | 4,343        | 14.92% |
| EWR           | 4,343        | 14.92% |
| Manhattan     | 4,343        | 14.92% |
| Queens        | 4,343        | 14.92% |
| Staten Island | 4,343        | 14.92% |
| Unknown       | 3,043        | 10.46% |

### Holiday vs Non-Holiday Pickups
| Day Type    | Mean Pickups |
|-------------|--------------|
| Non-Holiday | 492.34       |
| Holiday     | 437.20       |

### Pickups Summary Statistics
| Metric  | Value |
|---------|-------|
| Mean    | ~500  |
| Median  | 0     |
| Maximum | 8,000 |

> The median of 0 reflects many low-volume borough-hour combinations
> with zero pickups, particularly in EWR and Staten Island.

---

## Key Findings
- Manhattan accounts for the largest share of pickups across
  all time periods
- Demand shows a clear and consistent increasing trend from
  January through June with June pickups approximately 1.5
  times higher than January
- Weather variables show low linear correlation with pickups
  though non-linear effects may still exist and warrant
  further investigation
- Temporal features such as hour of day and day of week were
  stronger predictors of demand than weather variables
- Pickup demand peaks between 7 PM and 8 PM on weekdays
  consistent with evening office commute patterns
- A secondary morning peak is observed between 6 AM and 10 AM
  consistent with morning office commute patterns
- Weekend demand particularly Friday and Saturday nights remains
  high into midnight suggesting strong leisure travel demand
- Monday shows unusually low demand compared to other weekdays
  warranting further investigation
- EWR and Staten Island have negligible pickup volume suggesting
  demand in these areas can be covered by inbound drop-off trips
- Brooklyn and Queens show growth potential as secondary markets
  after Manhattan
- Findings are based on aggregated hourly data and may mask
  intra-hour variability in demand patterns

---

## Conclusions
- Uber pickups are most concentrated in Manhattan
- Weather variables do not show strong linear correlation with
  pickup demand
- Demand has been steadily increasing across all months analyzed
- Weekend and late evening hours represent peak demand periods
- Office commute hours drive strong weekday demand patterns
- New Yorkers use Uber for both regular commuting and leisure

---

## Recommendations

### Fleet Optimization
- Ensure maximum cab availability during 7 PM to 8 PM on weekdays
  to meet peak commute demand
- Increase fleet availability on Friday and Saturday nights when
  demand remains high into midnight
- Focus driver incentives in Manhattan where demand is highest
  and most consistent

### Market Development
- Invest in growing presence in Brooklyn and Queens which show
  strong potential as secondary markets
- Deprioritize EWR and Staten Island where demand is negligible
  and can be served by existing inbound trip drop-offs

### Data and Modeling
- Procure fleet size data to model demand-supply gaps
- Build a machine learning model to predict hourly pickups
  per borough for proactive fleet optimization
- Procure pricing data to build an optimal dynamic pricing model
- Investigate the consistently low Monday demand to identify
  whether it is a data issue or a genuine behavioral pattern

### Further Analysis
- Combine weekends and holidays as non-working days and compare
  against weekdays for deeper demand segmentation
- Remove EWR and Staten Island from borough-level analysis to
  reduce noise and sharpen insights for actionable boroughs
- Explore non-linear relationships between weather variables
  and pickups using tree-based models

---

## Tech Stack
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Google Colab

---

## How to Run

> This notebook is designed for Google Colab.

**Step 1 — Upload the dataset to Google Drive:**
- Upload Uber.csv to your Google Drive

**Step 2 — Open the notebook in Google Colab**

**Step 3 — Mount Google Drive and run all cells:**
```python
from google.colab import drive
drive.mount('/content/drive')
```

**Step 4 — Install dependencies if needed:**
```bash
pip install pandas numpy matplotlib seaborn
```

---

## Limitations
- Data covers only six months (Jan to June 2015) and may not
  represent full-year seasonal demand patterns
- Weather variables show low linear correlation with pickups
  but non-linear effects may still exist
- The Unknown borough category (10.46% of data) limits
  geographic precision of the analysis
- No pricing or driver supply data was available which limits
  demand-supply gap analysis
- Findings are based on aggregated hourly data and may mask
  intra-hour variability in demand patterns

---

## Disclaimer
The Uber NYC Pickup dataset is publicly available
and is not included in this repository. All analysis and
recommendations are based solely on the provided dataset sample.
