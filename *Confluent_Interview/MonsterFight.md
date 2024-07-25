# 问题
怪兽打架题，其实就是个graph题，假设有很多类似a能赢b，b能赢c…的打架胜负关系，且胜负关系transitive，开局给你个怪兽，返回你能打赢的怪兽集合，用bfs即可
![image](./img/monster_1.png)
![image](./img/monster_2.png)
![image](./img/monster_3.png)

# Code

* BFS
* 注意: if(defeated.contains(neighbor))不能省略，因为避免进入死循环
* 
```java
package org.example;

import java.util.*;

public class MonsterFight {

    public static Set<Integer> getAllDefeatableMonsters(int startMonster, List<int[]> winRelations) {
        // 创建图的邻接表表示
        Map<Integer, List<Integer>> graph = new HashMap<>();
        for (int[] relation : winRelations) {
            graph.computeIfAbsent(relation[0], k -> new LinkedList<>()).add(relation[1]);
        }

        // 使用BFS找到所有可达的节点
        Set<Integer> defeated = new HashSet<>();
        Queue<Integer> que = new LinkedList<>();
        que.offer(startMonster);
        while(!que.isEmpty()){
            int current = que.poll();
            if(graph.containsKey(current)){
                for(int neighbor : graph.get(current)){
                    //避免重复进入相同节点，死循环
                    if(!defeated.contains(neighbor)) {
                        defeated.add(neighbor);
                        que.offer(neighbor);
                    }
                }
            }
        }
        return defeated;
    }

    public static void main(String[] args) {
        List<int[]> winRelations = new ArrayList<>();
        winRelations.add(new int[]{1, 2});
        winRelations.add(new int[]{2, 3});
        winRelations.add(new int[]{3, 4});
        winRelations.add(new int[]{1, 5});
        winRelations.add(new int[]{5, 4});

        System.out.println(getAllDefeatableMonsters(1, winRelations)); // 输出: [2, 3, 4, 5]
        System.out.println(getAllDefeatableMonsters(2, winRelations)); // 输出: [4]
    }
}

```

# 问题2
![image](./img/monster.png)

## Code
```java
package org.example;

import java.util.*;

public class MonsterFight2 {

    public static String findLeastStrongMonster(List<String> monsters, Map<String, List<String>> relations, List<String> inputMonsters) {
        // 构建反向图
        Map<String, Set<String>> reverseGraph = new HashMap<>();
        for (String monster : monsters) {
            reverseGraph.put(monster, new HashSet<>());
        }
        for (String monster : relations.keySet()) {
            for (String defeated : relations.get(monster)) {
                reverseGraph.get(defeated).add(monster);
            }
        }

        // 找到所有能打赢输入列表中所有怪兽的怪兽
        Set<String> potentialMonsters = new HashSet<>(monsters);
        for (String inputMonster : inputMonsters) {
            Set<String> canDefeatInput = new HashSet<>();
            Queue<String> queue = new LinkedList<>();
            queue.add(inputMonster);

            while (!queue.isEmpty()) {
                String current = queue.poll();
                for (String neighbor : reverseGraph.get(current)) {
                    if (!canDefeatInput.contains(neighbor)) {
                        canDefeatInput.add(neighbor);
                        queue.add(neighbor);
                    }
                }
            }
            potentialMonsters.retainAll(canDefeatInput);
        }

        // 返回最弱的怪兽
        return potentialMonsters.iterator().next();
    }

    public static void main(String[] args) {
        List<String> monsters = Arrays.asList("Dragons", "Zombies", "Snakes", "Goblins");
        Map<String, List<String>> relations = new HashMap<>();
        relations.put("Dragons", Arrays.asList("Zombies", "Goblins"));
        relations.put("Zombies", Collections.singletonList("Goblins"));
        relations.put("Goblins", Collections.singletonList("Snakes"));

        List<String> inputMonsters = Arrays.asList("Snakes", "Goblins");
        System.out.println(findLeastStrongMonster(monsters, relations, inputMonsters)); // 输出: Zombies
    }
}

```