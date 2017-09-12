### Is Subsequence


说明：给定两个字符串s和t，问s是否是t的子串，通过在
t中删除一些元素构成s。

方法一：
```java
class Solution {
    public boolean isSubsequence(String s, String t) {
        if(s ==  null || s.length() == 0)
            return true;

        int sLen = s.length();
        int tLen = t.length();
        int i = 0;
        int j = 0;
        while(j < tLen) {
            if(s.charAt(i) == t.charAt(j))
                i++;
            j++;
            if(i == sLen)
                return true;
        }
        return false;
    }
}
```

方法二：
```java
class Solution {
    public boolean isSubsequence(String s, String t) {
        if(s ==  null || s.length() == 0)
            return true;
        int index = 0;
        for(int i = 0; i < s.length(); i++) {
            index = t.indexOf(s.charAt(i), index);
            if(index == -1) return false;
            index++;
        }
        return true;
    }
}
```
