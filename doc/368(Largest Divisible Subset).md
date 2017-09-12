### Largest Divisible Subset

说明：审题不清，真是无语了。。

答案：
```java
class Solution {
    public List<Integer> largestDivisibleSubset(int[] nums) {
        if(nums == null || nums.length <= 0)
            return new ArrayList<Integer>();
        int n = nums.length;
        Arrays.sort(nums);
        List<Integer>[] result = new ArrayList[n + 1];
        result[0] = new ArrayList<Integer>();
        ArrayList<Integer> list1 = new ArrayList<>();
        list1.add(nums[0]);
        result[1] = list1;
        int maxIndex = 1;
        int maxIndex1 =1;
        for(int i = 1; i < n; i++) {
            ArrayList<Integer> list = null;
            int index = -1;
            int le = -1;
            for(int j = 0; j < i; j++) {
                if(nums[i] % nums[j] == 0 && result[j + 1].size() > le) {
                    index = j + 1;
                    le = result[j + 1].size();
                }
            }
            if(index != -1) {
                list = new ArrayList<>(result[index]);
            }else {
                list = new ArrayList<>();
            }
            list.add(nums[i]);
            result[i + 1] = list;
            if(result[i + 1].size() > result[maxIndex].size())
                maxIndex = i + 1;
        }
       return result[maxIndex];

    }
}
```
