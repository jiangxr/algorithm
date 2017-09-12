### Word Ladder II

说明： 找到所有的将S转为T的最短路径

分析：不会，参考答案，是先进行BFS构造grapth，然后根据构造的图进行dfs

```java
class Solution {
    Map<String,List<String>> map;
    List<List<String>> results;
    public List<List<String>> findLadders(String start, String end, List<String> WordList) {
        results= new ArrayList<List<String>>();
        if (WordList.size() == 0)
            return results;

        Set<String> dict = new HashSet<>();
        for(String s: WordList)
            dict.add(s);

        int min=Integer.MAX_VALUE;

        Queue<String> queue= new ArrayDeque<String>();
        queue.add(start);

        map = new HashMap<String,List<String>>();

        Map<String,Integer> ladder = new HashMap<String,Integer>();
        for (String string:dict)
            ladder.put(string, Integer.MAX_VALUE);
        ladder.put(start, 0);

        dict.add(end);
        //BFS: Dijisktra search
        while (!queue.isEmpty()) {

            String word = queue.poll();

            int step = ladder.get(word)+1;//'step' indicates how many steps are needed to travel to one word.

            if (step>min) break;

            for (int i = 0; i < word.length(); i++){
                StringBuilder builder = new StringBuilder(word);
                for (char ch='a';  ch <= 'z'; ch++){
                    builder.setCharAt(i,ch);
                    String new_word=builder.toString();
                    if (ladder.containsKey(new_word)) {

                        if (step>ladder.get(new_word))//Check if it is the shortest path to one word.
                            continue;
                        else if (step<ladder.get(new_word)){
                            queue.add(new_word);
                            ladder.put(new_word, step);
                        }
                        if (map.containsKey(new_word)) //Build adjacent Graph
                            map.get(new_word).add(word);
                        else{
                            List<String> list= new LinkedList<String>();
                            list.add(word);
                            map.put(new_word,list);
                        }

                        if (new_word.equals(end))
                            min=step;

                    }
                }
            }
        }

        //BackTracking
        LinkedList<String> result = new LinkedList<String>();
        backTrace(end,start,result);

        return results;
    }
    private void backTrace(String word,String start,List<String> list){
        if (word.equals(start)){
            list.add(0,start);
            results.add(new ArrayList<String>(list));
            list.remove(0);
            return;
        }
        list.add(0,word);
        if (map.get(word)!=null)
            for (String s:map.get(word))
                backTrace(s,start,list);
        list.remove(0);
    }
}
```
