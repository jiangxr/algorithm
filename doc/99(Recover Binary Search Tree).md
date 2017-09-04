### Recover Binary Search TreeNode
描述：有一个平衡二叉树，其中有两个元素的位置出现了错误，请将其修正过来。

我的解答：
不会做，但是借助于discuss的内容，有了思路。在给出的讨论中，不仅给出了解决的方案，
而且使用O（1）的空间复杂度。非常厉害，下面我将借助于栈来实现O（N）的空间复杂度，起码得给出一种
解决方案吧。。

```java
class Solution {
    public void recoverTree(TreeNode root) {
        if(root == null)
            return;
        Stack<TreeNode> stack = new Stack<>();
        TreeNode pre = null;
        TreeNode first = null;
        TreeNode second = null;
        stack.push(root);
        TreeNode p = root;
        while(!stack.empty()) {
            if(p != null) {
                while(p.left != null) {
                    stack.push(p.left);
                    p = p.left;
                }
            }

            p = stack.pop();
            if(pre == null) {
                pre = p;
            }else {
                if(pre.val > p.val) {
                    if(first == null) {first = pre; second = p;}
                    else {second = p;}
                }
                pre = p;
            }
            p = p.right;
            if(p != null)
                stack.push(p);
        }
        if(first != null && second != null) {
            int temp = second.val;
            second.val = first.val;
            first.val = temp;
        }
    }
}
```
注：使用stack，没有达到O（1）的时间复杂度，但是在一般情况下还是能够解决问题的。主要还是如果找到
这两个被交换的元素。

网上的解法：（超级厉害，借助于线索化）
```java
class Solution {
    public void recoverTree(TreeNode root) {
        TreeNode pre = null;
        TreeNode first = null, second = null;
        // Morris Traversal
        TreeNode temp = null;
		while(root!=null){
			if(root.left!=null){
				// connect threading for root
				temp = root.left;
				while(temp.right!=null && temp.right != root)
					temp = temp.right;
				// the threading already exists
				if(temp.right!=null){
				    if(pre!=null && pre.val > root.val){
				        if(first==null){first = pre;second = root;}
				        else{second = root;}
				    }
				    pre = root;

					temp.right = null;
					root = root.right;
				}else{
					// construct the threading
					temp.right = root;
					root = root.left;
				}
			}else{
				if(pre!=null && pre.val > root.val){
				    if(first==null){first = pre;second = root;}
				    else{second = root;}
				}
				pre = root;
				root = root.right;
			}
		}
		// swap two node values;
		if(first!= null && second != null){
		    int t = first.val;
		    first.val = second.val;
		    second.val = t;
		}
    }
```
