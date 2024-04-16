# Forecasting Using ARIMA Model in Trendz Analytics

## **Overview** 

Trendz Analytics provides built-in instruments for time-series prediction. All necessary tasks, including data filtering, normalization, and model training, are performed in the background. You can enable prediction for any fields, including calculated ones.

## **ARIMA Model**
* ARIMA (AutoRegressive Integrated Moving Average) is a widely used statistical method for time series forecasting.
* It models the next step in the sequence as a linear function of the observations and the lagged observations.
* ARIMA models can capture different types of trends, seasonality, and cyclic patterns in the data.
* The model parameters include the order of autoregression (p), differencing (d), and moving average (q), which need to be manually selected or optimized.
* Unlike Prophet, ARIMA requires manual intervention for parameter selection and may not handle seasonality and data stationarity automatically.

## **Steps**

1. **Login:**

    * The first step is to log in to Trendz Analytics using the same email and password as your ThingsBoard.cloud account.

2. **Load the Dataset:**

    * We are using a dataset from a sealing machine, which consists of the following columns: id, times, shift, status, Lower Vertical Sealing Temperature, Upper Vertical Sealing Temperature, Front/Right Horizontal Sealing Temperature, and Back/Left Horizontal Sealing Temperature.

    * Our objective is to forecast the future values of the Lower Vertical Sealing Temperature and Upper Vertical Sealing Temperature.

    * To load the dataset, you can choose to visualize the data in card, table, line, or other formats. In this tutorial, we will visualize the data in **Table** to view the Lower Vertical Sealing Temperature and Upper Vertical Sealing Temperature. Then, we will choose **Line** to visualize the data in a graph and make forecasts.

        ![alt text](<../images/default model/format data visualization.png>)

    * Data visualization with Table

        ![alt text](<../images/default model/vertical bawah 26-29 march.png>)

    * Data visualization with Line

        ![alt text](<../images/default model/vertical bawah 26-29 march line.png>)

3. Forecasting with ARIMA:
    * Visualize data in **Line**

    * Enable the **Prediction** checkbox for the forecast field, as shown in the image marked with a green box.

        ![ARIMA Default Configuration](<../img/ARIMA_Default Configuration.png>)

    * Select **ARIMA** as the prediction model or method.

    * Set the **Prediction Unit** to days

    * Specify the **Prediction Range** (e.g., 1 days for the next 1 days)

4. Forecast Results with ARIMA:

    * Visualize the Prediction. After finishing the configuration, you can **BUILD** a view to see the result of your prediction model.
    * Since we are having issues with default model result, prediction results is not available for now.
    * Lower Vertical Sealing Temperature.
    * Upper Vertical Sealing Temperature.

## Conclusion
By following these steps, you can leverage the Prophet model in Trendz Analytics for accurate time series forecasting. For more details, refer to the [Trendz Analytics Documentation ](https://thingsboard.io/docs/trendz/). 
