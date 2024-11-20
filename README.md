# mlfs-book
O'Reilly book - Building Machine Learning Systems with a feature store: batch, real-time, and LLMs


## ML System Examples


[Dashboards for Example ML Systems](https://featurestorebook.github.io/mlfs-book/)

## Course Comparison

| Course                         | MLOps | LLLMs             | Feature/Training/Inference | Working AI Systems | Focus |
|--------------------------------|-------|----------------------------|--------------------|------------------|
| Building AI Systems (O'Reilly) | Yes   | Fine-Tuning & RAG | Yes                        | High               | Project-based, Software Engineering, Fundamentals    |
| [Made With ML](https://madewithml.com/)                   | No          | Yes   | No                         | No                 | Software Engineering, Model Training   |
| [7 Steps MLOps](https://www.pauliusztin.me/courses/the-full-stack-7-steps-mlops-framework)            | Yes   | Separate Course    | Yes                        | Low                | Learning Tools and Project    |


# **Air Quality Prediction System for ID2223**

### **Lab 1 - Serverless AI System for Air Quality Prediction**

This project is part of the ID2223 Machine Learning course at KTH for HT2024. The goal of the lab is to build a serverless AI system that predicts air quality (PM2.5) for a specified location, leveraging Hopsworks, feature engineering, and machine learning model development.

### Overview**

The objective of this lab is to create a serverless AI system to predict air quality levels at specific locations using machine learning. The system ingests air quality and weather data, creates feature groups in Hopsworks, trains a machine learning model, and visualizes the results on a public dashboard.

This project uses the following data sources:
- **Air Quality Data** from [AQICN](https://aqicn.org)
- **Weather Data** from [Open-Meteo](https://open-meteo.com)

The complete workflow includes data ingestion, feature engineering, training a model, making batch predictions, and visualization of results.

### **Architecture**

1. **Data Ingestion and Feature Engineering**:
   - **Daily Feature Pipeline**: Automatically ingests daily weather and air quality data and stores them as **Feature Groups** in the Hopsworks **Feature Store**.
   - **Backfill Pipeline**: Backfills historical data from the selected sensor to create a comprehensive dataset.

2. **Model Training**:
   - A regression model (`XGBRegressor`) is trained using weather and air quality features to predict PM2.5 levels.
   - Features are extracted from a **Feature View** created in the Hopsworks platform.

3. **Batch Inference**:
   - The trained model is used to predict PM2.5 levels for the next 7-10 days using weather forecast data.
   - The results are visualized using a dashboard.

### **Components**

This project is divided into several main components:

1. **Feature Pipelines**:
   - **Backfill Feature Pipeline** (`backfill-feature-group.ipynb`): Downloads and processes historical air quality and weather data.
   - **Daily Feature Pipeline** (`daily-feature-pipeline.py`): Runs daily to ingest fresh data from AQICN and Open-Meteo.

2. **Model Training Pipeline**:
   - **Training Pipeline** (`training-pipeline.ipynb`): Trains a machine learning model to predict PM2.5 levels based on features from air quality and weather data.

3. **Batch Inference and Dashboard**:
   - **Batch Inference Pipeline** (`batch-inference-pipeline.py`): Runs predictions on new data and saves the results for visualization.
   - **Dashboard** (`dashboard/`): A public dashboard visualizing air quality predictions for a selected location.

### **Setup Instructions**

To set up and run the system, please follow the steps below:

#### **Prerequisites**
- Create a **Hopsworks** account at [hopsworks.ai](https://app.hopsworks.ai).
- Set up a **GitHub** account to manage the code.
- (Optional) Set up **Modal.com** for serverless execution of pipelines.
- Use **Conda** or **virtual environments** to manage Python dependencies.

#### **Steps to Run the Project**

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/air-quality-prediction.git
   ```
2. **Create the Environment**:
   - Use the provided `environment.yml` or `requirements.txt` to create a Python environment:
     ```bash
     conda env create -f environment.yml
     conda activate air-quality
     ```
3. **Set Up Hopsworks**:
   - Register and log in to **Hopsworks**.
   - Create an **API Key** in Hopsworks and add it as an environment variable:
     ```bash
     export HOPSWORKS_API_KEY=your_api_key_here
     ```

4. **Run the Pipelines**:
   - **Backfill Feature Pipeline**: Run this notebook to backfill historical data.
   - **Daily Feature Pipeline**: Use **GitHub Actions** to run this daily and keep the feature groups up-to-date.
   - **Training Pipeline**: Run the training notebook to create and register the model.
   - **Batch Inference Pipeline**: Run the inference pipeline to generate predictions.

5. **Deploy the Dashboard**:
   - The dashboard is deployed using **GitHub Pages** or **Streamlit** and displays the predicted air quality levels.

### **Results**

- The trained model is capable of predicting PM2.5 levels based on weather conditions and historical air quality data.
- The model performance is evaluated using metrics like **Mean Squared Error (MSE)** and **R-squared (R²)**.
- **Hindcast Graphs** are provided to show prediction performance compared to observed values.

### **Dashboard Link**

The **public dashboard** showing predictions for air quality is available here:
[**Air Quality Prediction Dashboard**](https://yourusername.github.io/air-quality-prediction)

### **Acknowledgments**

- This project is part of the **ID2223 Machine Learning Course** at **KTH**.
- The main sources of data are **AQICN** for air quality and **Open-Meteo** for weather information.
- Reference materials include the **Building ML Systems with a Feature Store** book by Jim Dowling.