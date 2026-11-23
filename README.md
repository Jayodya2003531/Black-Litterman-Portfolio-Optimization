# Black-Litterman-Portfolio-Optimization
Black-Litterman-Portfolio-Optimization/
├── README.md
├── data/
│   └── CS3_Black_Litterman_Model.xlsx    # Renamed from CS3_17349 (1).xlsx for clarity
├── docs/
│   └── Black_Litterman_Study_Guide.pdf   # Your theoretical derivation & notes
└── images/                               # Exported charts from your Excel Dashboard

# 📊 The Black–Litterman Portfolio Optimization Model

A quantitative finance case study implementing the **Black–Litterman (BL) Asset Allocation Model** across 10 major U.S. large-cap equities. Developed as part of **FM3015 — Case Study for Finance** (Department of Mathematics, University of Colombo).

---

## 📌 Project Overview
Classical Markowitz Mean-Variance Optimization is notoriously sensitive to expected-return inputs—small estimation errors often produce extreme, concentrated, or unintuitive portfolio weights. 

This project overcomes that limitation by:
1. **Reverse-Engineering Market Equilibrium ($\Pi$):** Inferring implied returns from observable market-capitalization weights ($w_m$) and S&P 500 risk-aversion metrics ($\lambda$).
2. **Bayesian View Integration:** Blending the market equilibrium prior with 5 absolute and relative investor views ($P, Q$) weighted by view uncertainty ($\Omega$).
3. **Constrained Portfolio Optimization:** Maximizing the Sharpe Ratio using the posterior Black–Litterman expected returns ($\mu_{BL}$).

---

## 🧮 Mathematical Framework

* **Market Equilibrium Returns:** $\Pi = \lambda \Sigma w_m$
* **Risk-Aversion Coefficient:** $\lambda = \frac{E(R_m) - R_f}{\sigma_m^2}$[cite: 1]
* **View Uncertainty Matrix:** $\Omega = P(\tau \Sigma)P^T$[cite: 1]
* **Black–Litterman Posterior Returns:** 
  $$\mu_{BL} = \left[ (\tau\Sigma)^{-1} + P^T\Omega^{-1}P \right]^{-1} \left[ (\tau\Sigma)^{-1}\Pi + P^T\Omega^{-1}Q \right]$$[cite: 1]

---

## 📈 Asset Universe & Key Parameters
* **Historical Data Window:** May 13, 2023 – May 13, 2026 (Daily log returns)
* **Equities Analyzed (10):** NVIDIA, Apple, Amazon, Alphabet, Meta Platforms, Johnson & Johnson, JPMorgan Chase, Coca-Cola, Exxon Mobil, and Procter & Gamble
* **Total Market Cap:** $20,384.20 Billion
* **Risk-Free Rate ($R_f$):** 4.43% (U.S. Treasury yield proxy)
* **Scalar ($\tau$):** 0.025
* **Market Risk Aversion ($\lambda$):** 6.83 (derived from S&P 500 excess return of 15.08% and variance of 0.0221)

---

## 💡 Investor Views Encoded ($P$ and $Q$)
1. **Absolute View:** NVIDIA will generate an annual return of **40.0%**.
2. **Relative View:** Apple will outperform Coca-Cola by **10.0%**.
3. **Relative View:** Amazon will outperform Exxon Mobil by **12.0%**.
4. **Relative View:** Meta Platforms will outperform Johnson & Johnson by **8.0%**.
5. **Relative View:** Alphabet will outperform Procter & Gamble by **6.0%**.

---

## 🏆 Key Optimization Results

| Metric | Market-Cap Benchmark | Black–Litterman Optimal Portfolio |
| :--- | :---: | :---: |
| **Expected Annual Return** | 15.45% | **33.50%** |
| **Annualized Volatility (Risk)** | 10.23% | **27.71%** |
| **Sharpe Ratio** | — | **1.05** |

### Optimal Asset Allocation ($w_{BL}$)
* **NVIDIA:** 40.00%
* **Apple (AAPL):** 35.78%
* **Alphabet (GOOGL):** 16.07%
* **Amazon (AMZN):** 4.30%
* **JPMorgan Chase (JPM):** 1.97%
* **Procter & Gamble (PG):** 1.88%
* *(Meta, J&J, Coca-Cola, and Exxon Mobil received 0.00% allocation under long-only constraints)*

---

## 🛠️ Tools & Methodology
* **Microsoft Excel:** Matrix multiplication (`MMULT`, `MINVERSE`, `TRANSPOSE`), annualized covariance estimation, and Solver optimization[cite: 1].
* **Quantitative Finance Theory:** Linear-Gaussian Bayesian conjugacy and reverse optimization[cite: 1].
