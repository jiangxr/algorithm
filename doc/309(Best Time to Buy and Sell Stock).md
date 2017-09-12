### Best Time to Buy and Sell Stock with Cooldown

说明：买卖袜子，卖了袜子的下一天不能买袜子，最大的获益

不能理解。。

网上的解法：

方法一：
```java
class Solution {
    public int maxProfit(int[] prices) {
        int sell = 0;
        int pre_sell = 0;
        int buy = Integer.MIN_VALUE;
        int pre_buy;
        for(int price : prices) {
            pre_buy = buy;
            buy = Math.max(pre_sell - price, pre_buy);
            pre_sell = sell;
            sell = Math.max(pre_buy + price, pre_sell);
        }
        return sell;

    }
}
```

解法二：
网上的答案太厉害，居然把状态转移图都画出来了。
```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length == 0)
            return 0;
        int n = prices.length;
        int buy = -prices[0];
        int sell = Integer.MIN_VALUE;
        int rest = 0;
        int pre_buy;
        int pre_sell;
        for(int i = 1; i < n; i++) {
            pre_buy = buy;
            pre_sell = sell;
            buy = Math.max(pre_buy, rest - prices[i]);
            sell = pre_buy + prices[i];
            rest = Math.max(rest, pre_sell);
        }
        return Math.max(rest, sell);
    }
}
```
