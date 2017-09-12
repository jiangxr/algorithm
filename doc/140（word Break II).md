### Word Break II

说明： 给定字符串S和字符串列表list，通过list的字符串构造成S，找到所有的组合。

我的解法：
TMD又超时了。

```java
class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        if(s == null || s.length() == 0)
            return new ArrayList<String>();
        int n = s.length();
        Set<String> set = new HashSet<>();
        for(String ss : wordDict)
            set.add(ss);
        boolean[] isExist = new boolean[n + 1];
        isExist[0] = true;
       List<String>[] res = new ArrayList[n + 1];
       for(int i = 1; i <= n; i++) {
           StringBuilder sb = new StringBuilder(s.substring(0, i));
           ArrayList<String> temp = new ArrayList<>();
           for(int j = 0; j < i; j++) {
               if(set.contains(sb.toString()) && isExist[j]) {
                   isExist[i] = true;
                   if(j == 0) {
                      temp.add(sb.toString());
                   }else {
                       for(String tt:res[j]) {
                           temp.add(tt + " " + sb.toString());
                       }
                   }
               }
               sb.deleteCharAt(0);
           }
           res[i] = temp;
       }
        return res[n];

    }
}
```

网上的解法：DFS
```java
class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        Set<String> set = new HashSet<>();
        for(String ss : wordDict)
            set.add(ss);
        return dfs(s, set, new HashMap<String, LinkedList<String>>());
    }

    public List<String> dfs(String s, Set<String> set, HashMap<String, LinkedList<String>> map) {
        if(map.containsKey(s)) {
            return map.get(s);
        }
        if(s.length() == 0) {
            List<String> ll = new LinkedList<String>();
            ll.add("");
            return ll;
        }
        LinkedList<String> res = new LinkedList<>();
        for(String ss : set) {
            if(s.startsWith(ss)) {
                List<String> subList = dfs(s.substring(ss.length()), set, map);
                for(String sub : subList) {
                    res.add(ss + (sub.isEmpty()?"" : " ") + sub);
                }
            }
        }
        map.put(s, res);
        return res;
    }
}
```
