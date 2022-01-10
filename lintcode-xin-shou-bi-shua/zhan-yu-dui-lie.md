---
description: Stack and Queue
cover: >-
  https://images.unsplash.com/photo-1641451618985-58ab5f347e6b?crop=entropy&cs=srgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHJhbmRvbXx8fHx8fHx8fDE2NDE4Mzk4MzQ&ixlib=rb-1.2.1&q=85
coverY: 0
---

# 👍 栈与队列

## 771 · 二阶阶乘<mark style="color:green;">（简单）</mark>

### 题目要求

给定一个数`n`，返回该数的二阶阶乘。在数学中，正整数的[二阶阶乘](https://en.wikipedia.org/wiki/Double\_factorial)表示不超过这个正整数且与它有相同奇偶性的所有正整数乘积。

```
输入: n = 5
输出: 15
解释:
5!! = 5 * 3 * 1 = 15
```

### 解决方案

常规方案，使用if循环判断奇偶，再用for循环取范围内的奇数或偶数，然后相乘

```java
public class Solution {
    /**
     * @param n: the given number
     * @return:  the double factorial of the number
     */
    public long doubleFactorial(int n) {
        // Write your code here
        // 获取基准数：偶数就是2，奇数就是1
        long result = n % 2 == 0 ? 2:1;
        // 如果是奇数就循环取出范围内的所有奇数，并相乘；否则就取偶数
        if (result == 1) {
            // 这里的循环时从3开始，因为1已经在result里了，不需要重复获取
            for (int i = 3; i <= n; i++) {
                if (i % 2 != 0) {
                    result = result * i;
                }   
            }
        } else {
            // 这里的循环时从4开始，因为2已经在result里了，不需要重复获取
            for (int i = 4; i <= n; i++) {
                if (i % 2 == 0) {
                    result = result * i;
                }   
            }
        }
        return result;
    }
}
```

### 解决方案二（递归）

不论是奇数还是偶数，每两个数之间都相差2。所以，不论奇偶，只要不断地“减二相乘”，就可以得到结果。

```java
public class Solution {
    /**
     * @param n: the given number
     * @return:  the double factorial of the number
     */
    public long doubleFactorial(int n) {
        if (n <= 2) {
            return n;
        } 
        return n * doubleFactorial(n - 2);
    }
}va
```

## 495 · 实现栈<mark style="color:green;">（简单）</mark>

### 题目要求

实现一个栈，可以使用除了栈之外的数据结构。

### 解决方案

使用ArrayList

栈（Stack）是一个先进后出的数据结构，**添加和删除元素均在栈顶进行操作，即数组尾部。**

```java
public class Stack {
    /*
     * @param x: An integer
     * @return: nothing
     */

    // 使用ArrayList实现Stack：栈是一个先进后出的数据结构(First in Last out)
    ArrayList<Integer> array = new ArrayList<>();
    public void push(int x) {
        // 入栈：将元素加入栈顶(e.g. Bottom-0-Head - Bottom-0-1-Head)
        // 等价于将元素加入数组尾部
        array.add(x);
    }

    public void pop() {
        // 出栈：将栈顶的元素删除(e.g. Bottom-0-1-Head - Bottom-0-Head)
        // 等价于将数组的最后一个元素删除
        array.remove(array.size()-1);
    }

    public int top() {
        // 查看顶层元素：等价于查看数组的最后一个元素
        return array.get(array.size()-1);
    }

    public boolean isEmpty() {
        // 判断空栈：等价于看数组长度是不是0
        return array.isEmpty();
    }
}
```

## 492 · 队列维护<mark style="color:green;">（简单）</mark>

### 题目要求

按链表实现队列。支持以下基本方法：

1. `enqueue(item)`.将新元素放入队列中。
2. `dequeue()`. 将第一个元素移出队列，返回它。

### 解决方案

使用LinkedList实现Queue：Queue是一个先入先出的数据结构，相当于**从数组尾部加入元素，从顶部取出元素。**

```java
public class MyQueue {
    /*
     * @param item: An integer
     * @return: nothing
     */

    LinkedList<Integer> list = new LinkedList<>();
    public void enqueue(int item) {
        // write your code here
        list.add(item);
    }

    /*
     * @return: An integer
     */
    public int dequeue() {
        // write your code here
        int num = list.remove(0);
        return num;
    }
}
```

## 423 · 有效的括号序列

### 题目要求

给定一个字符串所表示的括号序列，包含以下字符： `'(', ')'`, `'{'`, `'}'`, `'['` and `']'`， 判定是否是有效的括号序列。

括号必须依照 `"()"` 顺序表示， `"()[]{}"` 是有效的括号，但 `"([)]"` 则是无效的括号。

```
输入："([)]"
输出：False
```

### 解决方案

使用栈的特征来做匹配

```java
import java.util.Stack;

public class Solution {
    /**
     * @param s: A string
     * @return: whether the string is a valid parentheses
     */
    public boolean isValidParentheses(String s) {
        // 使用Stack来存储括号（括号匹配满足先入后出的特性）
         Stack<Character> myStack = new Stack<>();
         // 遍历String里的每个符号
         for (int i = 0; i < s.length(); i++) {
             char c = s.charAt(i);
            //  如果是左侧括号就入栈
             if (c == '(' || c == '[' || c == '{') {
                 myStack.push(c);
             } else {
                //  如果不是左侧
                // 如果此时栈空，就return false，因为没有左侧括号出现
                 if (myStack.isEmpty()) return false;
                 // 如果是某一个括号没有其对应括号从栈内弹出，就说明匹配失败
                 if (c == ')' && myStack.pop() != '(') return false;
                 if (c == '}' && myStack.pop() != '{') return false;
                 if (c == ']' && myStack.pop() != '[') return false;
             }
         }
         // 如果全部执行完且最后栈空，就说明匹配成功
         return myStack.isEmpty();
    }

```

## 263 · 小括号匹配

### 题目要求

给定一个字符串所表示的括号序列，包含以下字符： `'(', ')'`， 判定是否是有效的括号序列。

括号必须依照 `"()"` 顺序表示， `"()"` 是有效的括号，但 `")("` 则是无效的括号。

```
input = "((()))"
output = true

input = "((())("
output = false
```

### 解决方案

跟上面一题一模一样

```java
import java.util.*;;
public class Solution {
    /**
     * @param string: A string
     * @return: whether the string is a valid parentheses
     */
    public boolean matchParentheses(String string) {
        // write your code here
        Stack<Character> myStack = new Stack<>();
        for (int i = 0; i < string.length(); i++) {
            char c = string.charAt(i);
            if (c == '(') {
                myStack.push(c);
            } else {
                if (myStack.isEmpty()) return false;
                if (c == ')' && myStack.pop() != '(') return false;
            }
        }
        return myStack.isEmpty();
    }
}
```
