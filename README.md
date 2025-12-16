📈 LSTM Stock Price Prediction Model (Kaggle Project)This project implements a Long Short-Term Memory (LSTM) Recurrent Neural Network (RNN) to predict the closing price of individual stocks listed on the National Stock Exchange (NSE) or other major global markets. The prediction is based solely on historical price data.🚀 How to Use the CodeThis code is designed to be run within a Kaggle Notebook or any standard Python environment (like Jupyter Notebook, Colab, or local IDE).PrerequisitesEnvironment: A Python environment (e.g., Kaggle, Colab, or local setup).Libraries: The following Python libraries are required:Bash!pip install yfinance pandas numpy tensorflow matplotlib
1. The Core Prediction FunctionThe entire process—data download, preprocessing, model training, and prediction—is encapsulated in the function predict_stock_price_inr_and_plot_data.ParameterDescriptionDefaulttickerThe stock symbol (e.g., 'INFY.NS', 'BHARTIARTL.NS').(Must be specified)prediction_daysThe number of previous trading days the LSTM looks at to predict the next day's price.60epochsThe number of times the model sees the entire training data. (More is generally better, but takes longer).15batch_sizeThe number of samples processed before the model is updated.322. Making a PredictionTo run the model, you only need to call the function with the desired ticker.Example: Predicting Bharti Airtel (NSE)Python# Ticker for Bharti Airtel on the NSE
airtel_ticker = 'BHARTIARTL.NS' 

# Run the analysis, which trains the model and provides a prediction for the next day.
actual_prices, predicted_prices, stock_name = predict_stock_price_inr_and_plot_data(
    ticker=airtel_ticker, 
    epochs=15, 
    prediction_days=60
)
3. Visualizing the PerformanceThe function returns the actual and predicted prices for the test period, allowing you to generate a comparison plot.Pythonimport matplotlib.pyplot as plt

# Check if data was returned successfully
if actual_prices is not None and predicted_prices is not None:
    plt.figure(figsize=(16, 7))
    
    plt.plot(actual_prices.index, actual_prices.values, color='blue', label=f'Actual {stock_name} Price')
    plt.plot(predicted_prices.index, predicted_prices.values, color='red', label=f'Predicted {stock_name} Price')
    
    plt.title(f'{stock_name} Price Prediction (LSTM Model)')
    plt.xlabel('Date')
    plt.ylabel(f'Price (₹)')
    plt.legend()
    plt.grid(True)
    plt.xticks(rotation=45)
    plt.tight_layout()
    plt.show()
⚙️ What to Edit to Predict a New StockTo adapt the code for any stock or financial instrument, you only need to change the ticker symbol and, optionally, the hyperparameters.A. Ticker Symbol (Mandatory)The ticker format depends on the stock's listing exchange:MarketTicker FormatExampleIndian Stocks (NSE)SYMBOL.NSTCS.NS, RELIANCE.NSIndian Indices (NSE)^NSEINifty 50US Stocks (NYSE/NASDAQ)SYMBOLAAPL, GOOGForexPAIR=XEURUSD=XTo predict a new stock, simply replace the ticker variable:Python# Change this line:
new_ticker = 'HDFCBANK.NS' # Example: HDFC Bank

# Then call the function:
actual, predicted, name = predict_stock_price_inr_and_plot_data(ticker=new_ticker)
B. Hyperparameters (Optional)Adjusting these parameters will force the model to retrain and may improve accuracy:ParameterWhat to EditEffect on ModelepochsIncrease the value (e.g., from 15 to 50).The model trains longer, potentially finding better patterns, but risks overfitting.prediction_daysChange the value (e.g., from 60 to 30).Changes the historical lookback window. A smaller value makes the prediction more sensitive to recent changes.Data Features(Advanced: requires code change)Adding features like RSI or MACD provides the model with more context than just price.
