# Weather & Calorie Burn Analysis

## 📌 Project Motivation
In this project, I will analyze weather and try to show the relationship between **weather conditions** and **calories I burned**.  
I believe there is a correlation between weather and calorie burn.  
I will analyze:
- **Rainfall**
- **Temperature**
- **Wind speed**  


---

## 📌 Data Source

- **🌧️ Rain:** I will collect rain volume data. **Data Source:** [OpenWeather API](https://openweathermap.org).
- **🌡️ Temperature:** It will show the highest temperature of the day. **Data Source:** [OpenWeather API](https://openweathermap.org).
- **🌬️ Wind Speed:** I will collect wind speed data. **Data Source:** [OpenWeather API](https://openweathermap.org).
- **🔥 Calories Burned:** I will collect daily calorie burn data using **[My Phone Apple Health]**.  
  - Calories I burned is related from exercise and daily activities.

---

## 📌 Data Collecting

### 🌦️ **Collecting Rain, Temperature, and Wind Speed Data**
- I will use `requests` in Python to fetch weather data from **OpenWeather API**.
- The API will provide historical and real-time weather data.
- **API Source:** [OpenWeather API](https://openweathermap.org)

### 🔥 **Collecting Calories Burned Data**
- I will extract calorie burn data from **My Phone Apple Health** as an **XML file**.
- The XML data will be converted into **CSV format** using `pandas` in Python.
- **Data Source:** [My Phone Apple Health]


## 📌 Technologies Used
- **Python** 🐍 (Data Processing)
- **Pandas** 📊 (Data Transformation)
- **Requests** 🌍 (API Calls)
- **OpenWeather API** ☁️ (Weather Data Collection)

---

## 1. Data Collection

I gathered two primary data sources—Apple Health export and OpenWeather API—using Google Colab to upload and process the raw files.

### 1.1 Apple Health Data  
1. **Export**  
   - On my iPhone, opened the Health app and exported my “Active Energy Burned” records as an XML file.  
2. **Upload to Colab**  
   ```python
   from google.colab import files
   uploaded = files.upload()  # Upload the Apple Health XML file




# Analysis of Calories Burned and Weather Data

This document outlines the process of collecting, visualizing, and analyzing personal Apple Health data and weather data obtained from the OpenWeather API. The goal was to investigate the potential relationship between daily average wind speed and calories burned over a recent 200-day period.

## 1. Data Collection

### 1.1. Apple Health Data
- My Apple Health data was downloaded from my phone in XML format.
- The XML file was uploaded to Google Colab using the `files.upload()` function.

### 1.2. OpenWeather API Data
- Hourly weather data for the last 5 years in Tuzla was collected using the OpenWeather API.
- The API provided the data in CSV format.
- The CSV file was uploaded to Google Colab using the `files.upload()` function.

## 2. Data Visualization

To gain an initial understanding of the datasets, several visualization techniques were employed:

- **Histograms:**
    - `CaloriesBurned`: To visualize the distribution of daily calorie expenditure.
    - `AvgWindSpeed`: To understand the frequency and range of average wind speeds.

- **Box-plots:**
    - For both `CaloriesBurned` and `AvgWindSpeed`, box-plots were generated before and after outlier removal. This allowed for the identification and quantification of outliers based on the IQR rule and demonstrated the impact of the cleaning process on the data distribution and sample size.

- **Time-series Line Charts:**
    - `AvgTemp`: To observe seasonal temperature variations over the 200-day period.
    - `AvgWindSpeed`: To illustrate the day-to-day volatility and any potential seasonal patterns in wind speed.
    - `CaloriesBurned`: To visualize trends and fluctuations in daily calorie expenditure over time.

- **Scatter Plot:**
    - `AvgWindSpeed` vs. `CaloriesBurned`: To visually inspect for any linear relationship between these two variables.

These visualizations provided insights into the data's characteristics, helped identify anomalies, and informed the subsequent statistical analysis.

## 3. Exploratory Data Analysis (EDA)

The initial phase of the analysis focused on understanding the structure, quality, and potential challenges of the raw data. The objective was to create a clean and unified dataset of daily calories burned and relevant weather metrics, focusing on the most recent 200 days.

### 3.1. Purpose:
- Verify the expected columns, data types, and date ranges in each file.
- Identify and quantify missing values or formatting inconsistencies.
- Detect extreme values (outliers) and determine a strategy for handling them.
- Plan the merging process of the two datasets into a cohesive time series.

### 3.2. Data Loading & Structure Inspection:
- The `calories.csv` (representing the processed Apple Health data) and `daily_weather.csv` (representing the processed OpenWeather data) were loaded into pandas DataFrames.
- The `.head()` method was used to display the first five rows of each DataFrame, and the `.info()` method provided a summary of the data types and non-null values. This step was crucial for understanding the initial structure of the data and identifying necessary transformations for merging.

### 3.3. Cleaning & Integration:
- Stray quotation marks were removed from the data.
- Numeric columns (`CaloriesBurned`, `temp`, `wind_speed`, `rain_1h`) were converted to their appropriate numeric data types.
- UNIX timestamps in the weather data were transformed into calendar dates, and a consistent `Date` column was created in both DataFrames to facilitate merging.
- An inner join was performed on the `Date` column to merge the two DataFrames (`merged_df`), ensuring that only days present in both datasets were included in the analysis.

### 3.4. Outlier Detection & Date Filtering:
- The Interquartile Range (IQR) rule was applied to identify and remove outliers in both `AvgWindSpeed` and `CaloriesBurned` within the 200-day window. Outliers were defined as values falling outside 1.5 times the IQR below the first quartile (Q1) or above the third quartile (Q3).
- The number of days in the dataset before and after outlier removal was confirmed (e.g., reducing from 200 to 197 days).

### 3.5. Preliminary Visualizations & Key Insights:
- Histograms of `CaloriesBurned` and `AvgWindSpeed` provided an overview of their distributions.
- Box-plots effectively highlighted the outliers that were subsequently removed during the cleaning process.
- Time-series line charts of `AvgTemp` and `AvgWindSpeed` revealed a clear seasonal cycle in temperature and significant day-to-day variability in wind speed.

By the conclusion of the EDA phase, a clean, outlier-free, and merged dataset, focused on the most recent 200 days, was prepared for further statistical analysis.

## 4. Hypothesis Testing

**Purpose:** To determine if there is a statistically significant linear relationship between daily average wind speed and calories burned over the 200-day period.

**Hypotheses:**

- **Null Hypothesis (H₀):** There is no linear correlation ($\rho = 0$) between average wind speed and calories burned.
- **Alternative Hypothesis (H₁):** There is a non-zero linear correlation ($\rho \neq 0$) between average wind speed and calories burned.

**Method:**

- The cleaned and merged dataset, excluding outliers and limited to the last 200 days (n=197), was used for this analysis.
- Pearson’s correlation test was applied using the `pearsonr` function from the `scipy.stats` library in Python:

```python
from scipy.stats import pearsonr

r, p_value = pearsonr(df_clean["AvgWindSpeed"], df_clean["CaloriesBurned"])
```
## 4. Hypothesis Testing Results

**Results:**

- **Sample Size (n):** 197
- **Pearson's r:** ≈ 0.025
- **p-value:** ≈ 0.73

**Interpretation:**

The calculated Pearson correlation coefficient ($r \approx 0.025$) is very close to zero, indicating no detectable linear trend in the data.

The p-value ($\approx 0.73$) is considerably higher than the commonly used significance level of $\alpha = 0.05$. This indicates that there is a high probability of observing such a weak correlation (or even a stronger one) if there were truly no correlation in the underlying population. Therefore, we fail to reject the null hypothesis (H₀).

**Conclusion:**

There is no statistically significant evidence of a linear relationship between daily average wind speed and calories burned within the most recent 200-day window of the analyzed data.



## ML Part

### 1) Data Extraction & Feature Engineering
- Loaded the cleaned “last 200 days” dataset (no outliers) plus merged in **humidity** from the 5-year weather archive via API.  
- Dropped raw **Temperature** & **TotalRain** columns, then created:
  - **RainPlus1** = `TotalRain + 1` (to avoid zero-multiplication)  
  - **Temp_x_RainPlus1** = `AvgTemp * RainPlus1`  
- Applied **log(1 + x)** transform to `Temp_x_RainPlus1` for a more symmetric distribution.  
- Added binary **RainFlag** = `(TotalRain > 0).astype(int)`  
- Standardized all X features and kept Y in its original units for RMSE reporting.

### 2) Train / Validation / Test Split
- **Hold-out**: 80 % train / 20 % test split (random_state=42).  
- **Inner CV**: 5-fold KFold on the 80 % training data for hyperparameter search & model comparison.

### 3) Models & Hyperparameter Search
- **Candidates**:
  - KNeighborsRegressor  
  - Ridge  
  - RandomForestRegressor  
- **Search**: `GridSearchCV` over each model’s key hyper-parameters:
  - KNN → `n_neighbors`: [1, 3, 5, 7, 9]  
  - Ridge → `alpha`: [0.01, 0.1, 1, 10, 100]  
  - RF → `n_estimators`: [50, 100, 200], `max_depth`: [None, 5, 10, 20]  
- **Scoring**: Neg MSE → RMSE  
- **Result (CV RMSE)**:  
 
- **KNN** → `best_params={'n_neighbors': 9}`, CV RMSE ≈ **116.6**  
- **Ridge** → `best_params={'alpha': 100}`, CV RMSE ≈ **111.8**  
- **RandomForest** → `best_params={'max_depth': 5, 'n_estimators': 200}`, CV RMSE ≈ **118.1**


### 4) Final Fit & Hold-out Evaluation
- **Best model** (lowest CV RMSE): **Ridge** (α = 100).  
- Re-fit **Ridge** on the full 80 % training set.  
- Evaluated on the 20 % unseen test set → **Test RMSE: 100.5**  

---

> **Key takeaway:**  
> By combining thoughtful feature engineering (Temp×Rain interactions, log-transform, humidity), robust outlier filtering, and nested CV hyperparameter tuning, we obtain a stable Ridge model that generalizes to unseen data with ~100 calories RMSE.


