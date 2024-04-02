# Forecasting Using Custom Model Prophet in Trendz Analytics

## **Overview** 

Trendz Analytics is a powerful tool for time-series forecasting, offering a user-friendly interface for creating predictive models. With the integration of the custom model Prophet, users can leverage advanced analytics to forecast future trends based on historical data. This feature is particularly useful for businesses and researchers looking to make informed decisions.

## **Prophet Model:**
* Prophet (or “Facebook Prophet”) is an open-source library for univariate time series forecasting developed by Facebook.
* It implements an additive time series forecasting model that supports trends, seasonality, and holidays.
* The library provides automatic parameter management related to seasonality and data stationarity.

## **Steps**

1. **Login:**

    * The first step is to log in to Trendz Analytics using the same email and password as your ThingsBoard.cloud account.

2. **Load the Dataset:**

    * We are using a dataset from a sealing machine, which consists of the following columns: id, times, shift, status, Lower Vertical Sealing Temperature, Upper Vertical Sealing Temperature, Front/Right Horizontal Sealing Temperature, and Back/Left Horizontal Sealing Temperature.

    * Our objective is to forecast the future values of the Lower Vertical Sealing Temperature and Upper Vertical Sealing Temperature.

    * To load the dataset, you can choose to visualize the data in card, table, line, or other formats. In this tutorial, we will visualize the data in **Table** to view the Lower Vertical Sealing Temperature and Upper Vertical Sealing Temperature. Then, we will choose **Line** to visualize the data in a graph and make forecasts.


3. Forecasting with Custom Model:
    * Visualize data in **Line**

    * Enable Custom Prediction Model. First, add the required telemetry or calculated fields into the Trendz view. Then, open the Field settings dialog and select the **CUSTOM** option in the Prediction method dropdown.

        ![alt text](<../images/custom model/custom model.png>)

    * Write the Python Code. For a univariable model, write the Python code in the Model function section. Here’s an example python code for Prophet model:

        ``` import pandas as pd
            from prophet import Prophet

            print(f"inputX: {inputX}")
            print(f"inputY: {inputY}")
            print(f"outputX: {outputX}")

            df = pd.DataFrame()
            df['ds'] = pd.to_datetime(inputX, unit='ms')
            df['y'] = inputY

            model = Prophet()
            model.fit(df)

            future = pd.DataFrame()
            future['ds'] = pd.to_datetime(outputX, unit='ms')
            forecast = model.predict(future)

            outputY = forecast['yhat'].tolist()

            print(f"result: {outputY}")

            return outputY 
        ```

    * Set the **Prediction Unit** to days. Specify the **Prediction Range** (e.g., 1 days for the next 1 days)

        ![alt text](<../images/custom model/1day.png>)


4. Visualize the Prediction. After writing the code, you can **BUILD** a view to see the result of your prediction model.
    * Lower Vertical Sealing Temperature: 

       ![alt text](<../images/custom model/vb_temp_pred.jpg>)

    * Upper Vertical Sealing Temperature: 
    
        ![alt text](<../images/custom model/va_temp_pred.jpg>)



5. Evaluate the Forecast Model:
    * Use in-sample forecast: To evaluate the performance of the Prophet model, we use sample data divided into training and testing datasets. In our case, we use data from 5 days, where 4 days are used for training and 1 day for testing.
    * Manually evaluate the forecast model using Python in Google Colaboratory. The evaluation metrics we use to measure the model's performance are MAE, MSE, RMSE, and MAPE. Here are the evaluation metric results for the Prophet model:


        | Temperature | MAE | MSE | RMSE | MAPE |
        |:---:|:---:|:---:|:---:|:---:|
        | Lower Vertical | 33.75 | 1401.16 | 37.43 | 17.33 |
        | Upper Vertical | 32.08 | 1335.25 | 36.54 | 17.94 |


        Here's the link for more details [Metrics Evaluation in GColab ](https://colab.research.google.com/drive/1OpmMeYe5ffuTmcCarwr2lnVKRToyctD-?usp=sharing)

## Conclusion
By following these steps, you can leverage the Prophet model in Trendz Analytics for accurate time series forecasting. For more details, refer to the [Trendz Analytics Documentation ](https://thingsboard.io/docs/trendz/). 

