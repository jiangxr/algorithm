###  Binary Tree Level Order Traversal II

描述：给定一个二叉树，从最底层开始遍历二叉树。

分析：我是借助两个LinkedList来完成的， 首先将所有的数据放到一个链表中，然后从最底层的数据开始遍历。
但是实际中我对null的控制出现了问题，导致调试了半天。

我的解决方法：
```java
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if(root == null)
            return result;
        LinkedList<TreeNode> origin = new LinkedList<>();

        LinkedList<Integer> actual = new LinkedList<>();
        origin.addFirst(root);
        origin.addFirst(null);
        while(origin.size() > 0) {
            actual.addLast(null);
            while(origin.peekLast() != null) {
                TreeNode node = origin.removeLast();
                actual.addLast(node.val);
                if(node.left != null)
                    origin.addFirst(node.left);
                if(node.right != null)
                    origin.addFirst(node.right);
            }
            origin.removeLast();
            if(origin.size() > 0)
                origin.addFirst(null);
        }

        while(actual.size() > 0) {
            LinkedList<Integer> list =  new LinkedList<>();
            while(actual.peekLast() != null) {
                list.addFirst(actual.removeLast());
            }
            result.add(list);
            actual.removeLast();
        }
        return result;    
    }

}
```
网上的解决方案：

BFS:
```java
public class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        List<List<Integer>> wrapList = new LinkedList<List<Integer>>();

        if(root == null) return wrapList;

        queue.offer(root);
        while(!queue.isEmpty()){
            int levelNum = queue.size();
            List<Integer> subList = new LinkedList<Integer>();
            for(int i=0; i<levelNum; i++) {
                if(queue.peek().left != null) queue.offer(queue.peek().left);
                if(queue.peek().right != null) queue.offer(queue.peek().right);
                subList.add(queue.poll().val);
            }
            wrapList.add(0, subList);
        }
        return wrapList;
    }
}
```

DFS
```java
public class Solution {
        public List<List<Integer>> levelOrderBottom(TreeNode root) {
            List<List<Integer>> wrapList = new LinkedList<List<Integer>>();
            levelMaker(wrapList, root, 0);
            return wrapList;
        }

        public void levelMaker(List<List<Integer>> list, TreeNode root, int level) {
            if(root == null) return;
            if(level >= list.size()) {
                list.add(0, new LinkedList<Integer>());
            }
            levelMaker(list, root.left, level+1);
            levelMaker(list, root.right, level+1);
            list.get(list.size()-level-1).add(root.val);
        }
    }
```
