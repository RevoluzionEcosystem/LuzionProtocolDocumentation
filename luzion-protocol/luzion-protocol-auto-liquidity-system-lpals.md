# Luzion Protocol Auto Liquidity System (LPALS)

### **What Is Luzion Protocol Auto Liquidity System (LPALS)**

Liquidity pools are one of the foundational technologies behind the current DeFi ecosystem. In itself, the idea is profoundly simple. A liquidity pool is basically funds thrown together in a big digital pile. But what can you do with this pile in a permissionless environment, where anyone can add liquidity to it? Let’s explore how DeFi has iterated on the idea of liquidity pools.

Basically, the liquidity pool will contain a split of <mark style="color:green;">**50/50 between LZN and BNB in the pool**</mark> to balance out the ratio. The price of start would depend on the start of the conversion ratio between BNB to LZN.\
\
For example, when someone buys, they put in more BNB into the pool while removing LZN from the pool, creating a higher balance of BNB instead of LZN in the pool which in turn increases the value of LZN to BNB ratio. This what makes the price of LZN to increase higher in return.\
\
By having a liquidity pool, users are free to buy and sell LZN at any given time as long there is enough liquidity inside the pool (BNB/LZN). To ensure the liquidity does not goes empty, this is where the LPALS system is utilize by Luzion Protocol by constantly adding liquidity.

### How Does LPALS Works?

To ensure the liquidity pool have sufficient LZN and BNB constantly, LPALS system will automatically inject BNB and LZN into the liquidity pool every <mark style="color:green;">**12 hours constantly**</mark>. The smart contract will take **2%** of all buy and sell txn and store the LZN into the Auto Liquidity wallet (LZN Deployer wallet) for the next **12 hours**.

Once the **12 hours** timer hits, the smart contract will automatically swap half of the LZN to BNB and inject both half LZN and half BNB into the liquidity pool pair smart contract address. By doing so, this ensures the liquidity pool will constantly have enough demand and supply to users always.

By having much more liquidity added to the pool, this helps the price and chart to maintain constantly even tho there's a huge sale. This helps keep a healthy looking chart while eventually having users to buy and sell without worrying the liquidity pool to run dry while **maintaining the sustainability of Luzion Protocol** for years to come.

Here's a quick video by whiteboard crypto on much easier understanding how liquidity pool works : [https://www.youtube.com/watch?v=dVJzcFDo498](https://www.youtube.com/watch?v=dVJzcFDo498)
