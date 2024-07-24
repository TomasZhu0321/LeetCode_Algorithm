# 题目
打游戏求最少生命量，一个人要打游戏，目的是打败每一个level的对手，一开始的level有n个对手，initial_players[i]对应每个对手的strength，然后给一个名为next_players的list，代表每增加一个level，会加进来的player的strength。他的目标是在每一个level打败strength排在第rank个的player（加进来新的player时，前面的player不改变），而他每打败一个人，他的血量会减去这个play‍‌‌‍‍‌‍‍‍‍‍‍‌‌‌‌‌‍‍‌er的strength，要保证他打到最后血量大于等于0，求初始最少需要的生命值。这题我维护了一个size为rank的minheap （是的，我理解的是维护一个size为rank的PQ，每一个level把新加入的player信息加进去之后，就知道目前第rank的人是谁，根据这个strength去update血量）

Sure, here's the translation of the problem into English:

## Problem Description

A player needs to play a game with the goal of defeating the opponents at each level. Initially, there are `n` opponents in the first level, with `initial_players[i]` representing the strength of each opponent. Additionally, there is a list named `next_players` that represents the strength of the players added at each subsequent level.

The player's objective is to defeat the opponent with the strength ranked at position `rank` in each level (when new players are added, the opponents from previous levels remain unchanged). Each time the player defeats an opponent, their health decreases by the strength of that opponent. The goal is to ensure the player's health is greater than or equal to zero by the end of all levels. Determine the minimum initial health required for the player to achieve this.

You maintained a min-heap (priority queue) of size `rank` to solve this problem. Each time a new player is added, you update the heap to determine the current player ranked at position `rank` and update the player's health accordingly.

### Input
- `int[] initial_players`: An array representing the strength of opponents in the initial level.
- `List<Integer> next_players`: A list representing the strength of new players added at each subsequent level.
- `int rank`: The rank of the opponent the player needs to defeat at each level (1-based index).

### Output
- `int`: The minimum initial health required for the player to ensure they can defeat the necessary opponents at each level without their health dropping below zero.

### Example
```plaintext
initial_players = [3, 1, 4, 1, 5]
next_players = [9, 2, 6, 5, 3]
rank = 3

Output: 10
Explanation: The player needs to defeat the opponent with the 3rd highest strength at each level.
```

By maintaining a min-heap of size `rank`, you can efficiently determine the opponent's strength at the `rank` position at each level and update the player's health accordingly.

# Code
```java
package org.example;

import java.util.Collections;
import java.util.PriorityQueue;
import java.util.List;

public class GameLevel {
    public static int minimumInitialHealth(int[] initialPlayers, List<Integer> nextPlayers, int rank) {
        // 使用一个最小堆
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        int initialHealth = 0;

        // 初始化堆，加入初始对手
        for (int strength : initialPlayers) {
            minHeap.offer(strength);
            if (minHeap.size() > rank) {
                minHeap.poll();
            }
        }
        // 计算初始生命值，加入初始对手中的第rank强对手的力量值
        initialHealth += minHeap.peek();
        // 处理每一个新加入的对手
        for (int newPlayer : nextPlayers) {
            minHeap.offer(newPlayer);
            if (minHeap.size() > rank) {
                System.out.println(minHeap.poll());
            }
            System.out.println("Peek" +  minHeap.peek());
            initialHealth += minHeap.peek();
        }

        return initialHealth;
    }

    public static void main(String[] args) {
        int[] initialPlayers = {3, 1, 4, 1, 5};
        List<Integer> nextPlayers = List.of(9, 2, 6, 5, 3);
        int rank = 3;

        int result = minimumInitialHealth(initialPlayers, nextPlayers, rank);
        System.out.println("Minimum initial health required: " + result); //
    }
}
```