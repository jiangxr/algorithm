### Gas Station

说明：有n个加油站构成一个环，每个加油站都有gas[i]数量的油，而从i到i+1车站
需要花费cost[i]数量的油，问从哪个车站出发，能够成功走完这个环。

我的解法：
```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        if(gas == null || gas.length == 0)
            return -1;
        int n = gas.length;
        int i = 0;
        while(i < n) {
            if(gas[i] < cost[i]) {
                i++;
            }else {
                int surplus = 0;
                for(int j = 0; j < n; j++) {
                    int index = (i + j) % n;
                    if(surplus + gas[index] >= cost[index]){
                        if(j == n - 1)
                            return i;
                        surplus += gas[index] - cost[index];
                    }else {
                        if(index < i)
                            return -1;
                        else {
                            i = index + 1;
                            break;
                        }
                    }
                }
            }
        }
        return -1;
    }
}
```

网上的方法：
(定理：如果一个环的和不小于0，则肯定存在可能走完路径)
```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        if(gas == null || gas.length == 0)
            return -1;
        int n = gas.length;
        int total = 0;
        int sum = 0;
        int start = 0;
        for(int i = 0; i < n; ++i) {
            total += gas[i] - cost[i];
            if(sum < 0) {
                sum = gas[i] - cost[i];
                start = i;
            }else
                sum += gas[i] - cost[i];
        }
        return total < 0?-1:start;
    }
}
```
