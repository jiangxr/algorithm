### Best Time to Buy and Sell Stock II

说明：允许多次买和卖，但是在买物品之前，必须将手头的东西卖掉。问能赚取的最大金额。

分析：经过分析，只需要找到连续的递增序列即可。

```java
class Solution {
    public int maxProfit(int[] prices) {
        int max = 0;
        int i = 0;
        while(i < prices.length) {
            int value = prices[i];
            int temp = value;
            while(i < prices.length && prices[i] >= temp) {
                temp = prices[i];
                i++;
            }
            max += prices[i-1] - value;
        }
        return max;
    }
}
```
