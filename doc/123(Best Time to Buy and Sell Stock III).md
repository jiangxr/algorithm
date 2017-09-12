### Best Time to Buy and Sell Stock III

说明：最多有两次记录，一次记录包括购买和出售

我的方法：
通过循环，找到两次购买记录的分隔点。找到最大的。
```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length <= 1)
            return 0;
        int n = prices.length;
        int[] a = new int[n];
        int[] b = new int[n];
        a[0] = 0;
        b[0] = 0;
        int min = prices[0];
        for(int i = 1; i < n; i++ ) {
            if(prices[i] - min > a[i-1]) {
                a[i] = prices[i] - min;
            }else {
                a[i] = a[i-1];
            }
            if(min > prices[i])
                min = prices[i];
        }
        int tempMax = prices[n-1];
        for(int j = n - 2; j >= 0; j--) {
            if(tempMax - prices[j] > b[j+1])
                b[j] = tempMax - prices[j];
            else
                b[j] = b[j+1];
            if(prices[j] > tempMax)
                tempMax = prices[j];
        }

        int result = 0;
        for(int i = 0; i<n;i++) {
            if(result < b[i] + a[i])
                result = b[i] + a[i];
        }
        return result;
    }
}
```

网上的解法：

方法一：（太难理解）
```java
public class Solution {
    public int maxProfit(int[] prices) {
        int hold1 = Integer.MIN_VALUE, hold2 = Integer.MIN_VALUE;
        int release1 = 0, release2 = 0;
        for(int i:prices){                              // Assume we only have 0 money at first
            release2 = Math.max(release2, hold2+i);     // The maximum if we've just sold 2nd stock so far.
            hold2    = Math.max(hold2,    release1-i);  // The maximum if we've just buy  2nd stock so far.
            release1 = Math.max(release1, hold1+i);     // The maximum if we've just sold 1nd stock so far.
            hold1    = Math.max(hold1,    -i);          // The maximum if we've just buy  1st stock so far.
        }
        return release2; ///Since release1 is initiated as 0, so release2 will always higher than release1.
    }
}
```

方法二：使用DP（好难理解）
总结：tmpMax用来记录当计算f[i][j]时，左边的最大值。。
所以每次找到f[i][j]时，都需要重新更新tmpMax.
```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length <= 1)
            return 0;
        int times = 2;
        int maxProf = 0;
        int n = prices.length;
        int[][] f = new int[times+1][n];
        for(int i = 1; i <= times; i++) {
            int tmpMax = f[i - 1][0] - prices[0];
            for(int j = 1; j < n; j++) {
                f[i][j] = Math.max(f[i][j-1], prices[j] + tmpMax);
                //tmpMax的更新好难理解
                //f[i-1][j] - prices[j]是如果最大值是以prices[j]为结尾时来
                //寻找最大值。
                tmpMax = Math.max(tmpMax, f[i - 1][j] - prices[j]);
                maxProf = Math.max(f[i][j], maxProf);
            }
        }
        return maxProf;
    }
}
```
