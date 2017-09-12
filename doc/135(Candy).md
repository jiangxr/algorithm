### Candy

说明：有n个小孩站成一排，给小孩分配糖果，每个小孩都有一个等级。
约束条件：
每个小孩至少一个糖果；
高等级的小孩比相邻的小孩的糖果多。问所需要的最少的糖果

我的解决方案：
又超时了。
```java
class Solution {
    public int candy(int[] ratings) {
       if(ratings == null || ratings.length == 0)
           return 0;
        int n = ratings.length;
        int[] count = new int[n];
        for(int i = 0; i < n; i++)
            count[i] = 1;
        for(int i = 1; i < n; i++) {
            if(ratings[i] > ratings[i - 1])
                count[i] = count[i - 1] + 1;
            else if(ratings[i] < ratings[i - 1]) {
                if(count[i - 1] > 1)
                    count[i] = 1;
                else {
                int index = i;
                while(index > 0 && ratings[index] < ratings[index - 1] && count[index - 1] <= count[index]) {
                    count[index - 1] = count[index] + 1;
                    index--;
                }
            }
            }
        }
        int sum = 0;
        for(int i = 0; i < n; i++)
            sum += count[i];
        return sum;
    }
}
```

网上的方法：
注：通过两次循环即可搞定，首先从左往右升序，然后从右往左升序
```java
class Solution {
    public int candy(int[] ratings) {
       if(ratings == null || ratings.length == 0)
           return 0;
        int n = ratings.length;
        int[] count = new int[n];
        count[0] = 1;
        for(int i = 1; i < n; i++) {
            if(ratings[i] > ratings[i - 1])
                count[i] = count[i - 1] + 1;
            else
                count[i] = 1;
        }

        int total = count[n - 1];
        for(int i = n - 2; i >= 0; i--) {
            if(ratings[i] > ratings[i + 1] && count[i] <= count[i + 1])
                count[i] = count[i + 1] + 1;
            total += count[i];
        }
        return total;
    }
}
```
