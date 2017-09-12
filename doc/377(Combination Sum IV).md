### Combination Sum IV

说明：给一个由正整数元素组成的数组和一个正整数
target，问有多少种可能使数组中的几个元素之和等于
target。

我的解决方案：

```java
class Solution {
    public int combinationSum4(int[] nums, int target) {
        if(nums == null || nums.length == 0)
            return 0;
        int[] result = new int[target + 1];
        result[0] = 1;
        int n = nums.length;
        for(int i = 1; i <= target; i++) {
            int total = 0;
            for(int j = 0; j < n; j++) {
                if(i >= nums[j])
                    total += result[i - nums[j]];
            }
            result[i] = total;
        }
        return result[target];
    }
}
```
