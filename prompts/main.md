TASK: Build a High-Performance Python Backtesting Engine for Brute-Force Indicator Strategy Search

Objective
Create a high-performance Python backtesting engine that brute-force tests a very large number of indicator parameter combinations (target ≈ 100,000+ combinations) on Nifty 15-minute historical data. The goal is to automatically discover potentially profitable trading strategies using combinations of EMA, RSI, and moving averages.

The system must be designed for efficiency and scalability so that it can test large numbers of strategies quickly.

Data Source
Historical Nifty 15-minute OHLC data is stored inside a folder named "data".

Assume the dataset contains the following columns:

timestamp
open
high
low
close
volume (optional)

The script should automatically load the dataset and prepare it for backtesting.

Indicators to Test

EMA
Period range: 5 to 200

RSI
Period range: 5 to 95

Moving Averages
Allowed types: SMA and EMA
Minimum moving averages per strategy: 0
Maximum moving averages per strategy: 4
Maximum MA period: 200

The engine must generate all valid combinations of these indicators within the constraints.

Important Constraint
The system should try every valid combination.
If the total combinations are below 100,000 that is acceptable.
If combinations exceed 100,000, sampling or batching may be used.

Entry Conditions

The system should automatically generate entry logic based on indicator relationships, including:

EMA crossover
Price above/below EMA
RSI above/below thresholds
Moving average crossover
Price crossing moving average

Each strategy must define a clear entry condition.

Exit Conditions

The system must also test exit logic combinations using indicators such as:

EMA cross exit
RSI exit thresholds (overbought / oversold)
Moving average crossover exit
Indicator reversal signals

Different exit rules must be tested for each strategy configuration.

Backtesting Rules

Initial Capital
Initial capital should be calculated as:

Initial Capital = 2 × First Trade Entry Price

Trade Execution
Trades should be simulated sequentially across the historical dataset.

Assume one position at a time (no pyramiding).

Performance Metrics

For each parameter combination calculate:

Absolute Returns
Sharpe Ratio
Absolute Maximum Drawdown
Average Points Per Trade
Average Profit
Average Loss
Profit Factor
Total Trades
Percent Profitable

System Architecture Requirements

The engine must be optimized for speed and scalability.

Use the following techniques:

Vectorized calculations using pandas and numpy
Pre-compute indicators to avoid recalculation
Parallel processing using multiprocessing or joblib
Batch processing of strategy combinations
Efficient memory usage to handle large search spaces

Optional but preferred optimizations:

Numba acceleration
Strategy evaluation caching
Checkpoint saving for long runs

Result Storage

Results must be exported into a CSV file called:

results.csv

Each row must contain:

Parameters (JSON format with indicator names and values)
Absolute Returns
Sharpe Ratio
Absolute Max Drawdown
Average Points Per Trade
Average Profit
Average Loss
Profit Factor
Total Trades
Percent Profitable

Example parameter JSON format

{
"ema_period": 20,
"rsi_period": 14,
"rsi_entry": 55,
"ma_1": {"type": "SMA", "period": 50},
"ma_2": {"type": "EMA", "period": 100},
"exit_rule": "ema_cross"
}

Logging and Progress Tracking

The script must print progress logs such as:

Total combinations generated
Current combination being tested
Estimated remaining time
Strategies processed per second

Final Output

The script should generate:

results.csv containing performance metrics for every tested strategy.

Goal

The objective is to brute-force search for profitable indicator combinations on Nifty 15-minute data by evaluating a large number of strategies automatically and ranking them by performance metrics such as Sharpe Ratio and Profit Factor.
