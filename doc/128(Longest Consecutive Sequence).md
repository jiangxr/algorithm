### Longest Consecutive Subsequences

说明：给一个无序的数组，找到最长的连续子串
限制：O(n)的时间复杂度。

我的解法：
说明：超时了，主要是更新过程中需要花很多的时间。
```java
class Solution {
    public int longestConsecutive(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < nums.length; i++) {
            int value = 1;
            Integer pre = map.get(nums[i] - 1);
            if(pre != null) {
              value += pre;  
            }

            int tempKey = nums[i] + 1;
            int tempValue = value + 1;
            if(!map.containsKey(nums[i])) {
                map.put(nums[i], value);
            }
            while(map.containsKey(tempKey)) {
                map.put(tempKey, tempValue);
                tempKey++;
                tempValue++;
            }
        }
        int max = 0;
        for(Integer value : map.values()) {
            if(value > max)
                max = value;
        }
        return max;
    }
}
```

网上的解法：
方法一：
```java
class Solution {
    public int longestConsecutive(int[] nums) {
        int res = 0;
        Map<Integer, Integer> map = new HashMap<>();
        for(int key : nums) {
            if(!map.containsKey(key)) {
                int left = map.containsKey(key - 1)?map.get(key-1):0;
                int right = map.containsKey(key + 1)?map.get(key + 1):0;
                int total = left + right + 1;
                map.put(key, total);
                res = Math.max(res, total);
                map.put(key - left, total);
                map.put(key + right, total);

            }

    }
        return res;
}
}
```
