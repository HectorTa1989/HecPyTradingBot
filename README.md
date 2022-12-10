# HecPyTradingBot
## Visual Strategy Development
Visual strategy creation is an important part of quick and efficient development, as it allows you to easily debug and adjust ideas by looking at how signals develop and change with shifts in the market.

I find Python to be a good language for this type of data-science, as the syntax is easy to understand and there are a wide range of tools and libraries to help you in your development. On top of this, the Alpaca Python API gives us an easy way to integrate market data without having to implement a new API wrapper*.

For data processing and plotting, I recommend using TA-Lib and Matplotlib. Ta-Lib provides a nice library to calculate common market indicators, so that you don’t have to reimplement them yourself; while matplotlib is a simple yet powerful plotting tool which will serve you well for all types of data visualization.

Here’s a code snippet of an example framework script I put together (full scripts at the end of this section).
![image](https://user-images.githubusercontent.com/31132150/206829525-80eb43f7-9a2d-4d2b-8f06-a2bdff806a68.png)

The script adds a simple moving average cross strategy against a few different trading symbols to give a small sample of the how it might fair in live trading. This allows for a first sanity check for a new strategy’s signals. Once a strategy has passed visual inspection you can run it through a backtesting tool, such as the one discussed in the “Algo Trading for Dummies” series.

You may even wish to add visual markers to each simulated trade and, for a move advanced strategy, the indicators the signal was derived from. This can make it even easier to analyze the weaknesses of a signal set so that you can adjust its parameters.

## Simple Trading Bot
Once you’ve moved past the backtesting stage, you’ll need a simple trading framework to integrate your strategies for live testing. This can then be run on a paper trading account to test the signals against a live data feed.

This is an important step in development, as it tests whether the strategy has been over-fit to its dataset. For example, a strategy could easily be tuned to perfectly trade a specific symbol over a backtesting period. However, this is unlikely to generalize well to other markets or different time periods — leading to ineffective signals and losses.

As such, you’ll want to a simple way to test your strategies in a staging environment, before committing any money to them with a real trading account. This is both for testing the strategy and the implementation, as a small bug in your code could be enough to wipe out an account, if left unchecked.

Here’s another example snippet of a trading bot which implements the moving average cross strategy (full script at end of this section).

![image](https://user-images.githubusercontent.com/31132150/206829576-8bad2ab9-df16-48d3-80de-57bcd42a50d1.png)

To make this into a full trading bot you could choose to either add a timed loop to the code itself or have the whole script run on a periodic schedule. The latter is often a better choice, as an exception causing an unexpected crash would completely stop the trading bot if it were a self contained loop. Where as, a scheduled task would have no such issue, as each polling step is a separate instance of the script.

On top of this, you’ll probably want to implement a logging system, so that you can easily monitor the bot and identify any bugs as it runs. This could be achieved by adding a function to write a text file with any relevant information at the end of each process.

Once you have a working strategy, the Alpaca API should make it easy to expand your trading bot into a full production system, allowing you to start trading quickly.
