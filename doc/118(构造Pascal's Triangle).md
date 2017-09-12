### Pascal's Triangle

我的方案：
```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> result = new ArrayList<>();
        if(numRows == 0)
            return result;
        for(int i = 0; i < numRows; i++) {
            List<Integer> list = new ArrayList<>();
            for(int j = 0; j < i+1; j++) {
                if(j == 0 || j == i)
                    list.add(1);
                else {
                    list.add(result.get(i-1).get(j-1) + result.get(i-1).get(j));
                }
            }
            result.add(list);
        }
        return result;
    }
}
```
