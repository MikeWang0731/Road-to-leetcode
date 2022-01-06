---
description: Array and Loop
cover: >-
  https://images.unsplash.com/photo-1641062245493-b242af3ff5bb?crop=entropy&cs=srgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHJhbmRvbXx8fHx8fHx8fDE2NDE0MzA3MTY&ixlib=rb-1.2.1&q=85
coverY: 0
---

# 👍 数组与循环

## 485 · 生成给定大小的数组（入门）

### 题目要求

给你一个大小size,生成一个元素`从1 到 size`的数组。

```
样例 1:
	输入:  size = 4
	输出: [1, 2, 3, 4]
	
	样例解释: 
	 返回一个顺序填充1到4的数组。
```

### 解决方案

使用for循环向数组内添加元素并返回

```java
public class Solution {
    /**
     * @param size: An integer
     * @return: An integer list
     */
    public List<Integer> generate(int size) {
        // write your code here
        List<Integer> array = new ArrayList<>();
        for (int i = 1; i <= size; i++) {
            array.add(i);
        }
        return array;
    }
}
```

## 484 · 交换数组两个元素

### 题目要求

给你一个数组和两个索引，交换下标为这两个索引的数字。

```
输入:  [1, 2, 3, 4], index1 = 2, index2 = 3
输出:  交换后你的数组应该是[1, 2, 4, 3]， 不需要返回任何值，只要就地对数组进行交换即可。
样例解释: 就地交换，不需要返回值。
```

### 解决方案

采用最基础的数组取值`Array[index]`来取出两个目标值，然后交换。

```java
public class Solution {
    /**
     * @param A: An integer array
     * @param index1: the first index
     * @param index2: the second index
     * @return: nothing
     */
    public void swapIntegers(int[] A, int index1, int index2) {
        // write your code here
        if (A[index1] == A[index2]) {
            return;
        } else {
            int tmp = A[index1];
            A[index1] = A[index2];
            A[index2] = tmp;
        }
    }
}java
```

## Question Title

### 题目要求



### 解决方案
