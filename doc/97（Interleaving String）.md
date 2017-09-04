### Interleaving String

问题描述：
给出三个字符串s1, s2, s3。问s3能否由s1和s2交叉插入构成？

我的解决方法：
```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        if(s1 == null && s2 == null || s3 == null)
            return true;
        if(s3 == null)
            return false;
        if(s1 == null)
            if(s3.equals(s2)) {
                return true;
            }else {
                return false;
            }
        if(s2 == null) {
            if(s3.equals(s1)) {
                return true;
            }else {
                return false;
            }
        }
        boolean[] isExist = new boolean[1];
        dfs(s1, s2, s3, 0, 0, 0, isExist);
        return isExist[0];


    }

    public void dfs(String s1, String s2, String s3, int i, int j, int k, boolean[] isExist) {
        if(k == s3.length()) {
            if(i == s1.length() && j == s2.length())
                isExist[0] = true;
            return;
        }
        if(i == s1.length()) {
            if(s3.substring(k).equals(s2.substring(j))) {
                isExist[0] = true;
            }
            return;
        }

        if(j == s2.length()) {
            if(s3.substring(k).equals(s1.substring(i)))
                isExist[0] = true;
            return;
        }

        if(!isExist[0]) {
            if(s1.charAt(i) == s3.charAt(k)) {
                dfs(s1, s2, s3, i+1, j, k+1, isExist);
            }
        }

        if(!isExist[0]) {
            if(s2.charAt(j) == s3.charAt(k)) {
                dfs(s1, s2, s3, i, j + 1, k+1, isExist);
            }
        }
    }
}
```
出现的问题： 我的解决方案主要采用recursive call来进行找到可行的答案。但是时间复杂度过高，当数据的规模过大时，导致超时。

网上给出的一些方法：

方法一：
采用穷举法的方式，如果找不到，但是时间复杂度超高。
```java
public class Solution {
    public boolean is_Interleave(String s1,int i,String s2,int j,String res,String s3)
    {
        if(res.equals(s3) && i==s1.length() && j==s2.length())
            return true;
        boolean ans=false;
        if(i<s1.length())
            ans|=is_Interleave(s1,i+1,s2,j,res+s1.charAt(i),s3);
        if(j<s2.length())
            ans|=is_Interleave(s1,i,s2,j+1,res+s2.charAt(j),s3);
        return ans;

    }
    public boolean isInterleave(String s1, String s2, String s3) {
        return is_Interleave(s1,0,s2,0,"",s3);
    }
}
```

方法二：
这种方法和我的算法的思想挺像的，但是在一些处理方面比我的号一些。

```java
public class Solution {
    public boolean is_Interleave(String s1, int i, String s2, int j, String s3, int k, int[][] memo) {
        if (i == s1.length()) {
            return s2.substring(j).equals(s3.substring(k));
        }
        if (j == s2.length()) {
            return s1.substring(i).equals(s3.substring(k));
        }
        if (memo[i][j] >= 0) {
            return memo[i][j] == 1 ? true : false;
        }
        boolean ans = false;
        if (s3.charAt(k) == s1.charAt(i) && is_Interleave(s1, i + 1, s2, j, s3, k + 1, memo)
                || s3.charAt(k) == s2.charAt(j) && is_Interleave(s1, i, s2, j + 1, s3, k + 1, memo)) {
            ans = true;
        }
        memo[i][j] = ans ? 1 : 0;
        return ans;
    }
    public boolean isInterleave(String s1, String s2, String s3) {
        int memo[][] = new int[s1.length()][s2.length()];
        for (int i = 0; i < s1.length(); i++) {
            for (int j = 0; j < s2.length(); j++) {
                memo[i][j] = -1;
            }
        }
        return is_Interleave(s1, 0, s2, 0, s3, 0, memo);
    }
}
```
注：这种方法的关键点在于内部的if条件中的递归。

方法三：借助于一个二维数组，采用DP的方法来进行判断，感觉很厉害。从1个字符一直到m+n个字符，超厉害
```java
public class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        if (s3.length() != s1.length() + s2.length()) {
            return false;
        }
        boolean dp[][] = new boolean[s1.length() + 1][s2.length() + 1];
        for (int i = 0; i <= s1.length(); i++) {
            for (int j = 0; j <= s2.length(); j++) {
                if (i == 0 && j == 0) {
                    dp[i][j] = true;
                } else if (i == 0) {
                    dp[i][j] = dp[i][j - 1] && s2.charAt(j - 1) == s3.charAt(i + j - 1);
                } else if (j == 0) {
                    dp[i][j] = dp[i - 1][j] && s1.charAt(i - 1) == s3.charAt(i + j - 1);
                } else {
                    dp[i][j] = (dp[i - 1][j] && s1.charAt(i - 1) == s3.charAt(i + j - 1)) || (dp[i][j - 1] && s2.charAt(j - 1) == s3.charAt(i + j - 1));
                }
            }
        }
        return dp[s1.length()][s2.length()];
    }
}
```

方法四：还是使用DP，降低了空间复杂度（厉害了word哥）
```java
public class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        if (s3.length() != s1.length() + s2.length()) {
            return false;
        }
        boolean dp[] = new boolean[s2.length() + 1];
        for (int i = 0; i <= s1.length(); i++) {
            for (int j = 0; j <= s2.length(); j++) {
                if (i == 0 && j == 0) {
                    dp[j] = true;
                } else if (i == 0) {
                    dp[j] = dp[j - 1] && s2.charAt(j - 1) == s3.charAt(i + j - 1);
                } else if (j == 0) {
                    dp[j] = dp[j] && s1.charAt(i - 1) == s3.charAt(i + j - 1);
                } else {
                    dp[j] = (dp[j] && s1.charAt(i - 1) == s3.charAt(i + j - 1)) || (dp[j - 1] && s2.charAt(j - 1) == s3.charAt(i + j - 1));
                }
            }
        }
        return dp[s2.length()];
    }
}
```
