### Guess Number Higher or Lower II

说明：猜硬币游戏，猜错了，惩罚猜的数字的钱数，问：至少
需要多少钱，能够保证肯定能赢得比赛？

解法：网上采用递归，但是呢，如果直接采用递归肯定时间复杂度
比较高，因此，在猜的过程中使用一个数组保存中间的结果。。
```java
class Solution {
    public int getMoneyAmount(int n) {
        int[][] table = new int[n + 1][n + 1];
        return dp(table, 1, n);
    }

    private int dp(int[][] t, int s, int e) {
        if(s >= e) return 0;
        if(t[s][e] != 0) return t[s][e];
        int res = Integer.MAX_VALUE;
        for(int i = s; i <= e; i++) {
            int tmp = i + Math.max(dp(t, s, i - 1), dp(t, i + 1, e));
            res = Math.min(res, tmp);
        }
        t[s][e] = res;
        return res;
    }
}
```

方法二：
```java
class Solution {
    public int getMoneyAmount(int n) {
        int[][] dp = new int[n + 2][n + 2];
        for(int len = 1; len < n; len++) {
            for(int from = 1, to = from + len; to <= n; from++, to++) {
                dp[from][to] = Integer.MAX_VALUE;
                for(int k = from; k <= to; k++)
                    dp[from][to] = Math.min(dp[from][to], k + Math.max(dp[from][k -1], dp[k + 1][to]) );
            }
        }
        return dp[1][n];
    }

}
```
