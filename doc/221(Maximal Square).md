### Maximal Square

说明：给一个矩阵，元素由0和1组成，求由1组成的最大的正方形面积。

我的解决方法：(DP)
```java
class Solution {
    public int maximalSquare(char[][] matrix) {
        if(matrix == null)
            return 0;
        if(matrix.length == 0)
            return 0;
        int row = matrix.length;
        int col = matrix[0].length;
        int[][] arr = new int[row][col];
        int[] colLen = new int[col];
        int max = 0;
        for(int i = 0; i < col; i++) {
            if(matrix[0][i] == '0') {
                arr[0][i] = 0;
                colLen[i] = 0;
            }else {
                max = 1;
                arr[0][i] = 1;
                colLen[i] = 1;
            }
        }
        int rowLen = 0;
        for(int i = 1; i < row; i++) {
            int pre = 0;
            for(int j = 0; j < col; j++) {
                if(matrix[i][j] != '0') {
                    rowLen = pre + 1;
                    colLen[j] += 1;
                }else {
                    rowLen = 0;
                    colLen[j] = 0;
                }
                if(j == 0) {
                    arr[i][0] = matrix[i][0] - '0';
                }else {
                    int tmp = Math.min(rowLen, colLen[j]);
                    if(tmp <= 1) {
                        arr[i][j] = tmp;
                    }else {
                        int tmp1 = Math.min(arr[i-1][j-1], tmp -1);
                        arr[i][j] = 1 + tmp1;
                    }

                }
                max = Math.max(max, arr[i][j] * arr[i][j]);
                pre = rowLen;
            }
        }

        return max;


    }
}
```

网上的解法：

方法一：和我的解决方法一样，但是写法比我的简洁多了。。
```java
class Solution {
    public int maximalSquare(char[][] matrix) {
        if(matrix == null)
            return 0;
        if(matrix.length == 0)
            return 0;
        int row = matrix.length;
        int col = matrix[0].length;
        int[][] arr = new int[row + 1][col + 1];
        int max = 0;
        for(int i = 1; i <= row; i++) {
            for(int j = 1; j <= col; j++) {
                if(matrix[i - 1][j - 1] == '1') {
                    arr[i][j] = Math.min(Math.min(arr[i][j - 1], arr[i-1][j-1]), arr[i-1][j]) + 1;
                    max = Math.max(max, arr[i][j]);
                }
            }
        }
        return max * max;
}
}
```
