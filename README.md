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




## 1. Data Collection

I gathered two primary data sources—Apple Health export and OpenWeather API—using Google Colab to upload and process the raw files.

### 1.1 Apple Health Data  
1. **Export**  
   - On my iPhone, opened the Health app and exported my “Active Energy Burned” records as an XML file.  
2. **Upload to Colab**  
   ```python
   from google.colab import files
   uploaded = files.upload()  # Upload the Apple Health XML file
Parse & Save

Parsed the XML with xml.etree.ElementTree, extracted daily calories, and built a DataFrame with columns Date and CaloriesBurned.

Saved to calories.csv:

python
Kopyala
Düzenle
df_cal.to_csv("calories.csv", index=False)
1.2 OpenWeather API Data
Fetch

Queried the OpenWeather “One Call” API for hourly weather in Tuzla covering the last 5 years.

Received the response as a CSV file.

Upload to Colab

python
Kopyala
Düzenle
uploaded = files.upload()  # Upload the OpenWeather CSV file
Process & Save

Loaded the CSV into pandas, converted UNIX timestamps to dates, and aggregated to daily metrics:

AvgTemp (mean of temp)

AvgWindSpeed (mean of wind_speed)

TotalRain (sum of rain_1h)

Saved the result to daily_weather.csv:

python
Kopyala
Düzenle
daily_summary.to_csv("daily_weather.csv", index=False)
