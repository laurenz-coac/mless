# Timeseries analysis and forecasting based on TOAR data

The [Tropospheric Ozone Assessment Report (TOAR)](https://igacproject.org/activities/TOAR) is an international research activity to provide globally consistent information on the distribution and trends of the air pollutant ozone in the lower part of the atmosphere. Ozone impacts human health, vegetation, and climate, and TOAR provides the data and analyses to quantify the damage caused by ozone.

As the central data service, the [Jülich Supercomputing Centre](https://www.fz-juelich.de/en/ias/jsc) developed and operates the [TOAR Data Infrastructure](https://toar-data.fz-juelich.de/), which stores more than 420,000 time series of ozone and related chemical and meteorological variables. The TOAR data services use a REST API to allow users the download and analysis of custom-tailored datasets. Here, we will make use of this API to obtain and preprocess a couple of exemplary timeseries, which we then use as input data to various machine learning models to demonstrate various aspects around forecasting and interpolation.

The notebooks in this folder are structured as follows:
* 1_Download_Preprocess_data.ipynb: in this notebook, data are downloaded from the TOAR data infrastructure and repackaged so that it can be easily used in the machine learning models
* 2_Data_Analysis.ipynb: here, some visualisations and statistical analyses are demonstrated to gain insights into the data and inform decisions on how the data should be trated in the machine learning workflow
* 3_AutoRegressive_Models.ipynb: this notebook implements a classical statistical technique to establish a baseline against which the ML models can be compared
* 4_MLP.ipynb: here we  build a multilayer perceptron model for timeseries forecasting (**how about RNN?**)
* 5_LSTM.ipynb: this notebook demonstrates a more refined ML architecture for timeseries analysis and forecasting 
* 6_PatchTST.ipynb: finally, we demonstrate the use of a modern, transformer-based architecture for timeseries forecasting

Note that these notebooks focus primarily on monovariate forecasting tasks (i.e. one variable at a time), so they ignore possible correlations among different variables. Extension to multivariate models is left as an exercise to the reader.

Authors: Sindhu Vasireddy and Martin Schultz, Jülich, May 2025
