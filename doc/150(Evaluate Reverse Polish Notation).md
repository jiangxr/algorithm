### Evaluate Reverse Polish Notation

说明： 计算逆波兰表达式

```java
class Solution {
    public int evalRPN(String[] tokens) {
        if(tokens == null || tokens.length == 0)
            return 0;
        Stack<Integer> stack = new Stack<>();
        int n = tokens.length;
        int i = 0;
        while(i < n) {
            if("+".equals(tokens[i])) {
                int m1 = stack.pop();
                int m2 = stack.pop();
                int m3 = m2 + m1;
                stack.push(m3);   
            }else if("-".equals(tokens[i])) {
                int m1 = stack.pop();
                int m2 = stack.pop();
                int m3 = m2 - m1;
                stack.push(m3);
            }else if("*".equals(tokens[i])) {
                int m1 = stack.pop();
                int m2 = stack.pop();
                int m3 = m2 * m1;
                stack.push(m3);
            }else if("/".equals(tokens[i])) {
                int m1 = stack.pop();
                int m2 = stack.pop();
                int m3 = m2 / m1;
                stack.push(m3);
            }else {
                stack.push(Integer.valueOf(tokens[i]));
            }
            i++;
        }
        return stack.pop();

    }
}
```
