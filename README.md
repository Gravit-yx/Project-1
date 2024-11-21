
Algorithmic Trading using the Moving Average Crossover Strategy
This project demonstrates a simple algorithmic trading strategy using the Moving Average Crossover technique. The strategy is implemented in Python, leveraging stock data obtained via the yfinance library. The goal is to test how this strategy performs compared to the market return over a given time period.


# Obtaining Previous Stock Data
Purpose: This function retrieves historical stock data for the specified ticker symbol and date range using the yfinance library.
Parameters:
ticker: The stock symbol (e.g., "AAPL" for Apple Inc.).
start_date: The start of the data range.
end_date: The end of the data range.
Output:
A DataFrame containing the stock's historical data with an additional column, 'Return', which represents daily percentage price changes.

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
    
   
