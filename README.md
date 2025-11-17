# COVID-19 Predictor

COVID-19 Predictor is an educational project that scrapes public COVID-19 case counts, trains a Long Short-Term Memory (LSTM) neural network to forecast short-term case counts, and exposes data and predictions via a Django website.

> Disclaimer: This project was created for learning purposes. Predictions are not validated for public health use and should not be treated as authoritative.

## Status
Prototype (proof-of-concept). Components include:
- Data scraper (dataScraper/)
- Model training and inference (AI/)
- Django website for visualization (Website/mysite/)

## Quick links
- AI inference script: [AI/runPUTCASES.py](AI/runPUTCASES.py)  
- AI training script: [AI/trainPUTCASES.py](AI/trainPUTCASES.py)  
- Django site root: [Website/mysite](Website/mysite)  
- Scraped CSV (example): [dataScraper/output.csv](dataScraper/output.csv)

## Requirements (Windows)
- Python 3.8+ (adjust as needed)
- pip packages: tensorflow, keras, pandas, numpy, scikit-learn, matplotlib, django, scrapy (for scraper)
Suggested install:
    python -m venv .venv
    .venv\Scripts\activate
    pip install --upgrade pip
    pip install tensorflow keras pandas numpy scikit-learn matplotlib django scrapy

## Usage

1. Prepare data
   - Run your scraper to generate the CSV used by the model (example path: dataScraper/output.csv).
   - Confirm the CSV matches the format expected by [AI/runPUTCASES.py](AI/runPUTCASES.py).

2. Train model (optional)
   - To train or re-train, run the training script:
     cd to repository root and run:
       python AI\trainPUTCASES.py
   - The training script can save a model under `AI/models/PUTCASES/model` (see script prompts).

3. Run prediction (inference)
   - Run the inference script which loads the saved model and writes predictions to `AI/putPrediction.txt`:
       python AI\runPUTCASES.py

4. Start the website (Django)
   - From the Django project directory:
       cd Website\mysite
       python manage.py runserver
   - Open http://127.0.0.1:8000/ in a browser.
   - The site reads predictions from `AI/putPrediction.txt` and historical data stored in the app database.

## Project structure (high level)
- AI/ — model training and inference
  - runPUTCASES.py — loads model and creates short-term forecasts
  - trainPUTCASES.py — training script to build & save LSTM model
  - models/ — saved Keras/TensorFlow models
- dataScraper/ — scraper that produces data (example output: output.csv)
- Website/mysite/ — Django website showing past data and predictions
  - main/ — Django app (models, views, templates, migrations)
  - manage.py — Django management wrapper