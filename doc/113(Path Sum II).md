### Path Sum II

说明：找到所有的路径是使其路径节点元素之和等于一个给定的常数

分析：采用dfs即可。主要是每次找到路径之后如何存储

我的解决方法：
```java
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> result = new ArrayList<>();
        dfs(root, sum, 0, new ArrayList<Integer>(), result);
        return result;

    }

    public void dfs(TreeNode root, int sum, int total, List<Integer> list, List<List<Integer>> result) {
        if(root == null)
            return;
        if(root.left == null && root.right == null && total + root.val == sum) {
            List<Integer> temp = new ArrayList<>(list);
            temp.add(root.val);
            result.add(temp);
            return;
        }
        List<Integer> temp2 = new ArrayList<>(list);
        temp2.add(root.val);
        dfs(root.left, sum, total + root.val, temp2, result );
        dfs(root.right, sum, total + root.val, temp2, result );

    }
}
```

网上的方案：

方法一：
注：和我的方法一样，只是本方法对List的处理比我好。。
```java
public List<List<Integer>> pathSum(TreeNode root, int sum){
	List<List<Integer>> result  = new LinkedList<List<Integer>>();
	List<Integer> currentResult  = new LinkedList<Integer>();
	pathSum(root,sum,currentResult,result);
	return result;
}

public void pathSum(TreeNode root, int sum, List<Integer> currentResult,
		List<List<Integer>> result) {

	if (root == null)
		return;
	currentResult.add(new Integer(root.val));
	if (root.left == null && root.right == null && sum == root.val) {
		result.add(new LinkedList(currentResult));
    //这一步好给力。。
		currentResult.remove(currentResult.size() - 1);//don't forget to remove the last integer
		return;
	} else {
		pathSum(root.left, sum - root.val, currentResult, result);
		pathSum(root.right, sum - root.val, currentResult, result);
	}
	currentResult.remove(currentResult.size() - 1);
}

```
