### Palindrome Partitioning II

说明：将一个字符串分割为不同的子串，使其子串都是回文。问最少的
分割次数是多少？

我的解决方法：
超时了，但是测试用例基本通过了.

```java
class Solution {
    public int minCut(String s) {
        if(s == null || s.length() <= 1)
            return 0;
        int n = s.length();
        int[] cuts = new int[n+1];
        cuts[0] = 0;
        cuts[1] = 1;
        for(int i = 1; i < n; i++) {
            int min =  Integer.MAX_VALUE;
            for(int j = 0; j <= i; j++) {
                if(isPalindrome(s, j, i)) {
                    if(cuts[j] + 1 < min )
                        min = cuts[j] + 1;
                }
            }
            cuts[i + 1] = min;
        }
        return cuts[n] - 1;

    }

    public boolean isPalindrome(String s, int lo, int hi) {
        while(lo < hi) {
            if(s.charAt(lo) != s.charAt(hi))
                return false;
            lo++;
            hi--;
        }
        return true;
    }
}
```

优化回文的判断：
```java
class Solution {
    public int minCut(String s) {
        if(s == null || s.length() <= 1)
            return 0;
        int n = s.length();
        int[] cuts = new int[n+1];
        cuts[0] = 0;
        cuts[1] = 1;
        boolean[][] isPar = new boolean[n][n];
        for(int i = 1; i < n; i++) {
            int min =  Integer.MAX_VALUE;
            for(int j = 0; j <= i; j++) {
                if(s.charAt(j) == s.charAt(i) && (i <= j+1 || isPar[j+1][i-1])) {
                    isPar[j][i] = true;
                    if(cuts[j] + 1 < min )
                        min = cuts[j] + 1;
                }
            }
            cuts[i + 1] = min;
        }
        return cuts[n] - 1;

    }

}
```

网上的解法：

方法一：
说明：对于每一个值，采用向两边扩展更新的策略，不需要每次都和
所有的进行比较
```java
class Solution {
    public int minCut(String s) {
        if(s == null || s.length() <= 1)
            return 0;
        int n = s.length();
        int[] cuts = new int[n+1];
        for(int i = 0; i <= n; i++)
            cuts[i] = i - 1;
        for(int i = 0; i < n; i++) {
            for(int j = 0; i - j >= 0 && i + j < n && s.charAt(i - j) == s.charAt(i + j); j++)
                cuts[i + j + 1] = Math.min(cuts[i + j + 1], 1 + cuts[i -j]);
            for(int j = 1; i - j + 1 >= 0 && i + j < n && s.charAt(i - j + 1) == s.charAt(i + j); j++)
                cuts[i + j + 1] = Math.min(cuts[i + j + 1], 1 + cuts[i - j + 1]);
        }
        return cuts[n];
    }

}
```

方法二：
```java
class Solution {
    public int minCut(String s) {
        if(s == null || s.length() <= 1)
            return 0;
        int n = s.length();
        boolean[][] isPar = new boolean[n][n];
        int[] d = new int[n];
        for(int i = n - 1; i >= 0; i--) {
            d[i] = n - i - 1;
            for(int j = i; j < n; j++) {
                if(s.charAt(i) == s.charAt(j) && (j - i < 2 || isPar[i+1][j-1])) {
                    isPar[i][j] =  true;
                    if(j == n -1)
                        d[i] = 0;
                    else if(d[j + 1] + 1 < d[i])
                        d[i] = d[j + 1] + 1;
                }
            }
        }
        return d[0];
    }

}
```
