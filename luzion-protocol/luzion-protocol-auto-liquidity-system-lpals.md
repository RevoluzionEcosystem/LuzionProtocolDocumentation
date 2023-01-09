# Luzion Protocol Auto Liquidity System (LPALS)

### <mark style="color:yellow;">**What Is Luzion Protocol Auto Liquidity System (LPALS)**</mark>

The Luzion Protocol Auto Liquidity System (LPALS) is a mechanism that allows users to buy and sell the LZN token on a decentralized exchange using a liquidity pool. The liquidity pool contains an equal balance of LZN and BNB tokens, which are used to facilitate trades on the exchange. When a user buys LZN, they add BNB to the pool and remove LZN, causing the value of the LZN to BNB ratio to increase. This increase in value allows LZN to be sold at a higher price.

To ensure that there is always sufficient liquidity in the pool to facilitate trades, the LPALS system is used to constantly add new LZN and BNB tokens to the pool. This allows users to buy and sell LZN at any time, as long as there is enough liquidity available. Overall, the LPALS system helps to ensure that the Luzion Protocol's decentralized exchange operates smoothly and efficiently, allowing users to trade LZN with confidence.

Please see the following code snippets for a more technical understanding of the implementation.

{% code overflow="wrap" lineNumbers="true" %}
```solidity
 // Liquidity related functions

    /**
     * @dev Get liquidity backing.
     */
    function getLiquidityBacking(uint256 accuracy) public view returns (uint256) {
        uint256 liquidityBalance = _gonBalances[pair].div(gonsPerFragment);
        return accuracy.mul(liquidityBalance.mul(2)).div(getCirculatingSupply());
    }

    /**
     * @dev Set the status for add liquidity automation.
     */
    function setAutoAddLiquidity(bool _flag) external authorized {
        if(_flag) {
            autoAddLiquidity = _flag;
            lastAddLiquidityTime = block.timestamp;
        } else {
            autoAddLiquidity = _flag;
        }
    }

    /**
     * @dev Set settings for target liquidity.
     */
    function setTargetLiquidity(uint256 _target, uint256 _denominator) external authorized {
        targetLiquidity = _target;
        targetLiquidityDenominator = _denominator;
    }
```
{% endcode %}

### <mark style="color:yellow;">How Does LPALS Works?</mark>

Here is a step-by-step guide to how the Luzion Protocol Auto Liquidity System (LPALS) works:

1. A user wants to buy or sell LZN on the decentralized exchange.
2. The user accesses the exchange and selects the LZN/BNB trading pair.
3. The exchange checks the balance of the liquidity pool, which contains an equal balance of LZN and BNB.
4. If there is sufficient liquidity in the pool to facilitate the trade, the exchange executes the trade by adding or removing the appropriate amount of LZN and BNB from the pool.
5. If the trade causes the LZN to BNB ratio to change, the value of LZN may also change as a result.
6. If the liquidity in the pool becomes low, the LPALS system kicks in to add more LZN and BNB to the pool, ensuring that there is always enough liquidity available for users to trade.

The Luzion Protocol Auto Liquidity System (LPALS) is a mechanism that helps to ensure the stability and sustainability of the Luzion Protocol's decentralized exchange. It does this by injecting new LZN and BNB into the liquidity pool on a regular basis, ensuring that there is always sufficient liquidity available for users to buy and sell the LZN token.

The LPALS system operates as follows: every 12 hours, a smart contract takes a 2% fee from all buy and sell transactions on the exchange, and stores the resulting LZN in the Auto Liquidity wallet (LZN Deployer wallet). When the 12-hour timer expires, the smart contract automatically exchanges half of the stored LZN for BNB and injects both the LZN and BNB into the liquidity pool's smart contract address. This process helps to maintain a constant supply of LZN and BNB in the liquidity pool, allowing users to trade without worrying about the pool running dry.

The injection of additional LZN and BNB into the liquidity pool also helps to maintain the price and chart for LZN, even in the face of large trades. This promotes the sustainability of the Luzion Protocol over the long term, as users can buy and sell LZN with confidence knowing that the liquidity pool will always have sufficient demand and supply.

Here's a quick video by whiteboard crypto on much easier understanding how liquidity pool works : [https://www.youtube.com/watch?v=dVJzcFDo498](https://www.youtube.com/watch?v=dVJzcFDo498)
