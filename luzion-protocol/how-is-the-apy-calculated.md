---
description: APY calculation.
---

# 💸 How is the APY calculated?

## Continuous Compounding Formula

Before understanding what rebase or continuous compounding formula, let us recall few things about the well know compound interest like staking APR. Compound interest is called APR or annual percentage rate, it could be calculated daily or weekly, but the interest is calculated based on initial investment only.\
\
Luzion Protocol Rebase uses an Continuous Compounding Interest formula in rebasing the supply constantly every EPOCH (15 minutes) to all BSC wallet that are holding LZN. Basically, if someone had invest 100 BUSD and received 100 LZN, the first EPOCH will calculate based on the 100 LZN as initial. However, the second EPOCH will now calculate the initial 100 LZN plus the previous epoch LZN interest he received together, therefore, receiving more LZN from the previous EPOCH.

Below is the Calculation of APY :

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Here is the formula for you to utilize in browser itself, just paste the formula in the browser and you will able to review the correct APY based on the Rebase Rate percentage.

$$
(1 + (insert rebaserate/100))^35040*100
$$

### Variable Rebase Rate vs. Fixed Rebase Rate

Many Rebase Tokens out there runs on flexible APY rate or adjusted as they wish. Some runs on a fixed APY rate perpetually and some runs on a fixed rate according to timeline like how LZN Token Smart Contract does. Luzion Protocol was the first, to run an actual correct rebase rate logic in the smart contract.&#x20;

Revoluzion developers realize the mistake that many rebase tokens such as Safuu did was not developing the proper logic for their smart contract, which prevented the rebase rate to adjust accordingly to the set timeline, this causes the rebase rate to never be adjusted and proceeds to increase the tokens continuously till max supply.

Therefore, we develop the proper logic and test run the smart contract on the TestNet to ensure the logic is working according to the timeline set. Revoluzion team was able to manage testing in a much shorter time frame by adjusting the rebase to 1.5 secs per rebase.

### Continuous Compounding Formula Derivation

We will derive the continuous compounding formula below.&#x20;

The compound interest formula is,

A = P (1 + r/n)nt

Here, n = the number of terms the initial amount (P) is compounding in the time t and A is the final amount (or) future value. For the continuous compound interest, n → ∞. So we will take the limit of the above formula as n → ∞.

A = limn→∞n→∞ P (1 + r/n)nt = Pert&#x20;

The final step is by using one of the limit formulas which says, limn→∞n→∞ (1 + r/n)n = er.

Thus, the continuous compound interest formula is,

A = Pert&#x20;

### <mark style="color:green;">Example:</mark>

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
P = (Principle + Interest) = <mark style="color:green;">$1,000</mark>\ <mark style="color:green;"></mark>\ <mark style="color:green;"></mark>Total accumulated end of 1 year rebase :

A = (Total Accrued Amount) = <mark style="color:green;">$3,831,258.01</mark>
