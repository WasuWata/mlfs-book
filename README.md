# PM2.5 Forecasting of Stockholm St. Eriksgatan 83

## Project Description
In this project, we use weather data (Open-meteo) and PM2.5 data (AQICN) of selected street, in order to train the XGBoost model and forecast the future PM2.5 level of the sensor. In addition, we utilize the Huggingface Gradio to create the dashboard, to visualize the prediction, feature importance, and performance of the model.


[Dashboards for PM2.5 Prediction](https://huggingface.co/spaces/wasu2704/Iris)
[Air quality data from AQICN](https://aqicn.org/city/sweden/stockholm-st-eriksgatan-83/)



# Feature Selection
We selected total seven features, four from weather data and another three creating from PM2.5 data, according to the table below.
| Features | Description |
| -------- | ----------- |
|`temperature_2m_mean`|Mean daily temperature at 2 meters above ground|
|`precipitation_sum`|Sum of daily precipitation (including rain, showers and snowfall)|
|`wind_speed_10m_max`|Maximum wind speed and gusts on a day|
|`wind_direction_10m_dominant`|Dominant wind direction|
|`lagging1`|Lagged air quality for the previous 1 day|
|`lagging2`|Lagged air quality for the previous 2 days|
|`lagging3`|Lagged air quality for the previous 3 days|

From the feature importance, it is apparent that the `lagging1` and `temperature_2m_mean` are the most important features for our XGBoost model. While `lagging2` and `lagging3` are far less important compared to `lagging1`, that means the previous one day data has the significant effect to the PM2.5 level. On the other hand, `precipitation_sum` is the least important feature among all features.
![alt text](https://raw.githubusercontent.com/WasuWata/mlfs-book/main/notebooks/airquality/air_quality_model/images/feature_importance.png)
