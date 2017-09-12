### Arithmetic Slices

说明：给一个整数数组，使数组的子序列为arithmetic，问
这样的子序列有多少个？

注：dp方法，当前的值通常依赖于当前的装态和历史的状态，
因此，如果能够记录历史的装态，极大降低算法的时间。即拿
空间换时间。。。

解法：

```java
class Solution {
    public int numberOfArithmeticSlices(int[] A) {
        if(A == null || A.length <= 2)
            return 0;
        int n = A.length;
        int[] result = new int[n];
        result[0] = 0;
        int same = 0;
        int distance = Integer.MAX_VALUE;
        for(int i = 1; i < n; i++) {
            if(A[i] - A[i - 1] == distance) {
                same++;
            }else {
                distance = A[i] - A[i - 1];
                same = 1;
            }
            if(same >= 2) {
                result[i] = result[i - 1] + same - 1;
            }else {
                result[i] = result[i -  1];
            }
        }
        return result[n - 1];

    }
}
```
