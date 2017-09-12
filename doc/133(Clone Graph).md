### Clone Graph

说明：进行图的复制

我的解决方法：

```java
public class Solution {
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        if(node == null)
            return null;
        Map<Integer, UndirectedGraphNode> map = new HashMap<>();
        Queue<UndirectedGraphNode> queue = new LinkedList<>();
        HashSet<UndirectedGraphNode> set =new HashSet<>();
        UndirectedGraphNode head = null;
        queue.offer(node);
        set.add(node);
        while(!queue.isEmpty()) {
            UndirectedGraphNode temp = queue.poll();
            List<UndirectedGraphNode> neighbors = temp.neighbors;
            UndirectedGraphNode newNode = null;
            if(map.containsKey(temp.label))
                newNode = map.get(temp.label);
            else {
                newNode = new UndirectedGraphNode(temp.label);
                map.put(temp.label, newNode);
            }
            if(head == null)
                head = newNode;
            for(UndirectedGraphNode temp2 : neighbors) {
                if(!set.contains(temp2)) {
                    set.add(temp2);
                    queue.offer(temp2);
                }
                if(map.containsKey(temp2.label)) {
                    newNode.neighbors.add(map.get(temp2.label));
                }else {
                   UndirectedGraphNode temp3 = new UndirectedGraphNode(temp2.label);
                    map.put(temp2.label, temp3);
                    newNode.neighbors.add(temp3);

                }
            }
        }
        return head;

    }
}
```

网上的方法：dfs

```java
public class Solution {
    private Map<Integer, UndirectedGraphNode> map = new HashMap<>();
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        if(node == null)
            return null;
        return clone(node);
    }

    private UndirectedGraphNode clone(UndirectedGraphNode node) {
        if(map.containsKey(node.label))
            return map.get(node.label);
        UndirectedGraphNode newNode = new UndirectedGraphNode(node.label);
        map.put(node.label, newNode);
        for(UndirectedGraphNode temp : node.neighbors) {
            newNode.neighbors.add(clone(temp));
        }
        return newNode;
    }
}
```
