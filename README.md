# Project-1
Algorithmic Tradin(using crossover stratergy)
import yfinance as yf
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Obtaining Previous Stock Data
def get_stock_data(ticker, start_date, end_date):
    data = yf.download(ticker, start=start_date, end=end_date)
    data['Return'] = data['Adj Close'].pct_change()
    return data

# Applying the specific strategy: Moving Average Crossover
def apply_strategy(data, short_window=10, long_window=50):
    data['Short_MA'] = data['Adj Close'].rolling(window=short_window).mean()
    data['Long_MA'] = data['Adj Close'].rolling(window=long_window).mean()
    data['Signal'] = 0
    data.loc[data['Short_MA'] > data['Long_MA'], 'Signal'] = 1
    data.loc[data['Short_MA'] <= data['Long_MA'], 'Signal'] = -1
    return data

# Backtesting
def backtest(data):
    data['Position'] = data['Signal'].shift(1)
    data['Strategy_Return'] = data['Position'] * data['Return']
    data['Cumulative_Strategy_Return'] = (1 + data['Strategy_Return']).cumprod()
    data['Cumulative_Market_Return'] = (1 + data['Return']).cumprod()
    return data

# Plotting results
def plot_results(data, ticker):
    plt.figure(figsize=(12, 6))
    plt.plot(data.index, data['Cumulative_Market_Return'], label="Market Return", color="blue")
    plt.plot(data.index, data['Cumulative_Strategy_Return'], label="Strategy Return", color="green")
    plt.title(f"Backtesting Results for {ticker}")
    plt.xlabel("Date")
    plt.ylabel("Cumulative Returns")
    plt.legend()
    plt.grid()
    plt.show()

# Main function
if __name__ == "__main__":
#Example
    ticker = "AAPL"  # Apple Inc.
    start_date = "2018-01-01"
    end_date = "2023-12-31"
    
   
