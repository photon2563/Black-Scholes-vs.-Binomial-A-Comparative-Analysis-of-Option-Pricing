# Black Scholes vs Binomial Option Pricing Model:A Comparative Analysis

## Introduction
This project delves into the Black-Scholes Model (BSM) and the Binomial Option Pricing Model (BOPM), two foundational models in financial mathematics used for pricing options. It explores their underlying assumptions, mathematical frameworks, and practical implications, highlighting where theoretical constructs diverge from real-world market behavior. The notebook also provides a rigorous mathematical proof of the convergence of BOPM to BSM as the number of time steps increases, along with interactive simulations and comparative analysis with real-world data.

## Table of Contents

- [Introduction](#introduction)
- [Black-Scholes Model](#black-scholes-model)
  - [Assumptions and Implications](#the-constant-risk-free-rate-assumption)
  - [Mathematical Framework](#black-scholes-framework)
- [Binomial Option Pricing Model](#binomial-option-pricing-model)
  - [Assumptions and Implications](#discrete-time-price-movement)
  - [Mathematical Framework](#binomial-model-parameters)
- [BOPM Convergence to BSM](#bopm-convergence-to-bsm)
  - [Asymptotic Analysis of Parameters](#2-step-1-asymptotic-analysis-of-parameters)
  - [Log-Return Analysis](#3-step-2-log-return-analysis)
  - [Central Limit Theorem Application](#4-step-3-central-limit-theorem-application)
  - [Risk-Neutral Measure Adjustment](#5-step-4-risk-neutral-measure-adjustment)
  - [Option Pricing Convergence](#6-step-5-option-pricing-convergence)
  - [Rate of Convergence](#7-step-6-rate-of-convergence)
  - [Numerical Illustration](#8-numerical-illustration)
  - [Summary of Mathematical Results](#9-summary-of-mathematical-results)
- [Interactive Simulations](#interactive-simulations)
  - [BOPM vs. BSM Convergence Plotter](#plot-models)
  - [Option Price and Greeks Sensitivity](#plot-price-and-greeks)
- [Market Reality vs. Model Theories](#the-market-reality-vs-model-theories)
  - [Model Assumptions Do Not Reflect Reality](#1-model-assumptions-do-not-reflect-reality)
  - [Implied Volatility ≠ Constant Volatility](#2-implied-volatility--constant-volatility)
  - [Liquidity, Bid-Ask Spreads & Last Trade Noise](#3-liquidity-bid-ask-spreads--last-trade-noise)
  - [Dividend Impacts Aren't Covered in Vanilla Models](#4-dividend-impacts-arent-covered-in-vanilla-models)
  - [Early Exercise (American Options) vs. European Models](#5-early-exercise-american-options-vs-european-models)
  - [Human Behavior & Market Psychology](#6-human-behavior--market-psychology)
  - [Numerical Approximation Errors (particularly in BOPM)](#7-numerical-approximation-errors-particularly-in-bopm)
- [Resources](#resources)

## Black-Scholes Model

### Introduction
The Black-Scholes Model is a mathematical model used to price European-style options. Developed by Fischer Black, Myron Scholes, and Robert Merton, it revolutionized option pricing by providing a closed-form solution. The model is built on several key assumptions:

*   **Log-Normal Distribution**: Stock prices follow Geometric Brownian motion with constant drift and volatility.
*   **Constant Volatility**: The volatility of the asset remains constant throughout the option's life.
*   **Constant Risk-Free Rate**: The risk-free interest rate remains constant.
*   **No Dividends**: The underlying stock pays no dividends during the option's lifetime.
*   **Perfect Frictionless Market**: Assets can be traded continuously without transaction costs.
*   **European Exercise**: Options can only be exercised at expiration.
*   **No Transaction Costs**: No taxes, fees, etc.

### Formulae

#### Call Option Price
$C = S_0N(d_1) - Ke^{-rT}N(d_2)$

#### Put Option Price
$P = Ke^{-rt}N(-d_2) - S_0N(-d_1)$

Where:
$d_1=\frac{[ln(S_0/K) + (r + \sigma^{2}/2)T] }{ (\sigma\sqrt(T))}$

$d_2=d_1 - \sigma\sqrt(T)$

**Parameters:**
*   $C$ = Call option price
*   $P$ = Put option price
*   $S₀$ = Current stock price
*   $K$ = Strike price
*   $r$ = Risk-free interest rate
*   $T$ = Time to expiration
*   $σ$ = Volatility of the asset
*   $N(x)$ = Cumulative standard normal distribution function
*   $e$ = Euler's number
*   $ln$ = Natural logarithm

## Binomial Option Pricing Model

### Introduction
The Binomial Option Pricing Model (BOPM) is a discrete-time model that breaks down the life of an option into a series of time steps. At each step, the underlying asset's price is assumed to move either up or down by a specific factor. This model is more flexible than Black-Scholes, especially for American options.

### Formulae

*   **Up Factor**: $u = e^{\sigma\sqrt(\Delta t)}$
*   **Down Factor**: $d = e^{-\sigma\sqrt(\Delta t)}$ or $d = \frac{1}{u}$
*   **Risk-Neutral Probability**: $p = \frac{(e^{r\Delta t} - d)}{(u-d)}$

**Parameters:**
*   $u$ = Up factor
*   $d$ = Down factor
*   $\sigma$ = Volatility
*   $r$ = Risk-free rate
*   $T$ = Time to expiration
*   $n$ = Number of time steps

## BOPM Convergence to BSM

This section provides a rigorous mathematical derivation demonstrating how the Binomial Option Pricing Model converges to the Black-Scholes Model as the number of time steps approaches infinity. It covers asymptotic analysis of parameters, log-return analysis, application of the Central Limit Theorem, risk-neutral measure adjustment, and the convergence of option prices.

### Key Observations from Numerical Illustration
- Error decreases approximately as $1/\sqrt{n}$
- With 100 steps, error is less than 0.15%
- Convergence is rapid and practical for computational use

## Interactive Simulations

This section features Python code with interactive widgets to simulate and compare the Black-Scholes and Binomial Option Pricing Models. Users can adjust parameters like stock price, strike price, time to maturity, risk-free rate, and volatility to observe their impact on option prices and Greeks.

### BOPM vs. BSM Convergence Plotter
An interactive plot showing the convergence of BOPM prices to BSM prices as the number of steps in the binomial tree increases.

### Option Price and Greeks Sensitivity
Plots illustrating the sensitivity of option prices and their Greeks (Delta, Gamma, Vega, Theta, Rho) to various parameters for both Black-Scholes and BOPM.

## Market Reality vs. Model Theories

This section discusses the discrepancies between the theoretical assumptions of BSM and BOPM and the realities of financial markets. It covers topics such as:

1.  **Model Assumptions Do Not Reflect Reality**: How constant volatility, frictionless markets, and continuous trading assumptions diverge from actual market conditions.
2.  **Implied Volatility ≠ Constant Volatility**: The phenomenon of the volatility smile/skew, which contradicts the models' constant volatility assumption.
3.  **Liquidity, Bid-Ask Spreads & Last Trade Noise**: The impact of market microstructure on observed option prices.
4.  **Dividend Impacts Aren't Covered in Vanilla Models**: The effect of dividends on option pricing, which basic models often overlook.
5.  **Early Exercise (American Options) vs. European Models**: The limitations of BSM for American-style options and BOPM's potential for handling them.
6.  **Human Behavior & Market Psychology**: The role of sentiment and irrational behavior in option pricing.
7.  **Numerical Approximation Errors (particularly in BOPM)**: Challenges in achieving accuracy with discrete models.

## Resources

This section would list any external resources, academic papers, or further readings relevant to the Black-Scholes and Binomial Option Pricing Models.
