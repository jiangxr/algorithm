### Best Time to Buy and Sell Stock

说明：这道题的意思就是从数组中找两个数，是右边的数减去左边的数的差最大。

分析：其实就是每次遍历到一个节点时，都能够记录左边的最小值。差值和最大值比较。

```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null  || prices.length == 0)
            return 0;
        int max = 0;
        int minValue = prices[0];
        for(int i = 1; i < prices.length; i++) {
            if(prices[i] - minValue > max) {
                max = prices[i] - minValue;
            }
            if(prices[i] < minValue)
                minValue = prices[i];
        }
        return max;

    }
}
```
