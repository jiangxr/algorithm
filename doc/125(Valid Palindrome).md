### Valid Palindrome

说明：判断给定的字符串是否是回文，忽略大小写，只考虑字母和数字。

我的解决方法：
```java
import java.util.regex.*;
class Solution {
    public boolean isPalindrome(String s) {
        if(s == null || s.length() <= 1)
            return true;
        int i = 0, j = s.length() - 1;
        while(i < j) {
            while(i < j && !Pattern.matches("^\\w$", String.valueOf(s.charAt(i)))) {
                i++;
            }
            while(i < j && !Pattern.matches("^\\w$", String.valueOf(s.charAt(j))) ) {
                j--;
            }

            if(i < j && !String.valueOf(s.charAt(i)).toLowerCase().equals(String.valueOf(s.charAt(j)).toLowerCase())) {
                return false;
            }
            i++;
            j--;

        }
        return true;
    }
}
```

网上的解决方法：直接使用Character这个类。
```java
public class Solution {
    public boolean isPalindrome(String s) {
        if (s.isEmpty()) {
        	return true;
        }
        int head = 0, tail = s.length() - 1;
        char cHead, cTail;
        while(head <= tail) {
        	cHead = s.charAt(head);
        	cTail = s.charAt(tail);
        	if (!Character.isLetterOrDigit(cHead)) {
        		head++;
        	} else if(!Character.isLetterOrDigit(cTail)) {
        		tail--;
        	} else {
        		if (Character.toLowerCase(cHead) != Character.toLowerCase(cTail)) {
        			return false;
        		}
        		head++;
        		tail--;
        	}
        }

        return true;
    }
}
```
