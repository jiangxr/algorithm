### House Robbe II

说明：跟上题不同的是，所有的马围成一个环，问最大的金额？

我的解法：
```java
class Solution {
    public int rob(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        if(nums.length == 1)
            return nums[0];
        if(nums.length == 2)
            return Math.max(nums[0], nums[1]);
        int n = nums.length;
        int[] a = new int[n  - 1];
        a[0] = 0;
        a[1] = nums[1];
        for(int i = 2; i < n - 1; i++) {
            a[i] = Math.max(a[i - 1], a[i - 2] + nums[i]);
        }

        int[] b = new int[n - 1];
        b[0] = 0;
        b[1] = nums[n - 2];
        for(int i = n - 3; i >= 1; i--) {
            b[n- i -1] = Math.max(b[n - i - 2], b[n - i - 3] + nums[i]);
        }

        return Math.max(a[n - 2], Math.max(nums[0] + b[n - 3], a[n - 3] + nums[n - 1]));

    }
}
```

```java
class Solution {
    public int rob(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        if(nums.length == 1)
            return nums[0];
        if(nums.length == 2)
            return Math.max(nums[0], nums[1]);
        int n = nums.length;
        int include = 0;
        int exclude = 0;
        int i,e;
        for(int k = 0; k < n - 1; k++) {
            i = include;
            e = exclude;
            include = e + nums[k];
            exclude = Math.max(i, e);
        }
        int max1 = Math.max(include, exclude);

        include = 0;
        exclude = 0;
        for(int k = 1; k < n; k++) {
            i = include;
            e = exclude;
            include = nums[k] + e;
            exclude = Math.max(i, e);
        }
        int max2 = Math.max(include, exclude);
        return Math.max(max1, max2);
    }
}
```

网上的解法：
思路：思路差不多，但是写法比我的简单
```java
private int rob(int[] num, int lo, int hi) {
    int include = 0, exclude = 0;
    for (int j = lo; j <= hi; j++) {
        int i = include, e = exclude;
        include = e + num[j];
        exclude = Math.max(e, i);
    }
    return Math.max(include, exclude);
}

public int rob(int[] nums) {
    if (nums.length == 1) return nums[0];
    return Math.max(rob(nums, 0, nums.length - 2), rob(nums, 1, nums.length - 1));
}
```
