### House Robber


说明：有n匹马排成一行，抢劫犯来抢劫马，不能抢劫相邻的马，每匹马有一个价钱。问怎样抢劫马
能使金额最大？

我的解法：
```java
class Solution {
    public int rob(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        if(nums.length == 1)
            return nums[0];
        int n = nums.length;
        int[] arr = new int[n + 1];
        arr[0] = 0;
        arr[1] = nums[0];
        for(int i = 1; i < n; i++) {
            arr[i + 1] = Math.max(arr[i], arr[i -1] + nums[i]);
        }
        return arr[n];
    }
}
```
