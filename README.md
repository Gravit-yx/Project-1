
# Algorithmic Trading using the Moving Average Crossover Strategy

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

Purpose:
Implements a crossover strategy using two moving averages:
Short Moving Average (Short_MA): Represents short-term trends.
Long Moving Average (Long_MA): Represents long-term trends.
Logic:
Generates a 'Signal' column:
1 when the short moving average is above the long moving average (buy signal).
-1 when the short moving average is below the long moving average (sell signal).
Parameters:
short_window: The period for the short moving average (default = 10 days).
long_window: The period for the long moving average (default = 50 days).
Output:
A DataFrame with additional columns for the moving averages and trading signals.



# Backtesting

Purpose:
Evaluates the strategy’s performance compared to the market returns.
Logic:
'Position' represents the strategy’s position for the day (shifted to avoid lookahead bias).
'Strategy_Return' calculates daily returns based on the position and price change.
'Cumulative_Strategy_Return' and 'Cumulative_Market_Return' calculate compounded returns for the strategy and the market, respectively.
Output:
A DataFrame with columns for the strategy’s and market's performance.


# Plotting results

Purpose:
Visualizes the strategy’s performance compared to the market.
Logic:
Plots cumulative returns for both the strategy and the market.
Parameters:
data: DataFrame containing cumulative returns.
ticker: The stock symbol for labeling the chart.
Output:
A matplotlib chart illustrating the backtesting results.

# Main function

Purpose:
Executes the functions in sequence for a selected stock ticker and date range.
Logic:
Retrieves stock data.
Applies the crossover strategy.
Backtests the strategy’s performance.
Plots the results.
Example Execution:
Uses Apple Inc. (AAPL) as the example ticker, with data spanning from January 1, 2018, to December 31, 2023.09
    
   
