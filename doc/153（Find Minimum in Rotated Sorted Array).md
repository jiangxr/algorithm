### Find Minimum in Rotated Sorted ArrayList

说明：在一个循环中数组是有序的，找出最小的值。

```java
class Solution {
    public int findMin(int[] nums) {
        if(nums == null || nums.length == 0)
            return -1;
        if(nums.length == 1)
            return nums[0];
        int lo = 0;
        int hi = nums.length - 1;
        while(lo < hi) {
            int mid = (lo + hi) >> 1;
            if(nums[mid] > nums[hi])
                lo = mid + 1;
            else
                hi = mid;
        }
        return nums[lo];
    }
}
```
