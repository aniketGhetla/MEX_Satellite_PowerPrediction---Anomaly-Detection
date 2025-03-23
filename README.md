# Satellite_MEX
# Mars Express Orbiter Power Consumption Prediction
This repository contains the code and methodology for predicting power consumption and detecting behavior in the Mars Express Orbiter's telemetry data. The project explores different machine learning approaches to accurately model the power consumption of the satellite, using various features from satellite telemetry data, including solar aspect angles, subsystem commands, and other operational data.

# Project Structure
preprocessing.pynb:
This notebook contains all the preprocessing and feature engineering steps. It processes raw telemetry data from the Mars Express Orbiter, aligning timestamps, resampling data into 15-minute intervals, and creating new features such as energy received based on solar aspect angles and Sun-Mars distance. It also covers data normalization and feature extraction for use in machine learning models.

Baseline_and_ensembled_approach.pynb:
This notebook explores the baseline Linear Regression model and the ensemble model approach using XGBoost and Extra Trees Regressor. These models aim to predict power consumption using telemetry data as features. The ensemble model approach demonstrates improved predictive performance over the baseline linear regression model by capturing more complex relationships between satellite telemetry data and power consumption.

train_model_mex.ipynb:
This notebook contains the final behavioral model using a time-window-based approach. Different models (Random Forest, XGBoost, CatBoost) are trained for each time window (7-hour windows with 1-hour overlap), dynamically adjusting to changes in satellite behavior. The best-performing model for each time window is selected based on RMSE. This approach produced the best overall prediction accuracy, with an RMSE score of 0.0306 across all windows.

# Methodology

1. Preprocessing and Feature Engineering
The preprocessing.pynb notebook outlines the following steps:
Timestamp Alignment: Synchronizing telemetry data from various sources (e.g., Solar Aspect Angles, Subsystem Commands, Flight Timeline) by converting ut_ms to datetime format.
Feature Engineering: Key features such as energy received, subsystem activation counts, and solar aspect cosine transformations are generated.
Resampling and Aggregation: Data is resampled into 15-minute intervals, and missing values are interpolated or forward-filled as needed.

3. Baseline and Ensemble Modeling
The Baseline_and_ensembled_approach.pynb notebook includes:
Baseline Linear Regression: A simple model using the top 5 correlated features for each thermal power line.
Ensemble Models:
XGBoost and Extra Trees models are used to predict power consumption.
Feature importance is calculated using the Extra Trees Regressor to select the top 40 features for each power line.
Overall Model Performance:
XGBoost - Average RMSE: 0.0447, Average R²: 0.2028
Extra Trees - Average RMSE: 0.0451, Average R²: 0.1121

3. Behavioral Approach (Final Model)
The train_model_mex.ipynb notebook contains the final Behavioral Approach, which adapts to changes in spacecraft operations by training different models for different time windows:
Sliding Time Windows: 7-hour windows with a 1-hour overlap are used to capture the satellite's changing behavior over time.
Dynamic Model Selection: The best-performing model (Random Forest, XGBoost, or CatBoost) is selected for each time window based on RMSE.
Final Results:
Overall RMSE across all windows: 0.0306, indicating a highly accurate prediction of power consumption.
