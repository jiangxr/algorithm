### Count Numbers with Unique  Digits

说明：0至n之前的数字，使其中间的数字没有重复，问这样的数有多少？

```java
class Solution {
    public int countNumbersWithUniqueDigits(int n) {
        if(n == 0)
            return 1;
        int[] result = new int[n + 1];
        result[1] = 10;
        for(int i = 2; i <= n; i++) {
            result[i] = result[i - 1] + 9 * getComCount(9, i - 1);
        }
        return result[n];

    }

    private int getComCount(int n, int m) {
        int hh = 1;
        for(int i = n; i > n - m; i--) {
            hh *= i;
        }
        return hh;
    }
}
```
