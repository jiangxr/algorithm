### Single Number II

不会。。
注：这种题主要用到 desigin a counter that record state.
细粒度到bit，这种解法真的好厉害。。
网上的解法：

方法一：
```java
class Solution {
    public int singleNumber(int[] nums) {
        int ones = 0, twos = 0;
    for(int i = 0; i < nums.length; i++){
        ones = (ones ^ nums[i]) & ~twos;
        twos = (twos ^ nums[i]) & ~ones;
    }
    return ones;
    }
}
```

方法二：
```java
public class Solution {

    public int singleNumber(int[] nums) {
        //we need to implement a tree-time counter(base 3) that if a bit appears three time ,it will be zero.
        //#curent  income  ouput
        //# ab      c/c       ab/ab
        //# 00      1/0       01/00
        //# 01      1/0       10/01
        //# 10      1/0       00/10
        // a=~abc+a~b~c;
        // b=~a~bc+~ab~c;
        int a=0;
        int b=0;
        for(int c:nums){
            int ta=(~a&b&c)|(a&~b&~c);
            b=(~a&~b&c)|(~a&b&~c);
            a=ta;
        }
        //we need find the number that is 01,10 => 1, 00 => 0.
        return a|b;

    }
}
```
