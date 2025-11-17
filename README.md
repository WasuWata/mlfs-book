# PM2.5 Forecasting of Stockholm St. Eriksgatan 83
O'Reilly book - Building Machine Learning Systems with a feature store: batch, real-time, and LLMs


## Project Description
In this project, we use weather data (Open-meteo) and PM2.5 data (AQICN) of selected street, in order to train the XGBoost model and forecast the future PM2.5 level of the sensor. In addition, we utilize the Huggingface Gradio to create the dashboard, to visualize the prediction, feature importance, and performance of the model.


[Dashboards for PM2.5 Prediction](https://huggingface.co/spaces/wasu2704/Iris)




# Feature Selection
We selected total seven features, four from weather data and another three creating from PM2.5 data, according to the table below.
| Features | Description |
| -------- | ----------- |
|`temperature_2m_mean`||
|||
|||
|||
|||
|||
|||

See [tutorial instructions here](https://docs.google.com/document/d/1YXfM1_rpo1-jM-lYyb1HpbV9EJPN6i1u6h2rhdPduNE/edit?usp=sharing)
    # Create a conda or virtual environment for your project
    conda create -n book 
    conda activate book

    # Install 'uv' and 'invoke'
    pip install invoke dotenv

    # 'invoke install' installs python dependencies using uv and requirements.txt
    invoke install


## PyInvoke

    invoke aq-backfill
    invoke aq-features
    invoke aq-train
    invoke aq-inference
    invoke aq-clean



## Feldera


pip install feldera ipython-secrets
sudo apt-get install python3-secretstorage
sudo apt-get install gnome-keyring 

mkdir -p /tmp/c.app.hopsworks.ai
ln -s  /tmp/c.app.hopsworks.ai ~/hopsworks
docker run -p 8080:8080 \
  -v ~/hopsworks:/tmp/c.app.hopsworks.ai \
  --tty --rm -it ghcr.io/feldera/pipeline-manager:latest

