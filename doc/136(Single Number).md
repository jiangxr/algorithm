### Single Number

说明：给定一个数组，只有一个数出现一次，其他的所有数都是出现了两次， 找
到这个出现一次的那个数。

我的解决方法：
使用异或
```java
class Solution {
    public int singleNumber(int[] nums) {
        if(nums == null || nums.length == 0)
            return -1;
        if(nums.length == 1)
            return nums[0];

        int result = nums[0];
        int n = nums.length;
        for(int i = 1; i < n; i++) {
            result ^= nums[i];
        }
        return result;

    }
}
```
