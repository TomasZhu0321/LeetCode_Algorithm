# 题目
![image](./img/varadic_1.png)
![image](./img/varadic_2.png)
![image](./img/varadic_3.png)
题目细节补充:
* 设计一个interface，能够register不同的函数以及他们的参数类型，之后能按照参数类型进行查询
* 
## 可能问题
### 1. What is an optimal solution for this?
### 2. If getFunction(string, integer...) how to handle?
### 3. If getFunction(string, null) where null can stands for all the possibilities
### 4. Implement two follow ups above

## 第一问
![image](./img/isVariabic_solu1.jpeg)
![image](./img/isVariabic_solu2.jpeg)
```java
package org.example;

import java.util.*;

class TrieNode {
    HashMap<String, TrieNode> children;
    List<String> isVarTrue;
    List<String> isVarFalse;
    TrieNode(){
        this.children = new HashMap<>();
        this.isVarFalse = new ArrayList<>();
        this.isVarTrue = new ArrayList<>();
    }
}
class Function {
    String name;
    List<String> argumentTypes;
    boolean isVariadic;
    Function(String name, List<String> argumentTypes, boolean isVariadic){
        this.name = name;
        this.argumentTypes = argumentTypes;
        this.isVariadic = isVariadic;
    }
}
class FunctionLibrary{
    private TrieNode root;
    FunctionLibrary(){
        this.root = new TrieNode();
    }
    public void register(Set<Function> functionSet){
        for(Function f: functionSet){
            insert(f.name,f.argumentTypes,f.isVariadic);
        }
    }
    public List<String> findMatches(List<String> argumentTypes){
        TrieNode current = root;
        List<String> result = new ArrayList<>();
        for(int i = 0 ; i < argumentTypes.size(); i ++){
            String arg = argumentTypes.get(i);
            if(!current.children.containsKey(arg)){
                return result;
            }else {
                current = current.children.get(arg);
                if(i != argumentTypes.size() - 1 && !current.isVarTrue.isEmpty()){
                    if(allSame(argumentTypes.subList(i,argumentTypes.size()),arg)){
                        result.addAll(current.isVarTrue);
                    }
                }
                if(i == argumentTypes.size() - 1){
                    result.addAll(current.isVarTrue);
                    result.addAll(current.isVarFalse);
                }
            }
        }
        return result;
    }
    private void insert(String functionName, List<String> arguments, boolean isVariable){
        TrieNode current = root;
        for(String arg:arguments){
            current = current.children.computeIfAbsent(arg, k -> new TrieNode());
        }
        if(isVariable){
            current.isVarTrue.add(functionName);
        }else {
            current.isVarFalse.add(functionName);
        }
    }
    private boolean allSame(List<String> listInput, String arg){
        for(String str:listInput){
            if(!str.equals(arg)){
                return false;
            }
        }
        return true;
    }

    public static void main(String[] args) {
        FunctionLibrary functionLibrary = new FunctionLibrary();
        Set<Function> inputSet = new HashSet<>();
        inputSet.add(new Function("FuncA", Arrays.asList("String", "Integer", "Integer"), false));
        inputSet.add(new Function("FuncB", Arrays.asList("String", "Integer"), true));
        inputSet.add(new Function("FuncC", Arrays.asList("Integer"), true));
        inputSet.add(new Function("FuncD", Arrays.asList("Integer", "Integer"), true));
        inputSet.add(new Function("FuncE", Arrays.asList("Integer", "Integer", "Integer"), false));
        inputSet.add(new Function("FuncF", Arrays.asList("String"), false));
        inputSet.add(new Function("FuncG", Arrays.asList("Integer"), false));
        functionLibrary.register(inputSet);

        System.out.println("Print match:");
        System.out.println(functionLibrary.findMatches(Arrays.asList("String"))); // [FuncF]
        System.out.println(functionLibrary.findMatches(Arrays.asList("Integer"))); // [FuncC, FuncG]
        System.out.println(functionLibrary.findMatches(Arrays.asList("Integer", "Integer", "Integer", "Integer"))); // [FuncC, FuncD]
        System.out.println(functionLibrary.findMatches(Arrays.asList("String", "Integer", "Integer", "Integer"))); // [FuncB]
        System.out.println(functionLibrary.findMatches(Arrays.asList("String", "Integer", "Integer"))); // [FuncA, FuncB]
    }
}
```