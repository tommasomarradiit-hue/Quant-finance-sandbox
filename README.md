# Quant-finance-sandbox

Quantitative finance tools, portfolio analytics and time series modeling.

## Projects
- Annualized volatility S&P500


- 📈 Portfolio Optimization & Efficient Frontier Tool (MPT)

A Python quantitative framework developed for portfolio optimization, risk management, and asset allocation modeling according to Harry Markowitz's **Modern Portfolio Theory (MPT)**.

The tool analyzes three assets with distinct risk/return profiles (**Apple, Gold, Bitcoin**), integrating two complementary methodologies:
1. **Stochastic Monte Carlo Simulation** with a *Long-Only* constraint ($w_i \ge 0$).
2. **Analytical Quadratic Optimization (`scipy.optimize`)** allowing *Short Sales* ($w_i \in \mathbb{R}$).

---

### 🛠️ Tech Stack & Dependencies

* **Python 3.x**: Core quantitative language.
* **Pandas & NumPy**: Historical data manipulation, vectorization, and matrix algebra ($\mathbf{w}^T \mathbf{\Sigma} \mathbf{w}$).
* **SciPy (`scipy.optimize`)**: Constrained quadratic minimization via the **SLSQP** algorithm (*Sequential Least Squares Programming*).
* **Matplotlib & Seaborn**: Data visualization and mapping of the solution space (Efficient Frontier).
* **yfinance**: Automated ingestion of adjusted historical market data.

---

### 📐 Mathematical Framework

#### 1. Matrix Formulation of Portfolio Variance
Portfolio variance is calculated using the annualized covariance matrix $\mathbf{\Sigma}$:

$$\sigma_p^2 = \mathbf{w}^T \mathbf{\Sigma} \mathbf{w}$$

Where:
* $\mathbf{w}$: Column vector of asset weights.
* $\mathbf{\Sigma}$: Annualized Covariance Matrix of returns.
* **Expected Return:** $E(R_p) = \mathbf{w}^T \mathbf{R}$

#### 2. Analytical Optimization Constraints (SLSQP)
For each target return level $R_{\text{target}}$, the algorithm solves the following optimization problem:

$$\min_{\mathbf{w}} \mathbf{w}^T \mathbf{\Sigma} \mathbf{w}$$

Subject to equality constraints:
1. **Budget Constraint:** $\sum_{i=1}^{N} w_i = 1 \quad \implies \quad \mathbf{w}^T \mathbf{1} - 1 = 0$
2. **Target Return:** $\mathbf{w}^T \mathbf{R} = R_{\text{target}} \quad \implies \quad \mathbf{w}^T \mathbf{R} - R_{\text{target}} = 0$

> **Short Selling Note:** Unconstrained lower bounds ($w_i \in \mathbb{R}$) allow negative weights ($w_i < 0$), enabling short positions and financial leverage to extend the frontier beyond the highest-yielding individual asset (Bitcoin).

#### 3. Performance Metric (Sharpe Ratio)
$$\text{Sharpe Ratio} = \frac{E(R_p) - R_f}{\sigma_p}$$

---

### 📊 Methodological Comparison

| Feature | Monte Carlo Simulation | SciPy Optimization (SLSQP) |
| :--- | :--- | :--- |
| **Operational Constraint** | Long-Only ($w_i \ge 0$) | Short Sales Allowed ($w_i \in \mathbb{R}$) |
| **Methodology** | Stochastic Sampling (5,000 iterations) | Analytical Optimization |
| **Return Domain** | Bounded by max individual asset ($w_{\text{BTC}} = 100\%$) | Unbounded (extended via short/leverage) |
| **Frontier Precision** | Discrete cloud approximation | Exact continuous parabolic curve |

---

### 🚀 Setup & Execution

  


