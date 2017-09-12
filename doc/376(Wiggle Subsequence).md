### Wiggle Subsequence

说明： 两数之差为正/负相邻出现，问最长的序列？

我的解决方案：

```java
class Solution {
    public int wiggleMaxLength(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        int n = nums.length;
        int[] result = new int[n + 1];
        int total = 0;
        int pre = 0;
        boolean isAscend =  false;
        for(int i = 0; i < n; i++ ) {
            if(total == 0) {
                result[i + 1] = 1;
                pre = nums[i];
                total = 1;
            }else {
                if(total == 1) {
                    if(nums[i] == pre) {
                        result[i + 1] = result[i];
                    }else if(nums[i] > pre) {
                        result[i + 1] = 2;
                        isAscend = false;
                        pre = nums[i];
                        total++;
                        }else {
                        result[i + 1] = 2;
                        isAscend = true;  
                        pre = nums[i];
                        total++;
                    }
                }else {
                    if(nums[i] == pre) {
                        result[i + 1] = result[i];
                    }else {
                        if(isAscend) {
                            if(nums[i] > pre) {
                                result[i + 1] =  result[i] + 1;
                                total++;
                                isAscend = false;
                                pre = nums[i];
                            }else {
                                result[i + 1] = result[i];
                                pre = nums[i];
                            }
                        }else {
                            if(nums[i] < pre) {
                                result[i + 1] = result[i] + 1;
                                total++;
                                isAscend = true;
                                pre = nums[i];
                            }else {
                                result[i + 1] = result[i];
                                pre = nums[i];
                            }
                        }
                    }

                }
            }
        }
        return result[n];

    }
}
```
