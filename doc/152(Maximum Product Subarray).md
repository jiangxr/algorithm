### Maximum Product Subarray

说明：给一个整数数组，求连续数组乘积的最大值。

使用方法： DP

我的解决方法：

```java
class Solution {
    public int maxProduct(int[] nums) {
        int max = nums[0];
        int preMin = nums[0];
        int preMax = nums[0];
        for(int i = 1; i < nums.length; i++) {
            int s1 = preMin * nums[i];
            int s2 = preMax * nums[i];
            int s3 = nums[i];
            if(s1 > s2) {
                int tmp = s2;
                s2 = s1;
                s1 = tmp;
            }

            if(s1 > s3) {
                int tmp = s3;
                s3 = s1;
                s1 = tmp;
            }

            if(s2 > s3) {
                int tmp = s3;
                s3 = s2;
                s2 = tmp;
            }
            preMin = s1;
            preMax = s3;
            if(max < preMax)
                max = preMax;
        }
        return max;
    }
}
```
