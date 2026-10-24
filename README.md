# AtmosPredict AI — Complete ML + Streamlit Project

This project separates model development from the user interface:

- `AtmosPredict_AI_Machine_Learning.ipynb`: data exploration, model comparisons, evaluation, and the final deployment-export cell.
- `models/aqi_model.joblib` and `models/rainfall_model.joblib`: trained model bundles exported by the notebook using `joblib`.
- `app.py`: Streamlit frontend. It **loads the saved models** and does not retrain them.
- `data/`: the AQI and rainfall CSV datasets.

## Run locally

1. Extract the ZIP and open the project folder in VS Code.
2. Create/activate a virtual environment if desired.
3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Open `AtmosPredict_AI_Machine_Learning.ipynb` and run cells from top to bottom. The final section (15) exports the two models into `models/`. Pre-exported model files are included in this package, so you can also start the app directly.
5. Start the frontend:

   ```bash
   streamlit run app.py
   ```

## Model connection

The notebook exports two dictionaries using `joblib.dump`:
- `models/aqi_model.joblib`: Extra Trees regressor pipeline with median imputation.
- `models/rainfall_model.joblib`: Logistic Regression pipeline with median imputation and standard scaling.

`app.py` loads these using `joblib.load` and passes UI values into each pipeline's `predict`/`predict_proba` methods. If you retrain or change features, rerun the final export cell, then restart the app. Only load joblib files that you trust.

## Deploy on Streamlit Community Cloud

Push `app.py`, `requirements.txt`, the `models/` folder, and `data/` folder to a GitHub repository. In Streamlit Community Cloud, create an app using `app.py` as the main file. Include the notebook if you want the training workflow available in the repository.

## Important limitations

- AQI output estimates overall AQI from pollutant-specific AQI values; it is not a future AQI forecast.
- Rainfall data has 366 observations, so generalization is limited.
- Metrics shown in the app are held-out evaluation metrics for the deployed model family; the saved deployment model is then fitted on all available rows.
