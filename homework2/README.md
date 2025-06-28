*Second homework assignment*
Based on the notebooks in the time_series_forecasting folder, perform the three following tasks:

1. *Exercise Description* : Extend the code in notebook 7_multi_model_plotting to read the forecast results from all trained models and plot all curves in one panel. Make sure that your code can be re-used if you make forecasts for other stations or time episodes.

The exercise was to create a plotting function that is able to plot results from different model in a single panel. Since no concrete requirements towards the format of the data/models or the function itself was given, the following assumptions were made:

    1. All models were evaluated on the same time-series. The relevant sample (both context and ground truth) are saved as a single timeseries. This way, it does not matter what station the data is from and it is made sure that the context/ground-truth actually match the saved predictions.
    
    2. Limited assumptions were made towards the context-length, nor the prediction-window. It is just assumed that the predicted timepoints are a subset of the total timepoints of the whole time-series. Furthermore, the context-windows from which the predictions were obtained must share the same $0$-th timepoint (i.e. the length of the context-window and prediction-window is variable, but the plotting funciton does not support shifting the windows within the given time-series). Thus, we can dynamically display different models evaluated with different prediciton-windows for the same sample. Say our time-series evaluated on goes until timepoint $t^*$. The predictions $p$ must be saved together with their respective time-points $t_p$. Then $0 < min(t_p)$ and $max(t_p) < t^*$.

    3. If the training data was normalized, it is assumed that the saved predicions are already inverse scaled. The given time-series should be unnormalized.

    4. Obviously, the given timeseries and the predictions should be from the same variable.


The results from PatchTST were not obtained, since it was not possible to train PatchTST on the same data as the other models on Google Colab (unpaid). The given checkpoint was trained on another train-set, meaning it was not possible to rule out data leakage if evaluated on the same test-set as the other models. For this reason, the results were not obtained for the plot.

For the other models, the given data-pickles and trained checkpoints were used to obtain the predictions.

2. *Exercise Description*: Extend at least one of the models to input multivariate data. Download ozone data from TOAR (use the scripts in notebook 1). Copy the notebook with the model of your choice into a new notebook and extend the code so that temperazure and ozone data are used as inputs. The goal is to forecast ozone concentrations, you don't need to output temperature.

*Obtain the multi-variate data*: To obtain the multi-variate data, the code from notebook 1 was used. However, when fetching the data with multiple inputs, the code merging the individual time-series into a single dataframe seems to result in duplicates for the same time-point (i.e. datetime column). This resulted in problems when trying to split into the individual sample sequences. This issue could be mitigated by first interpolating the data and then dropping the duplicates. This, however, is just a work-around to be able to continue on this task. 

*Train LSTM*: The LSTM was chosen to be the model to be trained. To adapt the code to the multi-variable data, since the model was implemented in tensorflow, only the initialization of the model needed to be changed. Apart from that, some data-handling was adapted for more simple and readable code. The model was still trained on only 5 epochs, which did not result in very good results based on the single visualized sample. Over the whole test-dataset, a root mean-squared-error of 0.7 was achieved. 

3. *Exercise Description*: In reality, you will often have forecasts of weather variables (here temperature) available, so you can use future temperature values to forecast the ozone concentrations. Make another copy of your multivariate notebook and adjust the code accordingly. Use your multi-model plotter to compare the results from tasks 2 and 3.

Two different approaches were explored in this exercise. The approaches are explained in depth in the relevant notebook. Both approaches did not require any changes to the architecture or training procedure of the LSTM, instead, only the data-preparation needed to be adapted. 

Note, these two approaches were the only ones (within constraints of time and work) that came to mind. 

Both approaches improve on the RMSE score on the whole test-set from task two, where Approach 1 achieved a score of 0.6740 and Approach two improved on this with a score of 0.6370. This is also clearly visible the in the visualization for a single sample, shown in the notebook for Task 1.

Thus, it seems both approaches were valid and the future temperature data was successfully used by the model to better predict the ozone data.
