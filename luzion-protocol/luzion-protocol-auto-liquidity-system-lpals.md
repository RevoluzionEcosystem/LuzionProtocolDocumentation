# Luzion Protocol Auto Liquidity System (LPALS)

### **What Is Luzion Protocol Auto Liquidity System (LPALS)**

Luzion Protocol Auto Liquidity System (LPALS) is a feature that maintains liquidity in the LZN/BNB liquidity pool on the DeFi platform. The pool is comprised of a 50/50 split between LZN and BNB to balance the ratio. The starting price of LZN is determined by the conversion ratio between BNB and LZN.

When a user buys LZN, they add more BNB to the pool and remove LZN, which increases the balance of BNB and the value of the LZN/BNB ratio. This is what drives the price of LZN higher. The liquidity pool allows users to buy and sell LZN at any time as long as there is enough liquidity in the pool. To ensure that the pool does not run out of liquidity, the LPALS system is used to constantly add liquidity to the pool.

### How Does LPALS Works?

To ensure the liquidity pool have sufficient LZN and BNB constantly, LPALS system will automatically inject BNB and LZN into the liquidity pool every <mark style="color:green;">**12 hours constantly**</mark>. The smart contract will take **2%** of all buy and sell txn and store the LZN into the Auto Liquidity wallet (LZN Deployer wallet) for the next **12 hours**.

Once the **12 hours** timer hits, the smart contract will automatically swap half of the LZN to BNB and inject both half LZN and half BNB into the liquidity pool pair smart contract address. By doing so, this ensures the liquidity pool will constantly have enough demand and supply to users always.

By having much more liquidity added to the pool, this helps the price and chart to maintain constantly even tho there's a huge sale. This helps keep a healthy looking chart while eventually having users to buy and sell without worrying the liquidity pool to run dry while **maintaining the sustainability of Luzion Protocol** for years to come.

Here's a quick video by whiteboard crypto on much easier understanding how liquidity pool works : [https://www.youtube.com/watch?v=dVJzcFDo498](https://www.youtube.com/watch?v=dVJzcFDo498)
