# Portfolio Optimization using LSTMs and Genetic Algorithms

### ⚠️ **Work in Progress** ⚠️
> This is an active research and development project. The code, models, and documentation are currently under development, incomplete, and subject to frequent changes.

## 1. Project Overview

This project explores the application of deep learning and evolutionary computation to the problem of financial portfolio optimization. Traditional methods (e.g., Modern Portfolio Theory) rely on static, linear assumptions about asset correlations and returns. This project aims to move beyond that by using **Long Short-Term Memory (LSTM) networks** to capture complex, non-linear time-series dynamics.

We are developing two distinct LSTM-based approaches, which will be optimized and compared using a **Genetic Algorithm (GA)**.

## 2. Core Methodology

Our research is split into two primary experimental models.

### Model 1: The "Asset-Level" LSTM

This model takes a "bottom-up" approach by analyzing individual assets to determine optimal portfolio weights.

* **Input Data:** Time-series data for *N* individual stocks.
* **Features:** For each asset, the network is fed a vector of raw and engineered features, such as:
    * Raw Price
    * Historical Returns (e.g., 1-day, 5-day)
    * Historical Volatility (Sigma)
    * Market Beta
    * (Other technical indicators as developed)
* **Architecture:** The LSTM processes these parallel time-series data streams.
* **Output:** The model's final layer is designed to output a set of *N* portfolio weights $(w_1, w_2, ..., w_n)$ that sum to 1. The network is trained to find weights that optimize a specific objective function (e.g., maximizing the future Sharpe Ratio).

### Model 2: The "Portfolio-Level" LSTM

This model takes a "top-down" approach. Instead of learning from individual stocks, it learns from the historical behavior of *entire portfolios*.

* **Input Data:** Time-series data representing the daily performance of *M* different, pre-defined portfolio strategies (e.g., "Equal Weight," "Minimum Volatility," "Max Sharpe," etc.).
* **Features:** The input vector for each time step will be the performance metrics of these *M* portfolios, such as:
    * Portfolio Daily Return
    * Portfolio Realized Volatility
    * Portfolio Max Drawdown
* **Architecture:** The LSTM learns the dynamic relationships and performance regimes of these different strategies.
* **Output:** The model's goal is to predict which strategy (or blend of strategies) will perform best in the next time period, effectively creating a "strategy-of-strategies" allocation.

## 3. Optimization with Genetic Algorithms

A simple, static model architecture is unlikely to be optimal. We will use a **Genetic Algorithm (GA)** as a high-level optimization layer to find the "fittest" model. The GA will be responsible for:

1.  **Hyperparameter Tuning:** Evolving the optimal architecture for both LSTMs (e.g., number of layers, neurons per layer, learning rate, and sequence length).
2.  **Feature Selection:** Evolving the ideal combination of input features for Model 1.
3.  **Model Selection:** Creating a "population" of trained models from both approaches and using the GA to find the champion model that demonstrates the most robust performance across a backtest.

## 4. Repository Structure (Planned)
