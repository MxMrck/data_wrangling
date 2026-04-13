# Big Smile Loyalty Program - Data Wrangling Project

Work sample from loyalty program **"Big Smile"** — Student work from MSc Business Intelligence

## 📋 Project Overview

This project demonstrates professional data wrangling techniques applied to a real-world loyalty program dataset. 
The goal is to clean, transform, and prepare member and reward data for segmentation analysis using clustering algorithms.

### Key Objectives
- **Data Cleaning**: Handle missing values, outliers, and data quality issues
- **Data Transformation**: Create meaningful features for RFM (Recency, Frequency, Monetary) analysis
- **Member Segmentation**: Prepare data for K-Means and hierarchical clustering
- **Feature Engineering**: Develop loyalty scores and category-specific metrics

## 📁 Data Files

### 1. **MEMBERS_DIM.csv** (~49 MB)
Members dimension table containing:
- **Member ID**: Unique member identifier
- **Demographics**: Age, Gender, Language, Province
- **Account Info**: Email flag, Tenure in months
- **Loyalty Points**: 
  - Cash Back Points Balance
  - Reward Points Balance
- **Tier**: Member tier classification

**Data Quality Issues Addressed:**
- Negative age values → replaced with 0
- Negative reward points → removed (~92 records)
- Missing values in categorical fields → filled with "Unknown"

### 2. **REWARD_FACT.csv** (~73 MB)
Reward transactions covering 2 years of program data:
- **Transaction Details**: Points redeemed, Items redeemed, Redemption count
- **Categories**: Cash Back, Reward Category 1-4
- **Temporal**: Month ID for tracking transaction timing

**Data Transformations:**
- One-hot encoding for reward categories
- Aggregation by member ID (one row per member)
- Percentage calculations per category

### 3. **BigSmile_Data_wrangling.ipynb**
Main Jupyter Notebook containing complete workflow:
- Data loading and exploration
- Cleaning and preprocessing steps
- Feature engineering and RFM calculations
- Loyalty scoring and member segmentation

## 🔧 Methodology

### Phase 1: Data Loading & Exploration
- Load CSV files with automatic delimiter detection
- Descriptive statistics for numerical columns
- Identify missing values and data types
- Detect outliers and anomalies

### Phase 2: Data Cleaning
- **Handle Missing Values**: 
  - Categorical: Fill with "Unknown"
  - Numerical: Fill with 0 (age) or remove negative values
- **Remove Outliers**: Use ±2σ (standard deviation) method
- **Quality Checks**: Validate positive values for point balances

### Phase 3: Feature Engineering
- **Dummy Variables**: Create one-hot encoded features for reward categories
- **Percentage Metrics**: Calculate % of points/redemptions per category
- **Recency Score**: Months since last redemption (inverted for positive correlation)
- **Loyalty Score**: Composite RFM score using:
  - 20% weight: Recency (MONTHS_SIN_LAST_REDEMP_INV)
  - 40% weight: Points Redeemed (POINTS_REDEEMED)
  - 60% weight: Items Redeemed (NUMBER_ITEMS_REDEEMED)

### Phase 4: Member Segmentation
- **Standardization**: MinMaxScaler (0-1 range)
- **Clustering Algorithms**:
  - K-Means clustering
  - Hierarchical clustering
  - Silhouette score evaluation
- **Loyalty Labels**:
  - **Bronze**: Bottom 60% (SCORE_BS_USAGE)
  - **Silver**: 60-90th percentile
  - **Gold**: Top 10% (highest engagement)

## 📊 Key Variables & Outputs

### Input Features (Members)
- `TENURE_MONTHS`: Membership duration
- `AGE`: Member age
- `CASH_BACK_POINTS_BALANCE`: Accumulated cash back points
- `REWARD_POINTS_BALANCE`: Accumulated reward points

### Engineered Features (Rewards)
- `POINTS_REDEEMED`: Total points redeemed
- `NUMBER_ITEMS_REDEEMED`: Count of redeemed items
- `MONTHS_SIN_LAST_REDEMP`: Time since last redemption
- `%_POINTS_REDEEMED_PER_*`: Category-specific point percentages
- `SCORE_BS_USAGE`: Composite loyalty usage score (0-1000)
- `FIDELITY_LABEL`: Member tier (Bronze/Silver/Gold)

### Output Files
- `df_Members_final.csv`: Cleaned members dataset
- `df_Rewards_final.csv`: Aggregated rewards with loyalty scores

## 💡 Key Insights & Decisions

1. **Outlier Handling**: While outliers were identified using ±2σ method, they were retained initially as they may represent valuable high-engagement members—removal is exploratory.

2. **Missing Data Strategy**: Preserved all observations by filling missing categorical values with "Unknown" rather than deletion, ensuring comprehensive segmentation analysis.

3. **Negative Values**: Removed 92 records (~0.007%) with negative reward points—insufficient volume to warrant detailed root cause analysis.

4. **Scaling**: Used MinMaxScaler for RFM components to ensure non-negative composite scores and equal weighting on 0-1 scale.

5. **Tier Distribution**: Pyramid structure (60% Bronze, 30% Silver, 10% Gold) aligns with typical loyalty program economics.

## 🛠 Technologies & Libraries

```python
# Data Processing
pandas
numpy

# Machine Learning
scikit-learn (preprocessing, clustering, metrics)
scipy (hierarchical clustering)

# Visualization (in notebook, currently commented)
matplotlib
seaborn
