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