### Integer Break

说明：将一个整数拆成几个数相加，并使这几个数之积最大。

解法：

```java
class Solution {
    public int integerBreak(int n) {
        int[] result = new int[n + 1];
        result[1] = 1;
        result[2] = 1;
        for(int i = 3; i <= n; i++) {
            int max = 1;
            for(int j = 1; j <= i / 2; j++) {
                max = Math.max(max, Math.max(result[j], j) * Math.max(result[i - j], i - j));
            }
            result[i] = max;
        }
        return result[n];
    }
}
```
