# PM2.5 Forecasting of Stockholm St. Eriksgatan 83

## Project Description
In the present, air pollution has become one of the most significant problems to our world, especially for both people's physical and mental health. Because of that, it will be benefit if we create the model to predict the air quality from the available sensors in the opensource, so we expect to see both the future PM2.5 level and the feature importance of the environment's properties to PM2.5 level.

## Data Source and Data Acquisition
In this project, we use weather data (Open-meteo) and PM2.5 data (AQICN) of selected street, in order to train the model and forecast the future PM2.5 level of the sensor. In addition, we utilize the Huggingface Gradio to create the dashboard, to visualize the prediction, feature importance, and performance of the model.

Additionally, we use the github action and github workflow to do the daily data acquisition of PM2.5 data and generate the batch inference of PM2.5 for future 7 days.

[Air quality data from AQICN](https://aqicn.org/city/sweden/stockholm-st-eriksgatan-83/)

[Weather data from Open-meteo](https://open-meteo.com/)


## Feature Selection
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

Additionally, PM2.5 levels are mostly influenced by weather rather than car traffic or industry. Nevertheless, it could be interesting to add features such as the day of the week (e.g., whether it is a working day or a rest day like Sunday, when there may be less traffic) to see whether the model performs better and whether these features are important.

## Model Training and Result
We used the XGBoost model to train the acquired data, setting the data before 2025-05-01 as training data and after that as test data. As a result, we can see the performance of the model according to the graph.
![alt text](https://raw.githubusercontent.com/WasuWata/mlfs-book/main/notebooks/airquality/air_quality_model/images/pm25_hindcast.png)
Compared to the original features, without lagging features, it is obvious that just adding the lagging features helps tremendously increase the model performance, from MSE = 155.21/R2 = -0.709 to MSE = 55.905/R2 = 0.3998. It is because of the new features. In the real world, it is understandable that the PM2.5 level of the current date will be affected from PM2.5 level of the past dates, like it is treated as the source for the current date. So, it is beneficial to add the lagging features. Also, It could also be useful to train a single model on several sensors from the same area to increase the amount of data, and then fine-tune it for a specific sensor.

[Dashboards for PM2.5 Prediction](https://huggingface.co/spaces/wasu2704/Iris)

## Future Forecasting
We will use the mentioned features for PM2.5 forcasting (7 days), however, the problem occurs when we try to predict the PM2.5 at D+2,D+3,... because we do not have the PM2.5 data of D+1 from the historical dat. So, we will use the predicted data of D+i as the lagging data of D+i+1, then we do it recursively to the 7th day, so the result of D+7 may lead to a high error due to the accumulation of errors across each daily prediction. As as result, we got the graphs below. Additionally, we do the hindcast 1 day to see the performance of our model daily.

![alt text](https://raw.githubusercontent.com/WasuWata/mlfs-book/main/docs/air-quality/assets/img/pm25_forecast.png)
![alt text](https://raw.githubusercontent.com/WasuWata/mlfs-book/main/docs/air-quality/assets/img/pm25_hindcast_1day.png)

## Conclusion
To be concluded, we can produce the model to predict and see the feature importance with the relatively good accuracy (MSE = 55.905/R2 = 0.3998), however, we personally think that the feature is not enough. For the weather data, we have temperature, wind, and precipitation which indicate the advection of the PM2.5 particles. For the air quality data, we have lagging1/2/3 data which indicate the previous PM2.5 level. There is nothing as the indicator of the source of PM2.5 level, if we have more data about it, the result of the model might be much more better.
