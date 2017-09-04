### Binary Tree Level Order Traversal
说明：一次打印出每一层的元素。这些代码中错误了使用了LinkedList的方法。导致调试了半天。
这道题并没有什么特别之处，主要需要引入特殊的标志位表明每一层遍历完。

我的解决方法：
```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if(root == null)
            return result;
        LinkedList<TreeNode> queue = new LinkedList<>();
        queue.addFirst(root);
        queue.addFirst(null);
        while(queue.size() > 0) {
            List<Integer> list = new ArrayList<>();
            while(queue.peekLast() != null) {
                TreeNode node = queue.removeLast();
                if(node.left != null)
                    queue.addFirst(node.left);
                if(node.right != null)
                    queue.addFirst(node.right);
                list.add(node.val);
            }
            result.add(list);
            queue.removeLast();
            if(queue.size() > 0)
                queue.addFirst(null);
        }
        return result;
    }
}
```
