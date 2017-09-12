### Longest Increasing Subsequence

说明： 在一个数组中，寻找最长的递增子序列

分析：正常的解法需要的时间复杂度为O(N^2)，但是题目要求
O(NlogN)的时间复杂度，稍微难办。。。


解法：
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        int n = nums.length;
        int[] result = new int[n];
        int len = 0;
        for(int i = 0; i < n; i++) {
            int j = Arrays.binarySearch(result, 0, len, nums[i]);
            if(j < 0) {
                j = - (j + 1);
            }

            result[j] = nums[i];
            if(j == len)
                len++;
        }
        return len;
    }
}
```

这种方法真的很难想到
