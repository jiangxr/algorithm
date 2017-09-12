### Pascal's Triangle II

说明： 输出帕斯卡三角形的第i行的列表值

```java
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> result = new ArrayList<>();
        if(rowIndex < 0)
            return result;
        result.add(1);
        for(int i = 1; i <= rowIndex; i++) {
            int pre = 1;
            for(int j = 0; j <= i; j++) {
                if(j == 0)
                    continue;
                if(j == i)
                    result.add(1);
                else {
                    int temp = result.get(j);
                    result.set(j, pre + result.get(j));
                    pre = temp;

                }
            }
        }
        return result;
    }
}
```
