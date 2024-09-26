# Introduction
* Classic **Space - Time** Trade-Off

# HashMap<K,V> 常用方法
* `map.put(key,value);`
* `map.remove(key);`
* `map.containsValue(value) // return boolean`
* `map.size();`
* `map.isEmpty();`
* Accessing the **set of all keys** in the map: `Set <K_Type> keys = map.keySet(); // return all the keys, and put in the Set `
* Accessing the **collection of all values** in the map:`Collection <V_Type> values = map.values();`
*  `Set<Map.Entry<Key_Type, Value_Type>> entries = map.entrySet();`

```java
    HashMap<String, String> map = new HashMap<>();
    map.put("name", "John");
    map.put("age", "30");
    map.put("city", "Toronto");

    // 获取所有键
    Set<String> keys = map.keySet();
    Collection <String> values = map.values();

    // 使用 for-each 循环遍历键
    for (String key : keys) {
        System.out.println("Key: " + key);
        // 通过键获取值
        String value = map.get(key);
        System.out.println("Value: " + value);
    }
```
* `int value = map.getOfDefault(key, default); //如果有key，返回对应 value；没有key返回default的值`
* `map.putIfAbsent(key,value); //key不存在的时候，插入key-value； key存在，不覆盖`
* `int value = map.computeIfAbsent(key, k -> mappingFunction); 如果键不存在并且通过映射函数生成了一个新值，那么它返回生成的这个新值。如果键已经存在，则返回该键当前关联的现有值。`
```java
    Map<String, Integer> map = new HashMap<>();
    map.put("apple", 5);

    // "banana" 不存在，映射函数会计算新值并插入
    int value1 = map.computeIfAbsent("banana", key -> key.length());
    System.out.println("Value1: " + value1);  // 输出 6, 因为 "banana" 的长度为 6

    // "apple" 已存在，不会重新计算，返回现有值
    int value2 = map.computeIfAbsent("apple", key -> key.length());
    System.out.println("Value2: " + value2);  // 输出 5, 因为 "apple" 已存在，原值为 5

    System.out.println(map);  // 输出 {apple=5, banana=6}
```

# HashSet<E> 常用方法
* `set.add(value);`
* `set.contains(value);`
* 只能loop来获取数据(没有get)
* `new ArrayList(set)` 能够将set里面的内容自动转换成对应数据类型
  * e.g.`List<List<Integer>> res = new ArrayList(set);` `Set<List<Integer>> set = new HashSet<>();`
* Set能够自动比较看两个list是否相同（顺序+内容都要相同）
  
# LeetCode
## Essentials
* [1. Two Sum](https://leetcode.com/problems/two-sum/description/)
* [383. Random Note](https://leetcode.com/problems/ransom-note/)

## Recommended
* [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/)
* [380. Insert Delete GetRandom O(1)](https://leetcode.com/problems/insert-delete-getrandom-o1/)
* [41. First Missing Positive](https://leetcode.com/problems/first-missing-positive/)
* [146. LRU Cache](https://leetcode.com/problems/lru-cache/description/)
* [432. All O one Data Structure](https://leetcode.com/problems/all-oone-data-structure/description/)

