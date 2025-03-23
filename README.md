# Mars Express Orbiter Power Consumption Prediction
## Introduction
This repository contains the code and methodology for predicting power consumption and detecting behavior in the Mars Express Orbiter's telemetry data. The project explores different machine learning approaches to accurately model the power consumption of the satellite, using various features from satellite telemetry data, including solar aspect angles, subsystem commands, and other operational data.

## Architechture diagram
![Architecture Diagram](images/architecture_diagram_casestudy.png "Architecture Diagram")

## Methodology

1. Preprocessing and Feature Engineering
The preprocessing.pynb notebook outlines the following steps:
Timestamp Alignment: Synchronizing telemetry data from various sources (e.g., Solar Aspect Angles, Subsystem Commands, Flight Timeline) by converting ut_ms to datetime format.
Feature Engineering: Key features such as energy received, subsystem activation counts, and solar aspect cosine transformations are generated.
Resampling and Aggregation: Data is resampled into 15-minute intervals, and missing values are interpolated or forward-filled as needed.

2. Baseline and Ensemble Modeling
The Baseline_and_ensembled_approach.pynb notebook includes:
Baseline Linear Regression: A simple model using the top 5 correlated features for each thermal power line.
Ensemble Models:
XGBoost and Extra Trees models are used to predict power consumption.
Feature importance is calculated using the Extra Trees Regressor to select the top 40 features for each power line.
Overall Model Performance:
XGBoost - Average RMSE: 0.0447, Average R²: 0.2028
Extra Trees - Average RMSE: 0.0451, Average R²: 0.1121
The ensemble model approach demonstrates improved predictive performance over the baseline linear regression model by capturing more complex relationships between satellite telemetry data and power consumption.

3. Behavioral Approach
The train_model_mex.ipynb notebook contains the final Behavioral Approach, which adapts to changes in spacecraft operations by training different models for different time windows:
Sliding Time Windows: 7-hour windows with a 1-hour overlap are used to capture the satellite's changing behavior over time.
Dynamic Model Selection: The best-performing model (Random Forest, XGBoost, or CatBoost) is selected for each time window based on RMSE.
Final Results:
Overall RMSE across all windows: 0.0306, indicating a highly accurate prediction of power consumption.
Best performing model for each time window is stored in pickle file for using it during Testing Phase.

4. Test File and Prediction Generation
The Test_Model_MEX.ipynb file contains test telemetry data used for generating predictions. When executed, it applies the saved models from the model_pickle directory to produce a prediction_output.csv file. This output file contains the predicted power consumption values at 15-minute intervals, enabling further evaluation and analysis of the satellite's performance.  




