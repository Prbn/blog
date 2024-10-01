# Introduction to Investment Strategies: Capital Allocation to Risky Assets

## Introduction
Investing involves making crucial decisions about where to allocate your capital to achieve the best balance between risk and return. Two main types of assets are available to investors: **risk-free assets**, such as Treasury bills or savings accounts, and **risky assets**, including stocks, bonds, and real estate. While risk-free assets offer stability and guaranteed returns, they typically yield lower returns compared to the potential of risky assets, which come with uncertainty and market volatility. Understanding how to balance these asset classes according to your risk tolerance is key to constructing a sound investment portfolio.

In this blog post, we’ll explore the differences between risk-free and risky assets, discuss how personal risk preferences shape investment decisions, and dive into various portfolio allocation strategies. From calculating the realized return on a complete portfolio to understanding the impact of leverage and short selling, this guide will help you make informed decisions to optimize your investments.

## 1. **Risk-Free vs. Risky Assets**
Investors are often faced with a choice between two types of assets:

- **Risk-Free Assets**: These are investments like savings accounts or Treasury bills (T-bills) that offer guaranteed returns with virtually no risk of losing the initial investment. However, these assets generally offer **lower returns**.
- **Risky Assets**: These include stocks, bonds, real estate, and other investments that come with **higher risk** but offer the potential for **higher returns**. The risk involved comes from market fluctuations and the uncertainty of the asset’s future value.

## 2. **Personal Preferences and Risk Tolerance**
The decision to invest in risk-free or risky assets depends on the **investor's risk tolerance** and **preference for return**. Generally:
- **Older investors** tend to be more **risk-averse**. They prefer stable, lower-risk investments, such as risk-free assets, to preserve their capital.
- **Younger investors** are often more willing to take **higher risks**, as they have more time to recover from potential losses. They may allocate a larger portion of their wealth to risky assets to seek higher returns.

## 3. **Complete Portfolio’s Realized Return**
The **realized return of the complete portfolio** ($R_C$) is a weighted average of the returns from a risky asset ($R_P$) and a risk-free asset ($r_F$). The return on the complete portfolio is expressed as:

$$
\text{Complete Portfolio } (C) = \text{Riskey Assets } (P) + \text{Risk-free assets } (F)
$$
\
**Complete Portfolio Return Formula**

The return on the investor’s **complete portfolio** depends on how much is allocated to risky vs. risk-free assets. The return of the portfolio $R_C$ is a weighted average of the returns from the risky asset $R_P$ and the risk-free asset $r_F$. The proportion $y_0$ represents how much of the total wealth is allocated to the risky asset. The formula is:

$$
R_C = y_0 \times R_P + (1 - y_0) \times r_F
$$

Where:
- $y_0$ is the proportion of wealth allocated to the risky asset.
- $R_P$ is the return on the risky asset.
- $r_F$ is the risk-free rate.

- **Risk-Free Asset Return**: This is denoted by $r_F$, which is constant and has no risk.
- **Risky Asset Return**: This is denoted by $R_P$, which is uncertain and has some level of volatility.
- **Proportion of Wealth Allocated to the Risky Asset ($y_0$)**: This proportion can be adjusted based on the investor’s risk tolerance. If $y_0 = 1$, all the wealth is invested in the risky asset, while $y_0 = 0$ means all wealth is in the risk-free asset.
This formula helps to calculate the **expected return** of the complete portfolio depending on the allocation $y_0$.

## 4. **Wealth Allocation Between Risk-Free and Risky Assets**
The wealth allocation between risky and risk-free assets is represented by the variable **$y_0$**, which is the **proportion of wealth** invested in risky assets. The rest of the wealth is allocated to risk-free assets. Here’s how it works:

$$
y_0 = \left\{\begin{array}{}
0& : R_C = r_F\\
1& : R_C = R_P\\
(0,1)& : \text{Long position in portfolio P}\\
> 1 & : \text{Borrow & long in portfolio P}\\
< 0 & : \text{Short Postion in portfolio P}\\
\end{array}\right\}
$$

- **$y_0 = 0$**: \
This means the investor chooses to invest **none of their wealth** in risky assets. The entire portfolio is invested in risk-free assets, like a savings account or T-bills. In this case, the return on the portfolio will be equal to the return on the risk-free asset $r_F$.
- **$y_0 = 1$**: \
This means the investor allocates **all of their wealth** to risky assets. The entire portfolio will consist of risky investments like stocks. The return on the portfolio will be equal to the return on the risky asset $R_P$.
- **$0 < y_0 < 1$**: \
In this range, the investor splits their wealth between risky and risk-free assets. For example, if $y_0 = 0.5$, the investor allocates 50% of their wealth to risky assets and 50% to risk-free assets.
- **$y_0 > 1$**: \
The investor is borrowing money (leveraging) to invest **more than 100% of their wealth** in risky assets. This is a highly aggressive strategy that magnifies both potential returns and risks. For example, $y_0 = 1.5$ means the investor is borrowing additional capital equal to 50% of their own wealth to invest in risky assets.
- **$y_0 < 0$**: \
A negative value of $y_0$ indicates **short selling**. This means the investor is borrowing the risky asset, selling it, and expecting to repurchase it later at a lower price. In this scenario, the investor is betting against the risky asset.

