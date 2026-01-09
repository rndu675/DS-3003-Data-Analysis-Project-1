# Podcast User Engagement Analysis – Data Analysis Project 1

This notebook performs comprehensive data pre-processing, feature engineering, and exploratory data analysis on a podcast listening dataset with the goal of understanding factors that influence **completion rate**.

## Main Steps Performed

### 1. Environment Setup
- Installed `prince` (for FAMD)
- Imported standard data science libraries (pandas, numpy, sklearn, matplotlib, seaborn, prince)

### 2. Data Loading
- Fetched dataset from Kaggle: *Podcast Listening Time Prediction Dataset*
- Loaded `podcast_dataset.csv`

### 3. Initial Data Exploration
- Basic overview (head, info, describe, categorical summary)

## Data Pre-processing

### 4. Data Formatting
- Standardized column names (lowercase)
- Standardized categorical values (lowercase and whitespace stripping)

### 5. Removing Duplicates
- Removed exact duplicate observations

### 6. Dataset Splitting
- Stratified train–test split (80/20) using `genre` as the stratification variable
- Compared categorical distributions across original, training, and testing datasets

### 7. Missing Value Treatment
- Applied **IterativeImputer (MICE)** for:
  - `listening_time_minutes`
  - `episode_length_minutes`
- Applied **KNNImputer** (with feature scaling and one-hot encoded categorical variables) for `guest_popularity_percentage`

### 8. Outlier Detection
- **Univariate detection:** IQR method on key numerical variables
- **Multivariate detection:** Isolation Forest with 5% contamination

## Feature Engineering

### 9. Feature Extraction
- Created **completion_rate** = `listening_time_minutes / episode_length_minutes`
- Created **length_category** (Short / Medium / Long / Extra-Long)

### 10. Dimensionality Reduction
- Applied **FAMD (Factor Analysis of Mixed Data)** on mixed numerical and categorical features
- Reduced data to two components for visualization
- Analyzed variable contributions to the extracted dimensions

### 11. Clustering
- Performed **K-Means clustering** on FAMD components
- Determined optimal number of clusters using:
  - Elbow method
  - Silhouette score
  - Davies–Bouldin index
- Optimal solution identified at **k ≈ 3 clusters**

## Exploratory Data Analysis (EDA)

### 12. Exploratory Data Analysis
- Distribution analysis of numerical features (pairplots and individual histograms)
- Count plots for categorical variables
- Correlation heatmap for numerical variables
- Completion rate analysis by:
  - Genre
  - Number of advertisements
  - Episode sentiment
  - Publication day and time (heatmap)
  - Episode length category
- Interaction effects:
  - Genre × number of ads
  - Genre × episode length category
- Mutual Information analysis between predictors and completion rate

## Key Target Variable
- **completion_rate (0–1):** proportion of the episode that listeners actually consumed
