### Ugly Number II

说明： 一个数的素因子只能由2，3，5组成。1作为第一个丑数，问第n个丑数是多少？

我的解决方法：DP

```java
class Solution {
    public int nthUglyNumber(int n) {
        if(n == 1)
            return 1;
        int[] arr = new int[n];
        arr[0] = 1;
        int[] index = new int[]{0, 0, 0};
        for(int i = 1; i < n; i++) {
            int min = Math.min(arr[index[0]] * 2, Math.min(arr[index[1]] * 3, arr[index[2]] * 5));
            arr[i] = min;
            if(min == arr[index[0]] * 2)
                index[0] += 1;
            if(min == arr[index[1]] * 3)
                index[1] += 1;
            if(min == arr[index[2]] * 5)
                index[2] += 1;
        }
        return arr[n - 1];
    }
}
```
