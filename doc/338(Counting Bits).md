### Counting Bits

说明：给一个整数，求其二进制中1出现的次数

分析：实在想不到，头脑反应不过来，虽然知道使用DP，但是无法写出状态转移方程。

解决方法：
```java
class Solution {
    public int[] countBits(int num) {
        int[] result = new int[num + 1];
        for(int i = 1; i <= num; i++) {
           result[i] = result[i >> 1] + (i & 1);
        }
        return result;
    }
}
```
