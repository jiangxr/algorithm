### Word Ladder

说明：给定两个字符串S和T，和一个字符串列表list，问从S变为T总共需要
多少步？  
约束条件：  
（1）S每次只能变换一个字符
（2）S变换的之间字符串必须在list中

我的解决方法：
注：从S到T，现在list中找字符串只和S字符串相差一个字符的所有字符串。
并把这些字符串排除掉。然后针对新找到的字符换再从list中相差一个字符的
字符串。按照相同过程，直到找到对应的T为止。首先找到的序列长度即为最短长度。

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> set = new HashSet<>();
        for(String s : wordList) {
            set.add(s);
        }
        if(!set.contains(endWord)) {
            return 0;
        }

        if(beginWord.equals(endWord))
            return 0;

        List<String> list = new ArrayList<>();
        list.add(beginWord);
        int index = 0;
        int size = list.size();
        int level = 1;
        while(index <= size){
            if(index == size) {
                if(size == list.size()) {
                    break;
                }else {
                    level++;
                    index = size;
                    size = list.size();
                }
            }
            if(set.size() == 0)
                break;
            Iterator<String> it = set.iterator();
            int length = set.size();
            for(int j = 0; j < length; j++) {
                String ss = it.next();
                if(differNum(list.get(index), ss) == 1) {
                    list.add(ss);
                    it.remove();
                    if(ss.equals(endWord)) {
                        level++;
                        return level;
                    }
                }
            }
            index++;
        }
        return 0;

    }

    private int differNum(String s, String t) {
        int count = 0;
        for(int i = 0; i < s.length(); i++) {
            if(s.charAt(i) != t.charAt(i))
                count++;
        }
        return count;
    }
}
```

网上的解决方案：

方法一：
说明：和我的方法挺像的，但是此方法的从两端分别走是个好的想法。
因为所有的字母都是小写的字符，不需要从list出发。每个字符的变化只能从'a'到'z'
```java
public class Solution {

public int ladderLength(String beginWord, String endWord, Set<String> wordList) {
	Set<String> beginSet = new HashSet<String>(), endSet = new HashSet<String>();

	int len = 1;
	int strLen = beginWord.length();
	HashSet<String> visited = new HashSet<String>();

	beginSet.add(beginWord);
	endSet.add(endWord);
	while (!beginSet.isEmpty() && !endSet.isEmpty()) {
        //select less elements from beginSet and endSet
		if (beginSet.size() > endSet.size()) {
			Set<String> set = beginSet;
			beginSet = endSet;
			endSet = set;
		}

		Set<String> temp = new HashSet<String>();
		for (String word : beginSet) {
			char[] chs = word.toCharArray();


			for (int i = 0; i < chs.length; i++) {
				for (char c = 'a'; c <= 'z'; c++) {
					char old = chs[i];
					chs[i] = c;
					String target = String.valueOf(chs);

					if (endSet.contains(target)) {
						return len + 1;
					}

					if (!visited.contains(target) && wordList.contains(target)) {
						temp.add(target);
						visited.add(target);
					}
					chs[i] = old;
				}
			}
		}

		beginSet = temp;
		len++;
	}

	return 0;
}
}
```

方法二：BFS
```java
public class Solution {

public int ladderLength(String beginWord, String endWord, List<String> wordList) {
    Set<String> wordSet = new HashSet();
    for(String s: wordList)
        wordSet.add(s);
    if(!wordSet.contains(endWord))
        return 0;
	Queue<String> queue = new LinkedList<>();
    queue.add(beginWord);
    queue.add(null);
    Set<String> visited = new HashSet<>();
    visited.add(beginWord);

    int level = 1;
    while(!queue.isEmpty()) {
        String s = queue.poll();
        if(s != null) {
            char[] c = s.toCharArray();
            for(int i = 0; i < c.length; i++) {
                char temp = c[i];
                for(int j = 0; j < 26; j++) {
                    c[i] = (char)('a' + j);
                    String ss = new String(c);

                    if(ss.equals(endWord))
                        return level + 1;

                    if(!visited.contains(ss) && wordSet.contains(ss)) {
                        visited.add(ss);
                        queue.add(ss);
                    }

                }
                c[i] = temp;
            }
        }else {
            if(!queue.isEmpty()) {
                level++;
                queue.add(null);
            }
        }
    }
    return 0;
}
}
```
