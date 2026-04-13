# Big Smile Loyalty Program Data Wrangling Project

## Project Overview
This repository showcases a comprehensive data wrangling that prepares data for downstream customer segmentation analysis through systematic cleaning, transformation, and feature engineering. The analysis is based on realistic datasets from a fictive Big Smile loyalty program.

## Files Description
- **BigSmile_Data_wrangling.ipynb**: This Jupyter notebook contains the step-by-step data cleaning process applied to the raw data into ready-to-us data for k-means algorythm usage
- - **MEMBERS_DIM.csv**: File containing informations about members.
- - **REWARD_FACT.csv**: File containing reccords of points redeemed by members
- - **TRANSACTRIONS.csv**: !NOT INCLUDED! This is the raw data file containing transaction records of loyalty program participants. 

## Methodology
1. **Data Collection**: The raw transaction data was collected from the Big Smile program's database.
2. **Data Cleaning**: Missing values were identified and handled
3. **Data Transformation**: The cleaned data was transformed to create new features relevant to the analysis such as retention rates and average transaction values, dummies variables were created to prepare the dataset for machine learning operations.
4. **Data Analysis and Segmation**: !NOT INCLUDED YET! Exploratory data analysis (EDA) and K-Means clustering algorithm were applied to segment members based on loyalty program usage patterns and points redemption behavior.

