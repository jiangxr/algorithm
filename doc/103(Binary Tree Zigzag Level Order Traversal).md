### Binary Tree Zigzag Level Order Traversal
说明：给一个二叉树，根据之字形遍历二叉树。这道题的关键之处在于通过什么标记来表明是
从左往右遍历，还是从右往左遍历。并且明白数据进入的顺序是什么样的。

```java
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if(root == null)
            return result;
        //0表示从左往右，1表示从右往左
        int i = 0;
        LinkedList<TreeNode> queue = new LinkedList<>();
        queue.addFirst(root);
        queue.addFirst(null);
        while(queue.size() > 1) {
            List<Integer> list = new ArrayList<>();
            if(i == 0) {
                while(queue.peekLast() != null) {
                    TreeNode node = queue.removeLast();
                    if(node.left != null) {
                        queue.addFirst(node.left);
                    }
                    if(node.right != null) {
                        queue.addFirst(node.right);
                    }
                    list.add(node.val);

                }
                i = 1;
            }else {
                while(queue.peekFirst() != null) {
                    TreeNode node = queue.removeFirst();
                    if(node.right != null)
                        queue.addLast(node.right);
                    if(node.left != null)
                        queue.addLast(node.left);
                    list.add(node.val);
                }
                i = 0;
            }
            result.add(list);
        }
        return result;
    }
}
```

网上的解决方法：
注：使用递归的方式，使用DFS的方式，将每个元素添加到对应的lis中。
感觉能使用这个写出来，作者真是对DFS有着比较深刻的理解。
```java
public class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root)
    {
        List<List<Integer>> sol = new ArrayList<>();
        travel(root, sol, 0);
        return sol;
    }

    private void travel(TreeNode curr, List<List<Integer>> sol, int level)
    {
        if(curr == null) return;

        if(sol.size() <= level)
        {
            List<Integer> newLevel = new LinkedList<>();
            sol.add(newLevel);
        }

        List<Integer> collection  = sol.get(level);
        if(level % 2 == 0) collection.add(curr.val);
        else collection.add(0, curr.val);

        travel(curr.left, sol, level + 1);
        travel(curr.right, sol, level + 1);
    }
}
```