### Example Scenarios:
1. **If $y_0 = 0$**:
   $$
   R_C = 0 \times R_P + (1 - 0) \times r_F = r_F
   $$
   In this case, the portfolio return is equal to the risk-free rate because all the wealth is in risk-free assets.

2. **If $y_0 = 1$**:
   $$
   R_C = 1 \times R_P + (1 - 1) \times r_F = R_P
   $$
   The entire portfolio return depends on the risky asset because all wealth is invested in risky assets.

3. **If $y_0 = 0.5$** (50% in risky assets and 50% in risk-free assets):
   $$
   R_C = 0.5 \times R_P + (1 - 0.5) \times r_F
   $$
   In this scenario, the portfolio return will be a blend of both risky and risk-free returns.

## 5. **Short Selling and Borrowing (Leverage)**
- **Short Selling, When $y_0 < 0$:** \
The investor is engaging in **short selling**. This means they are borrowing the risky asset and selling it at time 0, with the expectation of buying it back at a lower price at time 1. Short selling can generate a profit if the asset’s price declines, but it also carries the risk of unlimited losses if the price rises.
  4. **If $y_0 = -1$** (short selling in risky assets):
    $$
    R_C = -1 \times R_P + (1 + 1) \times r_F
    $$

- **Leveraging, When $y_0 > 1$:** \
The investor is borrowing money to invest more in risky assets than their available capital allows. This is called leveraging, and while it can amplify returns, it also increases the risk of loss if the market moves against the investor.
  4. **If $y_0 = 1.5$** (borrowing money to invest in risky assets):
    $$
    R_C = 1.5 \times R_P + (1 - 1.5) \times r_F
    $$

## 6. **Excess Return of the Complete Portfolio**
The **excess return** is the return earned beyond the risk-free rate. For the complete portfolio, the excess return is the proportion of wealth invested in the risky asset ($y_0$) times the excess return of the risky asset over the risk-free rate. This can be expressed as:

$$
\text{Excess Return of Complete Portfolio} = y_0 \times (R_P - r_F)\ \ .....(1)
$$

Thus, the complete portfolio’s excess return scales with how much is allocated to the risky asset.

## 7. **Risk and Volatility**
The **volatility** of the complete portfolio ($\sigma_C$) is proportional to the volatility of the risky asset ($\sigma_P$):

$$
\sigma_C = y_0 \times \sigma_P\ \ .....(2)
$$

This means that as you increase your allocation to risky assets, the overall risk of the portfolio increases. The risk of the risk-free asset is zero, so it doesn't contribute to the portfolio’s volatility.

## 8. **Expectation of the Final Value of a Portfolio**
The **final value of a portfolio** refers to the total worth of an investment at a future point in time, after considering returns earned on both risky and risk-free assets. In the context of a portfolio that mixes risky and risk-free assets, the **expected final value** is an estimate of what the portfolio will be worth at the end of the investment period, based on the expected return of the portfolio.

**Definition of Final Value of a Portfolio**: \
The **final value** of the portfolio at time $t = 1 $ (one year, for example) is the initial investment at time $ t = 0 $ multiplied by the portfolio’s realized return over the period. The general formula is:

$$
\text{Final Value of Portfolio} = \text{Initial Investment} \times (1 + R_C)
$$

Where:
- $ R_C $ is the **realized return** of the complete portfolio, which is a combination of risky and risk-free assets.
- The **initial investment** is the amount invested at the start (time $ t = 0 $).

**Expectation of the Final Value**: \
The **expectation** of the final value refers to the expected or average value of the portfolio at the end of the investment period, based on the expected return of the portfolio, rather than the realized return (since realized returns are unknown at the time of investment).

The formula for the **expected final value** is:

$$
\text{E(Final Value)} = I_0 \times (1 + E(R_C))
$$

Where:
- $\text{E(Final Value)}$ is the **expected Final Value** of the complete portfolio.
- $ E(R_C) $ is the **expected return** of the complete portfolio, which is a weighted average of the expected returns of the risky and risk-free assets.
- $I_0$ is the Initial Investment amount invested at the start.

## 9. **Risk-Return Trade-Off**
The main point is that **investors must decide how much risk they are willing to take**, balancing between risky and risk-free assets. More risk generally leads to higher expected returns, but it also increases the possibility of large losses. Investors use their personal preferences for risk and return to make decisions about their portfolio allocation, reflected in the value of $y_0$.

