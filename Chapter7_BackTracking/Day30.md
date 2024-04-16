# 332. Reconstruct Itinerary
* **一刷:60:22(❌)**
* [332. Reconstruct Itinerary](https://leetcode.com/problems/reconstruct-itinerary/)

## 知识点
### 1. Map/List/String的相关操作
* **map.getOrDefault(key, 初始化)** ：map获取key对应的value，如果key不存在，初始化
* **(String类型的值A).compareTo(String类型的值B)**: return 的是一个int，依次比较字典顺序abcdefg..
  * == 0：相等
  * \>0: A的字典顺序大于B
  * <0: A的字典顺序小于B
* LinkedList类型的 **.add(index, 插入内容)** :在指定位置插入具体内容，并且**之后的内容的index依次往后挪动！！！**
* LinkedList类型的 **.add(插入内容)**: 默认在末尾添加
* List内容单独取出来，添加了，他就直接加上去了
## Code 
### 思路
* 通过
```java
if(backTracking(tmp)){
    return true;
}
```
这一步来确保**没有走错**！！ ==>他是存在走错的情况的，也就是当走到null或者isEmpty但是tickets没有取完的情况，就是走错了，需要回溯！
```java
class Solution {
    int total;
    Map<String, List<String>> map = new HashMap<>();
    List<String> res = new LinkedList<>();

    public List<String> findItinerary(List<List<String>> tickets) {
        // store tickets into map
        total = tickets.size() + 1;
        for (int i = 0; i < tickets.size(); i++) {
            storeMap(tickets.get(i));
        }
        backTracking("JFK");
        return res;
    }

    private void storeMap(List<String> singleTicket) {
        String key = singleTicket.get(0);
        String value = singleTicket.get(1);
        List<String> mapValues = map.getOrDefault(key, new LinkedList<>());
        if (mapValues.isEmpty()) {
            mapValues.add(value);
            map.put(key, mapValues);
        } else {
            int sizeOfValues = mapValues.size();
            for (int i = 0; i < sizeOfValues; i++) {
                if (value.compareTo(mapValues.get(i)) < 0) {
                    mapValues.add(i, value);
                    return;
                }
            }
            mapValues.add(sizeOfValues,value);
        }
    }

    private boolean backTracking(String start) {
        res.add(start);
        if (total == res.size()) {
            return true;
        }
        List<String> values = map.get(start);
        if (values != null && !values.isEmpty() ) {
            String tmp ;
            for (int i = 0; i < values.size(); i++) {
                tmp = values.remove(i);
                if(backTracking(tmp)){
                    return true;
                }
                values.add(i,tmp);
                res.removeLast();
            }
        }
        return false;
    }
}
```