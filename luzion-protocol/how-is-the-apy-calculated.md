---
description: APY calculation.
---

# How is the APY calculated?

## <mark style="color:yellow;">Continuous Compounding Formula</mark>

Before delving into the concept of rebase and the continuous compounding formula, it is important to review the basics of compound interest, also known as the annual percentage rate (APR). Compound interest is calculated based on the initial principal balance and is compounded at a specified frequency, such as daily or weekly.

The compound interest formula is used to calculate the total interest earned on an investment over a certain period of time. It takes into account the effect of interest being added to the principal balance, which can lead to exponential growth.

In the example given, the daily compound interest rate is 2.28635% and the initial balance is 100 LZN tokens. Using the compound interest formula, we can calculate the final balance after one year as follows:

Final Balance = Principal \* (1 + Rate/n)^(n\*t)

Where:

* Principal is the initial balance of 100 LZN tokens
* Rate is the daily compound interest rate of 2.28635%
* n is the number of times the interest is compounded per year (in this case, daily)
* t is the number of years the interest is compounded (in this case, 1 year)

Plugging these values into the formula, we get:

Final Balance = 100 \* (1 + 0.0228635/365)^(365\*1)

This simplifies to:

Final Balance = 100 \* (1.0228635)^365

Which gives us a final balance of approximately 383,125.800 LZN tokens.

This demonstrates the potential for significant growth through compound interest, as the balance grows exponentially over time rather than linearly. It is important to consider the effect of compounding when evaluating the potential return on an investment, as it can greatly impact the final balance.

The Luzion Protocol utilizes a continuous compounding interest formula in its rebase process, which occurs every EPOCH (15 minutes) for all BSC wallets holding LZN. In this system, the initial investment of, for example, 100 BUSD and receipt of 100 LZN serves as the principal balance. During each subsequent EPOCH, the interest earned on this initial balance is added to the principal, resulting in an updated balance that is used to calculate the next period's interest.

This process effectively compounds the interest earned on the principal balance, leading to exponential growth over time. For instance, in the second EPOCH, the initial balance of 100 LZN is compounded with the interest earned in the previous period, resulting in the receipt of additional LZN. As the rebase process continues, the compounded interest on the growing principal balance results in an increasing return on the initial investment.

Below is the Calculation of APY :

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Here is the formula for you to utilize in browser itself, just paste the formula in the browser and you will able to review the correct APY based on the Rebase Rate percentage.

$$
(1 + (insert rebaserate/100))^35040*100
$$

### <mark style="color:yellow;">Variable Rebase Rate vs. Fixed Rebase Rate</mark>

There are a variety of approaches to setting the annual percentage yield (APY) rate for rebase tokens. Some systems utilize a flexible APY that can be adjusted at the discretion of the issuer, while others utilize a fixed APY that remains constant over time. The Luzion Protocol represents a unique approach in that it utilizes a fixed APY rate that is implemented according to a predetermined timeline.

It is worth noting that some rebase tokens, such as Safuu, have encountered issues due to the lack of proper logic in their smart contracts. Specifically, these smart contracts have been unable to properly adjust the rebase rate according to the set timeline, leading to continuous token issuance until the maximum supply is reached.

The Revoluzion team recognized the importance of developing the proper logic for the Luzion Protocol's smart contract to ensure that the rebase rate adjusts according to the timeline as intended. In order to efficiently test this logic, the team implemented a rebase rate of 1.5 seconds per rebase on the TestNet. This enabled the team to thoroughly test the smart contract's functionality in a shorter timeframe. Overall, the development of a robust and well-designed smart contract is crucial for the proper functioning of a rebase token system.

### <mark style="color:yellow;">Continuous Compounding Formula Derivation</mark>

We will derive the continuous compounding formula below.&#x20;

The compound interest formula is,

A = P (1 + r/n)nt

Here, n = the number of terms the initial amount (P) is compounding in the time t and A is the final amount (or) future value. For the continuous compound interest, n → ∞. So we will take the limit of the above formula as n → ∞.

A = limn→∞n→∞ P (1 + r/n)nt = Pert&#x20;

The final step is by using one of the limit formulas which says, limn→∞n→∞ (1 + r/n)n = er.

Thus, the continuous compound interest formula is,

A = Pert&#x20;

### <mark style="color:yellow;">Examples</mark>

Lets say, Zack, invested into LZN and received 1000 LZN tokens, now just for example, the price sustains at 1 BUSD constantly.\
\
And just for example, the rebase rate is at 0.04722 for 1 year timeline. Now since we know the rate from the smart contract codes, to determine the total of tokens Zack can accumulate at the end of the year timeline will be :

$$
(1 + (0.04722/100))^35040*100
$$

Rebase rate : 0.04722

1 Year Epoch : 35040

Total tokens accumulated will be : 1,527,889,076.52 Tokens.

To understand a better perspective on LZN rate :

Total invested at LZN start of rebase :\
\
P = (Principle + Interest) = <mark style="color:yellow;">**$1,000**</mark>\ <mark style="color:green;"></mark>\ <mark style="color:green;"></mark>Total accumulated end of 1 year rebase :

A = (Total Accrued Amount) = <mark style="color:yellow;">**$3,831,258.01**</mark>
