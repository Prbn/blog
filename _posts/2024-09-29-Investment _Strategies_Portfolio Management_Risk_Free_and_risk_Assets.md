# Understanding the Balance Between Risk-Free and Risky Assets in Portfolio Management

## Introduction

When it comes to investing, one of the most critical decisions an investor faces is how to allocate their wealth between risk-free and risky assets. Risk-free assets, such as Treasury bills, offer stability and predictable returns, while risky assets, like stocks, come with the potential for higher returns but also higher risk. The proportion of wealth allocated to these two types of assets significantly influences the overall return and risk of a portfolio.

In this blog, we will explore how the return of a complete portfolio is calculated, how excess return and volatility play a role, and the importance of understanding the trade-off between risk and return. We’ll also delve into the Capital Allocation Line (CAL) and its relevance to portfolio management.

## 1. **Complete Portfolio’s Realized Return**

The return on a complete portfolio ($R_C$) is a weighted average of the returns from a risky asset ($R_P$) and a risk-free asset ($r_F$). The proportion of wealth allocated to the risky asset, denoted by $y_0$, determines how much of the portfolio's return is driven by the performance of the risky asset.

$$
R_C = y_0 \times R_P + (1 - y_0) \times r_F
$$

- **Risk-Free Asset Return**: Denoted by $r_F$, this is a constant return with virtually no risk.
- **Risky Asset Return**: Denoted by $R_P$, this return fluctuates based on market performance and carries a level of volatility.
- **Proportion of Wealth Allocated to the Risky Asset** ($y_0$): This proportion can be adjusted depending on the investor’s risk tolerance. A higher $y_0$ means more wealth is allocated to the risky asset, increasing potential returns as well as risk.

## 2. **Excess Return of the Complete Portfolio**

The **excess return** is the return earned beyond the risk-free rate, driven by the performance of the risky asset. The excess return of a portfolio is proportional to the wealth allocated to the risky asset ($y_0$) and the difference between the risky asset return and the risk-free rate.

$$
\text{Excess Return of Complete Portfolio} = y_0 \times (R_P - r_F)
$$

The more wealth invested in risky assets, the greater the potential excess return, but also the greater the exposure to risk.

## 3. **Risk and Volatility**

Volatility is a critical factor in portfolio management, as it represents the level of uncertainty or risk in the return of a portfolio. The volatility of the complete portfolio ($\sigma_C$) is directly proportional to the volatility of the risky asset ($\sigma_P$) and the proportion of wealth allocated to it.

$$
\sigma_C = y_0 \times \sigma_P
$$

As more wealth is allocated to risky assets, the portfolio's volatility increases. Conversely, risk-free assets have zero volatility, thus stabilizing the portfolio.

## 4. **Risk Premium and Sharpe Ratio**

- **Risk Premium**: This is the expected return above the risk-free rate. The risk premium for the complete portfolio is proportional to the risk premium of the risky asset and the amount invested in it.

  $$
  \text{Risk Premium of Complete Portfolio} = y_0 \times \text{Risk Premium of Risky Asset}
  $$

- **Sharpe Ratio**: A widely used metric to assess risk-adjusted returns. It is calculated as the risk premium divided by the portfolio's volatility.

  $$
  \text{Sharpe Ratio} = \frac{\text{Risk Premium}}{\text{Volatility}}
  $$

Interestingly, the Sharpe ratio remains constant for all portfolios that combine the same risky asset with a risk-free asset. This is a fundamental property of the **Capital Allocation Line (CAL)**.

## 5. **Capital Allocation Line (CAL)**

The Capital Allocation Line (CAL) represents the trade-off between risk and return for portfolios that combine risky and risk-free assets. The slope of the CAL is the Sharpe ratio of the risky portfolio, and every portfolio on this line has the same Sharpe ratio. The equation for the CAL is:

$$
E(R_C) = r_F + \frac{E(R_P) - r_F}{\sigma_P} \times \sigma_C
$$

Where:
- $E(R_C)$ is the expected return of the complete portfolio.
- $r_F$ is the risk-free rate.
- $E(R_P) - r_F$ is the risk premium of the risky asset.
- $\sigma_C$ is the standard deviation (risk) of the complete portfolio.

## Opinion: The Importance of Understanding the Risk-Return Trade-Off

In my opinion, understanding the dynamics between risk and return is essential for every investor. While it is tempting to chase higher returns by allocating more to risky assets, investors must be mindful of the accompanying risks. The Sharpe ratio and the CAL provide excellent frameworks for assessing whether the additional risk is justified by the potential reward. Investors who ignore these principles may find themselves exposed to unnecessary volatility, leading to suboptimal outcomes.

## 6. **Range of $y_0$ Values**

- **$y_0 = 1$**: All wealth is allocated to risky assets, and the portfolio's return mirrors the risky asset.
- **$0 < y_0 < 1$**: A balanced portfolio with wealth allocated to both risky and risk-free assets, yielding a return between the two.
- **$y_0 > 1$**: The investor borrows funds to invest more than 100% of their wealth in risky assets (leverage), amplifying both risk and return.
- **$y_0 < 0$**: The investor engages in short-selling, betting that the value of the risky asset will decline.

## 7. **Application Example**

Let’s consider an example:
- The risky asset has a return of 15% with a volatility of 22%.
- The risk-free rate is 7%.
- The Sharpe ratio of the risky portfolio is:

  $$
  \text{Sharpe Ratio} = \frac{15\% - 7\%}{22\%} = 0.36
  $$

Suppose an investor allocates 30% of their wealth to the risky asset ($y_0 = 0.3$). The expected return of the complete portfolio would be:

$$
E(R_C) = 7\% + 0.3 \times (15\% - 7\%) = 9.4\%
$$

The volatility of the complete portfolio would be:

$$
\sigma_C = 0.3 \times 22\% = 6.6\%
$$

## Conclusion: Balancing Risk and Return

Investors need to strike the right balance between risk and return by carefully adjusting their wealth allocation between risky and risk-free assets. The risk-return trade-off is a fundamental principle in portfolio management. Higher risk can lead to higher returns, but only when managed properly. The Sharpe ratio, excess return, and CAL provide essential tools for understanding and navigating this trade-off.

## Summary

- **Complete Portfolio’s Realized Return**: Calculated as a weighted average of risky and risk-free asset returns.
- **Excess Return**: Represents the return above the risk-free rate, determined by the proportion of wealth allocated to risky assets.
- **Risk and Volatility**: As more wealth is allocated to risky assets, portfolio volatility increases.
- **Sharpe Ratio**: A constant measure of risk-adjusted return, regardless of portfolio allocation along the CAL.
- **Capital Allocation Line (CAL)**: Illustrates the trade-off between risk and return for portfolios, with the Sharpe ratio as its slope.