## 10. **Sharpe Ratio and Wealth Allocation**
When an investor allocates wealth between a **risky asset** and a **risk-free asset**, the **Sharpe ratio of the complete portfolio** remains **constant** and is **equal to the Sharpe ratio of the risky asset**. This means that the wealth allocation between risky and risk-free assets **does not affect** the Sharpe ratio.

**Sharpe Ratio of a Risk-Free Asset**: \\
The Sharpe ratio of a risk-free asset is **zero**, because the return on the risk-free asset is always equal to $r_F$, and its volatility ($\sigma$) is zero. Thus, risk-free assets do not contribute to risk-adjusted return in the Sharpe ratio sense.

## 11. **Risk Premium and Sharpe Ratio**
- **Risk Premium**: The **risk premium** of a portfolio is the expected return above the risk-free rate. For a complete portfolio, the risk premium is proportional to the risk premium of the risky asset:

  $$
  \text{Risk Premium of Complete Portfolio} = y_0 \times \text{Risk Premium of Risky Asset} \\
  \text{[Risk Premium]}_C = y_0 \times \text{[Risk Premium]}_P
  $$

  Where:
  - $\text{[Risk Premium]}_C$: Risk Premium of Complete Portfolio
  - $y_0$: wealth allocation between risky and risk-free assets
  - $\text{[Risk Premium]}_P$: Risk Premium of Risky Asset

- **Sharpe Ratio**: The **Sharpe ratio** measures the amount of risk premium earned per unit of risk (volatility):

  $$
  \text{Sharpe Ratio} = \frac{\text{Risk Premium}}{\text{Volatility}} 
  $$

Interestingly, **all complete portfolios that combine the same risky asset with a risk-free asset will have the same Sharpe ratio as the risky portfolio itself**, regardless of the allocation $y_0$. This is a key property of the **Capital Allocation Line (CAL)**.

## 12. **Capital Allocation Line (CAL)**
The **Capital Allocation Line (CAL)** represents the possible combinations of risky and risk-free assets, showing the trade-off between risk and return. The slope of the CAL is the **Sharpe ratio** of the risky portfolio, and every portfolio on this line shares the same Sharpe ratio. The equation for the CAL is:

$$
E(R_C) = r_F + \frac{E(R_P) - r_F}{\sigma_P} \times \sigma_C
$$

Where:
- $E(R_C)$ is the expected return of the complete portfolio.
- $r_F$ is the risk-free rate.
- $E(R_P) - r_F$ is the risk premium of the risky asset.
- $\sigma_C$ is the standard deviation (risk) of the complete portfolio.

## Opinion

Investors face the constant trade-off between security and higher returns, with the choice between risk-free and risky assets playing a pivotal role in this decision. The proportion of wealth allocated to risky assets (\( y_0 \)) significantly influences the overall return and volatility of the complete portfolio. As we’ve explored, personal risk tolerance and time horizons dictate whether investors lean towards conservative or aggressive strategies.

The concepts of **short selling** and **leveraging** introduce more complex ways to adjust risk and return. Investors who borrow to increase their exposure to risky assets can amplify returns, but at the cost of greater volatility. Similarly, those who engage in short selling seek to profit from declining asset prices but take on the risk of unlimited losses.

Ultimately, effective portfolio management hinges on understanding the **Capital Allocation Line (CAL)** and how to balance risk and reward while maintaining a constant **Sharpe ratio**. This approach helps investors align their strategies with their financial goals, optimizing the mix of risky and risk-free assets to achieve their desired outcomes.

## Summary

- Investors must choose between **risk-free assets** (e.g., Treasury bills) offering stable, low returns and **risky assets** (e.g., stocks, bonds) with potential for higher returns but more volatility.
- The allocation of wealth between risky and risk-free assets depends on an investor's **risk tolerance**:
  - **Older investors** typically prefer risk-free assets for stability.
  - **Younger investors** may lean toward risky assets for higher growth potential.
- The return of a complete portfolio (\(R_C\)) is calculated as a weighted average of the returns from both risky (\(R_P\)) and risk-free (\(r_F\)) assets, based on how much wealth is allocated to each.
- **Wealth allocation (\(y_0\))** affects the portfolio’s risk and return:
  - $y_0 = 0$: All wealth in risk-free assets.
  - $y_0 = 1$: All wealth in risky assets.
  - $y_0 > 1$: Leveraging—borrowing money to invest more in risky assets.
  - $y_0 < 0$: Short selling—betting against the risky asset.
- **Excess return** refers to the return above the risk-free rate, proportional to how much is invested in risky assets.
- Portfolio **volatility** increases as more is allocated to risky assets; risk-free assets do not contribute to volatility.
- The **Capital Allocation Line (CAL)** represents the risk-return trade-off, showing possible combinations of risky and risk-free assets.
- The **Sharpe ratio** of a complete portfolio remains constant, matching the Sharpe ratio of the risky asset, regardless of how wealth is allocated between risk-free and risky assets.
- Investors must balance risk and return, considering personal financial goals and risk tolerance to optimize their portfolio’s allocation.

