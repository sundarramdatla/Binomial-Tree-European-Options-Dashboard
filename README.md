# Binomial Tree Pricing Model for Derivatives

**[View the Model on Browser](https://sundarramdatla.github.io/Binomial-Tree-European-Options-Dashboard/)**

## 1. Introduction

The binomial tree model is a discrete time method for pricing derivatives by modeling probabilistic movements in the underlying asset's price. Using risk-neutral probabilities and backward induction, the tree determines the present value of an option from terminal payoffs.

The Cox Ross Rubinstein (CRR) model is a recombining variation on the binomial tree, where each upward movement followed by a downward movement leads to the same stock price as a downward movement followed by an upward movement. This symmetry reduces computational complexity from an exponentially growing tree to \(O(N^2)\) nodes.

## 2. Mathematical Methodology

**Stock Price Dynamics**

At each time step \(\Delta t=T/N\), the stock price moves by an up or down factor:

$$
u=e^{\sigma\sqrt{\Delta t}},\qquad d=e^{-\sigma\sqrt{\Delta t}}
$$

The stock price at a node with \(j\) downward movements after \(n\) steps is:

$$
S_{n,j}=S_0u^{n-j}d^j
$$

**Risk-Neutral Valuation**

Under the no-arbitrage assumption, the risk-neutral probability of an upward movement is:

$$
p=\frac{e^{r\Delta t}-d}{u-d}
$$

At maturity, European call and put payoffs are:

$$
C_T=\max(S_T-K,0)
$$

$$
P_T=\max(K-S_T,0)
$$

Option values are calculated through **backward induction**, discounting the risk-neutral expected value at each node:

$$
V_{n,j}=e^{-r\Delta t}\left[pV_{n+1,j}+(1-p)V_{n+1,j+1}\right]
$$

## 3. Convergence to Black–Scholes

As the number of time steps increases, the CRR binomial model converges to the continuous-time Black–Scholes solution for European options under the same modeling assumptions:

$$
\lim_{N\to\infty}V_{\mathrm{CRR}}(N)=V_{\mathrm{BS}}
$$

The interactive model visualizes this convergence across increasing tree depths, comparing numerical prices against analytical Black–Scholes benchmarks.

**Error Analysis**

Pricing accuracy is evaluated using:

$$
\text{Absolute Error}(N)=|V_{\mathrm{CRR}}(N)-V_{\mathrm{BS}}|
$$

The model also reports convergence behavior and pricing errors as the number of time steps changes.

## 4. Put–Call Parity

European call and put prices with identical strike prices and maturities satisfy:

$$
C+Ke^{-rT}=P+S_0
$$

This no-arbitrage relationship provides an additional validation of the binomial pricing methodology. The CRR model preserves put–call parity when both options are priced using consistent parameters.

## 5. Interactive Features

- Adjustable stock price, strike, volatility, risk-free rate, maturity, and binomial steps.
- Interactive recombining trees displaying stock prices and option values.
- European call and put pricing using risk-neutral backward induction.
- Convergence and absolute-error plots against analytical Black–Scholes prices.
- Risk-neutral probability, up/down factors, and pricing diagnostics.

---

**Developed by Sundarram Datla**
