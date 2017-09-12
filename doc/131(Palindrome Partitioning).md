### Palindrome Partitioning

说明： 给一个字符串，将其分成一个个子串，使其每一个子串都是回文，找到
所有的可能的分法。

我的解决方案：

```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<List<String>>> list = new ArrayList<>();
        List<List<String>> list0 = new ArrayList<>();
        if(s == null || s.length() == 0)
            return list0;
        List<String> temp = new ArrayList<>();
        temp.add(s.substring(0, 1));
        list0.add(temp);
        list.add(list0);
        for(int i = 1; i < s.length(); i++) {
            List<List<String>> temp1 = new ArrayList<>();
            for(List<String> ll : list.get(i - 1)) {
                List<String> temp2 = new ArrayList<>(ll);
                temp2.add(s.substring(i, i+1));
                temp1.add(temp2);
            }
            if(isPalindrome(s, 0, i)) {
                temp1.add(new ArrayList<String>(Arrays.asList(s.substring(0, i+1))));
            }
            for(int j = 1; j <= i - 1; j++) {
                if(isPalindrome(s, j, i)) {
                    for(List<String> ll : list.get(j-1)) {
                        List<String> temp3 = new ArrayList<>(ll);
                        temp3.add(s.substring(j, i+1));
                        temp1.add(temp3);
                    }
                }
            }

            list.add(temp1);   
        }
        return list.get(s.length() - 1);
    }


    private boolean isPalindrome(String s, int lo, int hi) {
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

网上的方法：

方法一：（使用backtrack）
```java
public class Solution {
        List<List<String>> resultLst;
	    ArrayList<String> currLst;
	    public List<List<String>> partition(String s) {
	        resultLst = new ArrayList<List<String>>();
	        currLst = new ArrayList<String>();
	        backTrack(s,0);
	        return resultLst;
	    }
	    public void backTrack(String s, int l){
	        if(currLst.size()>0 //the initial str could be palindrome
	            && l>=s.length()){
	                List<String> r = (ArrayList<String>) currLst.clone();
	                resultLst.add(r);
	        }
	        for(int i=l;i<s.length();i++){
	            if(isPalindrome(s,l,i)){
	                if(l==i)
	                    currLst.add(Character.toString(s.charAt(i)));
	                else
	                    currLst.add(s.substring(l,i+1));
	                backTrack(s,i+1);
	                currLst.remove(currLst.size()-1);
	            }
	        }
	    }
	    public boolean isPalindrome(String str, int l, int r){
	        if(l==r) return true;
	        while(l<r){
	            if(str.charAt(l)!=str.charAt(r)) return false;
	            l++;r--;
	        }
	        return true;
	    }
}
```

方法二：和我的思路一样.
```java
public class Solution {
 	public static List<List<String>> partition(String s) {
		int len = s.length();
		List<List<String>>[] result = new List[len + 1];
		result[0] = new ArrayList<List<String>>();
		result[0].add(new ArrayList<String>());

		boolean[][] pair = new boolean[len][len];
		for (int i = 0; i < s.length(); i++) {
			result[i + 1] = new ArrayList<List<String>>();
			for (int left = 0; left <= i; left++) {
				if (s.charAt(left) == s.charAt(i) && (i-left <= 1 || pair[left + 1][i - 1])) {
					pair[left][i] = true;
					String str = s.substring(left, i + 1);
					for (List<String> r : result[left]) {
						List<String> ri = new ArrayList<String>(r);
						ri.add(str);
						result[i + 1].add(ri);
					}
				}
			}
		}
		return result[len];
	}
}
```
