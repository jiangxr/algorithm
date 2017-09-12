### Rangle Sum Query - Immutable

说明：求任意两个索引之间元素之和

解法：
```java
class NumArray {
    private int[] num;
    public NumArray(int[] nums) {
        if(nums == null || nums.length == 0)
            return;
        this.num = nums;
        for(int i = 1; i < nums.length; i++) {
           num[i] = num[i-1] + num[i];
        }
    }

    public int sumRange(int i, int j) {
        if(num == null)
            return 0;
        if(i < 0 || j >= num.length)
            return 0;
        if(i == 0)
            return num[j];
        return num[j] - num[i - 1];
    }
}
```
