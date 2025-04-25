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
## Data Collecting

I used my apple heath data and OpenWeather API to collect weather data.

- **Collecting Apple Heath Data**:  
  I download my apple heath data as xml format to my computer from my phone, then I used  
  ```python
  uploaded = files.upload()
to upload it to my Google Colab.

Collecting Data from OpenWeather API:
For taking the hourly weather data for last 5 year in Tuzla, I used OpenWeather API. It gave me a CSV format, and I used

python
Kopyala
Düzenle
uploaded = files.upload()
to upload it to my Google Colab.

