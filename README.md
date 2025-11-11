# Portfolio Optimization using LSTMs and a Genetic Algorithm

###  **Work in Progress** ️
> This is an active research and development project. The code, models, and documentation are currently under development, incomplete, and subject to frequent changes.

## 1. Project Overview

This project explores advanced computational methods for financial portfolio optimization. We are developing and comparing two distinct approaches that leverage Recurrent Neural Networks (LSTMs) to capture complex, non-linear time-series dynamics in financial markets.

The goal is to move beyond the static, linear assumptions of traditional models (like Modern Portfolio Theory) by creating models that can adapt to changing market regimes.

## 2. Methodology: Two Competing Models

We are building two separate, competing models to solve the optimization problem.

### Model 1: The "Asset-Level" LSTM (End-to-End)

This model takes a "bottom-up" approach by learning directly from individual assets.

* **Concept:** This is an end-to-end model. The LSTM is trained to look at the features of *all* assets and directly output the optimal portfolio weights.
* **Input Data:** A time-series tensor for *N* individual stocks.
* **Features (per asset):** For each asset, the network receives a vector of raw and engineered features, such as:
    * Raw Price
    * Historical Returns
    * Historical Volatility (Sigma)
* **Output:** A vector of *N* portfolio weights $(w_1, w_2, ..., w_n)$ that are constrained to sum to 1.
* **Training:** The network is trained to find weights that directly optimize a future-looking objective function, such as the (risk-adjusted) return of the portfolio.

---

### Model 2: The "Portfolio-Level" LSTM + Genetic Algorithm (Hybrid)

This model takes a "top-down," two-stage hybrid approach. It separates the task of *prediction* from the task of *optimization*.

* **Concept:** We hypothesize that searching for the optimal portfolio from all possible combinations of assets ("brute-force") is computationally intractable.
* **The Problem:** An "enormous portfolio" creates a search space that is too large to calculate exhaustively.
* **The Solution:** We use an LSTM to predict the *properties* of the ideal portfolio, and then use a Genetic Algorithm (GA) as an efficient *search tool* to find the portfolio that matches those properties.

#### Step A: The LSTM (The "Oracle")
The LSTM's job is not to pick stocks, but to predict the *characteristics* of the best possible portfolio for the next time period, based on current market conditions.

* **Input Data:** Time-series data of market-wide factors or the performance of different, pre-defined portfolio strategies.
* **Output (Prediction):** A vector of *target properties*. For example:
    * `Target_Expected_Return = 0.08`
    * `Target_Expected_Volatility = 0.12`
    * `Target_Max_Drawdown = -0.05`

#### Step B: The Genetic Algorithm (The "Searcher")
Once the LSTM provides the "target," the Genetic Algorithm's job is to find the *actual* portfolio weights that create a portfolio with those properties.

* **Search Space:** random possible portfolio weight combinations.
* **Process:** The GA runs for a set number of generations, "evolving" a population of random portfolios (through crossover and mutation) until it finds a "fittest" individual that best matches the LSTM's target.

This hybrid approach allows us to efficiently search a massive, non-linear problem space without calculating every possible outcome.

## 3. Repository Structure (Planned)
