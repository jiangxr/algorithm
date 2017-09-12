### Perfect Squares

说明：一个数分解为只由1，4，9这样整数平方组成的数，问：给
出n，最短的组合是多少？

我的解决方法：

result如果使用static关键字修饰会报错，不知道为什么。。

```java
class Solution {
    //这里加入static关键字结果不会，为什么啊？
    private List<Integer> result = new ArrayList<>();
    public int numSquares(int n) {
        if(n == 0)
            return 0;
        int square = 1;
        int size = result.size();
        for(int i = size; i < n; i++) {
           if(Math.pow((int)Math.sqrt(i + 1), 2) == i + 1) {
                square = i + 1;
                result.add(1);
            }else {
               int min = i + 1;
               int j = (int)Math.sqrt(square);
               while(j >= 1) {
                   min = Math.min(min, result.get(i - j * j) + 1);
                   j--;
               }
                result.add(min);
           }
        }
        return result.get(n-1);
    }
}
```
