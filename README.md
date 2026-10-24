# AtmosPredict-AI

AtmosPredict AI is an integrated machine learning project designed for air quality estimation and rainfall prediction. It includes robust data preprocessing pipelines, cross-validation methods, and exploratory visualization tools.

---

## 🚀 Key Components

* **AQI Regression:** 
  * Estimates overall `AQI Value` using specific pollutant metrics like Carbon Monoxide (`co aqi value`), Ozone (`ozone aqi value`), Nitrogen Dioxide (`no2 aqi value`), and PM2.5 (`pm2.5 aqi value`).
  * Geographic attributes (`latitude`, `longitude`) are reserved solely for exploratory spatial visualization.
* **Rainfall Classification:** 
  * Predicts binary rainfall outcomes (`yes`/`no`) using meteorological properties including pressure, temperatures, dew point, humidity, cloud cover, sunshine, wind direction, and wind speed.
  * Excludes temporal index fields (like `day`) to maintain reliable weather-driven signals.
* **Model Pipeline:** Built using robust ensemble and linear approaches (such as XGBoost, Random Forest, Extra Trees, Logistic/Linear Regression) combined with median imputation and standard scaling.

---

## 📦 Saved Models (`joblib`)

The training notebook exports two primary artifact dictionaries using `joblib.dump`:
* `models/aqi_model.joblib`: Extra Trees regressor pipeline with median imputation.
* `models/rainfall_model.joblib`: Logistic Regression pipeline with median imputation and standard scaling.

`app.py` loads these artifacts using `joblib.load` to power the Streamlit UI interface.

---

## ☁️ Deploy on Streamlit Community Cloud

To deploy this project live:
1. Push `app.py`, `requirements.txt`, the `models/` directory, and the `data/` directory to your GitHub repository.
2. In [Streamlit Community Cloud](https://streamlit.io/cloud), create a new app pointing to `app.py` as the main entry point.

---

## ⚠️ Important Limitations

* **AQI Output:** Estimates overall AQI derived from pollutant-specific values; it is not a forward-looking temporal AQI forecast.
* **Generalization:** Rainfall data samples are limited, meaning generalization bounds apply.
* **Evaluation Metrics:** Displayed metrics inside the application reflect held-out validation performance for the deployed model families prior to final refitting on the full dataset.
