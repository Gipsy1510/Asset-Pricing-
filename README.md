# asset pricing – dividend–price ratio and return predictability

this folder contains the notebook `asset_pricing.ipynb`, developed as part of the master 2 *finance, technology and data* (ftd) program.

the goal is to study the informational efficiency of the stock market and the ability of the dividend–price ratio to predict future returns, using a classic monthly dataset in the spirit of robert shiller.

---

## 1. project overview

the notebook:

- imports and cleans a shiller-style stock market dataset  
- builds real (inflation-adjusted) prices and dividends  
- studies the **informational efficiency / martingale property** of returns  
- tests for **unit roots and stationarity** (adf tests)  
- checks **cointegration** between real prices and real dividends  
- constructs the **dividend–price ratio (`dp`)**  
- runs predictive regressions of future returns on `dp`

---

## 2. data

- **dataset**: monthly stock market data (prices, dividends, inflation, etc.), similar to the robert shiller database.  
- **frequency**: monthly  
- **main variables used**:
  - `p` – nominal price index  
  - `d` – nominal dividends  
  - `p_real`, `d_real` – real (inflation-adjusted) price and dividend  
  - `log_p_real`, `log_d_real` – logarithms of real price and dividend  
  - `dp` – dividend–price ratio: `log_d_real - log_p_real`  
  - `returns` – log returns on prices  
  - `r1_total_real` – 1-month ahead real total return (price change + dividend yield)

you may need to adjust the csv path inside the notebook so that it matches the location of your local file (for example, put the csv in the same folder as the notebook).

---

## 3. methods

the notebook applies several standard time-series tools:

1. **log returns and martingale property**
   - compute monthly log returns from real prices  
   - inspect basic summary statistics and plots  
   - test whether returns behave like a martingale difference (no linear predictability) using autocorrelation and simple diagnostic tools.

2. **stationarity and unit-root tests**
   - augmented dickey–fuller (adf) tests on:
     - `log_p_real`, `log_d_real` (levels)
     - first differences of these series  
   - typical finding: levels are non-stationary (i(1)), while first differences are stationary.

3. **cointegration between prices and dividends**
   - estimate a long-run relation:  
     `log_p_real = alpha + beta * log_d_real + error`
   - test stationarity of the residuals with an adf test.  
   - if residuals are stationary, prices and dividends are cointegrated, implying a stable long-run link between them.

4. **dividend–price ratio and predictability**
   - build `dp = log_d_real - log_p_real`.  
   - run predictive regressions of the form:

     \[
     r_{t+1} = a + b \cdot dp_t + \varepsilon_{t+1}
     \]

     and similarly for 1-month ahead total real returns.

---

## 4. requirements

the notebook is written in python and uses the following main libraries:

- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `statsmodels`
- `scipy`
- `plotly`
- `yfinance` (optional, for additional financial data)

install the dependencies with for example:

```bash
pip install pandas numpy matplotlib seaborn statsmodels scipy plotly yfinance

---

## 5. how to run

1. open a terminal in the root of the repository (or in this folder).
2. activate your virtual environment if you use one.
3. launch jupyter:

```bash
jupyter notebook
in the browser interface, open asset_pricing.ipynb.

run the cells from top to bottom
