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

