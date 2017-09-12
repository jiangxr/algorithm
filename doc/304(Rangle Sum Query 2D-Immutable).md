### Rangle Sum Query 2D - Immutable

说明：给一个矩阵，给出左上顶点和右下顶点，求这个矩阵元素之和。


解法：
```java
class NumMatrix {
    int[][] res;
    public NumMatrix(int[][] matrix) {
        if(matrix == null || matrix.length == 0)
            return;
       res = matrix;
        int row = matrix.length;
        int col = matrix[0].length;
        int sum = 0;
        for(int i = 0; i < row; i++) {
            sum = 0;
            for(int j = 0; j < col; j++) {
               sum += matrix[i][j];
                if(i == 0) {
                    res[i][j] = sum;
                }else {
                    res[i][j] = res[i - 1][j] + sum;
                }
            }
        }
    }

    public int sumRegion(int row1, int col1, int row2, int col2) {
        if(res == null)
            return 0;
       if(row1 == 0 && col1 == 0)
           return res[row2][col2];
        if(row1 == 0)
            return res[row2][col2] - res[row2][col1 - 1];
        if(col1 == 0)
            return res[row2][col2] - res[row1 - 1][col2];
        return res[row2][col2] - res[row2][col1 - 1] - res[row1 - 1][col2] + res[row1 - 1][col1 - 1];
    }
}
```
