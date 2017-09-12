### Word Break

说明：给一个字符串s和一个字符串dict，问能否由dict中的字符串构成
s。

网上的解法：
解法一：

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        if(s == null || s.length() == 0)
            return true;
        Set<String> set = new HashSet<>();
        for(String ss: wordDict) {
            set.add(ss);
        }
        int n = s.length();
        boolean[] res = new boolean[n + 1];
        res[0] = true;
        for(int i = 1; i <= n; i++) {
            StringBuilder sb = new StringBuilder(s.substring(0, i));
            for(int j = 0; j < i; j ++) {
                if(set.contains(sb.toString()) && res[j]) {
                    res[i] = true;
                    break;
                }
                sb.deleteCharAt(0);
            }
        }
        return res[n];
    }
}
```
