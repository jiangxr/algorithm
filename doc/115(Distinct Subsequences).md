### Distinct Subsequences

说明：给定两个字符串S和T，问通过在S中删除一些字符构成一个新的字符串
和T字符串相同的可能性。

我的解法：
注：我的解法是通过穷举法，通过递归直接可以得到，但是时间复杂度过高，未能通过，
不用说，正确的解法肯定得需要DP。

```java
class Solution {
    public int numDistinct(String s, String t) {
        int[] count = new int[1];
        if(s == null || t == null)
            return 0;
        if(s.length() == 0 && t.length() == 0)
            return 1;
        if(s.length() == 0)
            return 0;
        if(t.length() == 0)
            return 1;
        dfs(s, t, 0, s.length() - 1, 0, t.length() - 1, count );
        return count[0];
    }

    public void dfs(String s, String t, int slo, int shi, int tlo, int thi, int[] count) {
        if(tlo > thi) {
            count[0] += 1;
            return;
        }

        if(slo < shi)
            dfs(s, t, slo+1, shi, tlo, thi, count);
        if(slo <= shi && s.charAt(slo) == t.charAt(tlo)) {
            dfs(s, t, slo+1, shi, tlo+1, thi, count);
        }
    }
}
```

网上的解法：
说明：首先强调的是我的解法是不可取的，是最笨拙的解法。

方法一：
说明：写法超级简单，只是思路真是想不到。哎，这样的题还是得总结下。
重要的还是得抽象出动态规划的方程。如果能够把动态规划方程抽象出来就比较好写了。
动态规划方程
```
nums[i+1][j+1]表示有S0...j包含T0...i的次数
nums[0][j] = 1 j=0...s.length()
nums[i+1][j+1] = nums[i+1][j] if t.charAt(i) != s.chaAt(j)
nums[i+1][j+1] = nums[i][j] + nums[i+1][j] if t.charAt(i) == s.chaAt(j)
```
```java
class Solution {
    public int numDistinct(String s, String t) {
        int[][] num = new int[t.length() + 1][s.length() + 1];
        for(int i = 0; i <= s.length(); i++) {
            num[0][i] = 1;
        }

        for(int i = 0; i < t.length(); i++) {
            for(int j = 0; j < s.length(); j++) {
                if(t.charAt(i) == s.charAt(j)) {
                    num[i+1][j+1] = num[i][j] + num[i+1][j];
                }else
                    num[i+1][j+1] = num[i+1][j];
            }
        }
        return num[t.length()][s.length()];
    }
}
```
