### Coin Change

说明： 有不同金额的硬币，给一个amount，需要由这些硬币构成，相同硬币的个数不受
限制。问最少硬币的构成？

解法：
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        if(coins == null || coins.length == 0)
            return -1;
        int[] result = new int[amount + 1];
        Arrays.fill(result, -1);
        result[0] = 0;
        int n = coins.length;
        for(int i = 1; i <= amount; i++) {
            int min = Integer.MAX_VALUE;
            for(int j = 0; j < n; j++) {
               if(i - coins[j] >= 0 && result[i - coins[j]] != -1) {
                   min = Math.min(min, 1 + result[i - coins[j]]);
               }
            }
            result[i] = (min == Integer.MAX_VALUE?-1:min);
        }
        return result[amount];
    }
}
```
