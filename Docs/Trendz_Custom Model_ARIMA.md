# Forecasting Using ARIMA Custom Model in Trendz Analytics

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

    * Enable the **Prediction** checkbox for the forecast field, as shown in the image marked with a green box then select **CUSTOM**. As you can see, there is script to define our custom ARIMA model here with (0,1,1) since its best and most optimal configuration for our model (used autoarima library).

        ![ARIMA Custom Configuration](<../img/ARIMA_Custom Configuration.png>)

    * You can see script that we used below:
      ```
      import pandas as pd
      from statsmodels.tsa.arima.model import ARIMA

      print(f"inputX: {inputX}")
      print(f"inputY: {inputY}")
      print(f"outputX: {outputX}")

      df = pd.DataFrame() 
      df['ds']= pd.to_datetime(inputX, unit='ms')
      df['y']= inputY

      model = ARIMA(df['y'], order=(1,1,1))
      model_fit = model.fit()

      start_index = len(df)
      end_index = start_index + len(outputX) - 1

      forecast = model_fit.predict(start=start_index, end=end_index)
      outputY = forecast.tolist()

      print(f"result: {outputY}")
      return outputY
      ```

    * Set the **Prediction Unit** to days

    * Specify the **Prediction Range** (e.g., 1 days for the next 1 days)

4. Visualize the Prediction. After writing the code, you can **BUILD** a view to see the result of your prediction model.
    * Lower Vertical Sealing Temperature: 

       ![alt text](<../img/VB_ARIMA_Custom.png>)

    * Upper Vertical Sealing Temperature: 
    
        ![alt text](<../img/VA_ARIMA_Custom.png>)
      
5. Evaluate the Forecast Model:
    * Use in-sample forecast: To evaluate the performance of the Prophet model, we use sample data divided into training and testing datasets. In our case, we use data from 5 days, where 4 days are used for training and 1 day for testing.
    * Manually evaluate the forecast model using Python in Google Colaboratory. The evaluation metrics we use to measure the model's performance are MAE, MSE, RMSE, and MAPE. Here are the evaluation metric results for the Prophet model:


        | Temperature | MAE | MSE | RMSE | MAPE |
        |:---:|:---:|:---:|:---:|:---:|
        | Lower Vertical | 33.88 | 2172.13 | 46.61 | 20.09 |
        | Upper Vertical | 37.67 | 2499.42 | 49.99 | 22.87 |


        Here's the link for more details [Metrics Evaluation in GColab](https://colab.research.google.com/drive/15g8zCkCk3VMAwUm4ffNqKUIpTZAc0wIt?usp=sharing)

## Conclusion
By following these steps, you can leverage the Prophet model in Trendz Analytics for accurate time series forecasting. For more details, refer to the [Trendz Analytics Documentation ](https://thingsboard.io/docs/trendz/). 
