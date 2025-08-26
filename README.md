# Pricing-Swaptions-with-the-Black-Derman-Toy-BDT-Model
PRICING SWAPTION 
# Swaption Pricing with the Black–Derman–Toy Model

A Python implementation of swaption pricing using the Black–Derman–Toy (BDT) short-rate model. 
Includes calibration, valuation, visualization, and inline validation tests.
## Table of Contents
- [Overview](#overview)
- [The Black–Derman–Toy Model](#the-blackdermantoy-model)
- [Swaption Pricing Mechanics](#swaption-pricing-mechanics)
- [Results](#results)
- [Visualizations](#visualizations)
- [How to Run](#how-to-run)
- [Project Structure](#project-structure)
- [Next Steps](#next-steps)
## Overview
This project demonstrates how to price **payer** and **receiver swaptions** using the **Black–Derman–Toy (BDT)** short-rate model.  

The main objectives were:
- Calibrate a BDT tree to a given 10-period spot rate curve.
- Price a European payer swaption and receiver swaption expiring at t=3.
- Visualize both the short-rate tree and the option value trees.
- Validate results with inline tests and arbitrage checks.
## The Black–Derman–Toy Model
The BDT model is a one-factor short-rate model where the short rate evolves on a recombining binomial tree:

r_{n,j} = a_{n+1} * exp(b * j)

- **Calibration**: a_n parameters are chosen so model zero-coupon prices match market discount factors.
- **Parameter b**: controls volatility of rates.
- **Use**: Once calibrated, the tree can price bonds, swaps, swaptions, and other IR derivatives.
## Swaption Pricing Mechanics
A swaption is an option on a swap:
- **Payer Swaption**: right to pay fixed, receive floating.
- **Receiver Swaption**: right to receive fixed, pay floating.

Pricing steps:
1. Calibrate BDT to fit the market yield curve.
2. At expiry nodes, compute the value of the underlying swap.
3. Payer payoff = max(SwapValue, 0).
   Receiver payoff = max(-SwapValue, 0).
4. Backward-induct values to time 0 using the short-rate tree.
## Results
- Payer Swaption Price: **\$4,102**
- Receiver Swaption Price: **\$3,911**
- Calibration error: < 1e-12 (model curve ≈ market curve)

Interpretation:
- Payer swaption more valuable than receiver under an upward-sloping yield curve.
- Results consistent with put–call parity (payer + receiver = forward swap value).
## Visualizations
- **Short-Rate Tree Heatmap**
- **Payer Swaption Value Tree**
- **Receiver Swaption Value Tree**

<p align="center">
  <img src="images/short_rate_tree.png" width="400">
  <img src="images/payer_swaption.png" width="400">
  <img src="images/receiver_swaption.png" width="400">
</p>
## How to Run
Clone the repo and install requirements:

```bash
git clone https://github.com/your-username/bdt-swaption.git
cd bdt-swaption
pip install -r requirements.txt
jupyter notebook BDT_Swaption_Notebook.ipynb
## References
- Black, F., Derman, E., Toy, W. (1990). *A One-Factor Model of Interest Rates and Its Application to Treasury Bond Options.*
- Hull, J. (Options, Futures, and Other Derivatives) — Ch. on Interest Rate Derivatives.
