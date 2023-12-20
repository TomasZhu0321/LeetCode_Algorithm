# String的Conversion
![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter4_String/img/String%20Conversion.png)

# String常用方法
* `length()` - 返回字符串的长度（字符数）
```
String str = "Hello";
int length = str.length(); // length = 5
```
* `charAt(int index)` - 返回指定索引处的字符。
```
char ch = str.charAt(0); // ch = 'H'
```
* `substring(int beginIndex, int endIndex)` - 返回字符串的子字符串，从beginIndex开始到endIndex结束（不包括endIndex）
```
String subStr = str.substring(1, 4); // subStr = "ell"
```
* `equals(Object anotherObject)` - 比较两个字符串的内容是否相等
```
boolean isEqual = str.equals("Hello"); // isEqual = true
```
* `startsWith(String prefix)` - 检查字符串是否以指定的前缀开始
```
boolean startsWith = str.startsWith("He"); // startsWith = true
```
* `contains(CharSequence s)` - 检查字符串中是否包含指定的字符序列
```
boolean contains = str.contains("ell"); // contains = true
```
* `indexOf(String str)` - 返回指定子字符串第一次出现的字符串内的索引
```
int index = str.indexOf("e"); // index = 1
```
* `split(String regex)` - 根据匹配给定的正则表达式来拆分字符串
```
String[] parts = "a,b,c".split(","); // parts = ["a", "b", "c"]
```
* `trim()` - 返回去除前导和尾随空格的字符串
```
String trimmedStr = " Hello ".trim(); // trimmedStr = "Hello"
```
***
# StringBuilder和常用方法
## 定义
* StringBuilder是Java处理可变字符串处理的一个类，允许**不创建新对象**的情况下修改字符串
## StringBuilder 与 String 的区别
* 可变性
  * `String` 是不可变的（immutable），每次修改字符串内容时实际上是在创建一个新的字符串对象
  * `StringBuilder` 是可变的（mutable），允许在原有对象上进行修改，避免了频繁创建新对象的开销
* Performance
  * 在频繁修改字符串内容的场景下，StringBuilder 通常比 String 更高效，因为它减少了对象创建和内存占用
* 线程安全
  * `String` 由于不可变性，天然线程安全
  * `StringBuilder` 不是线程安全的。如果需要在多线程环境中进行字符串操作，可以考虑使用 `StringBuffer`（它是线程安全的，但性能略低于 StringBuilder）
## 常用方法
* `append(..)`: 用于在当前 StringBuilder 对象末尾添加数据（可以是字符串、字符、数字等）
```
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World"); // sb = "Hello World"
```
* `insert(int offset, ...)`: 在指定位置插入数据
```
sb.insert(6, "Java "); // sb = "Hello Java World"
```
* `delete(int start, int end)`:删除字符串中从 `start` 位置开始到 `end` 位置的内容（不包含 `end` 位置的字符）
```
sb.insert(6, "Java "); // sb = "Hello Java World"
```
* `replace(int start, int end, String str)`:替换从 `start` 到 `end` 位置的字符为指定的字符串
```
sb.replace(5, 10, " Java"); // sb = "Hello Java"
```
* `reverse()`:将当前 StringBuilder 对象的字符序列逆转
```
sb.reverse(); // sb = "avaJ olleH"
```
* `toString()`:转换为 `String`
```
String str = sb.toString(); // str = "avaJ olleH"
```
