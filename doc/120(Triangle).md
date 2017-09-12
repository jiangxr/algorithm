### 找三角形路径的最小值

说明：采用DP比较好解决。
```
使用d[i][j]表示第行的第i个元素到底部的最小值。
则d[i+1][j+1] = arr[i+1][j+1] + Math.min(d[i][j+1], d[i][j+2]);
```
```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        if(triangle == null)
            return 0;
        int[] num = new int[triangle.size()];
        for(int i = triangle.size() - 1; i >= 0; i--) {
            for(int j = 0; j < i+1; j++ ) {
                if(i == triangle.size()-1)
                    num[j] = triangle.get(i).get(j);
                else {
                    num[j] = triangle.get(i).get(j) + Math.min(num[j], num[j+1]);
                }
            }
        }
        return num[0];
    }
}
```
