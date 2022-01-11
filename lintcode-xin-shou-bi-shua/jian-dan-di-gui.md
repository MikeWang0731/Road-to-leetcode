---
description: Basic Recursive
cover: >-
  https://images.unsplash.com/photo-1639625555610-63f16b664434?crop=entropy&cs=srgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHJhbmRvbXx8fHx8fHx8fDE2NDE4NzI2ODE&ixlib=rb-1.2.1&q=85
coverY: 366.5811417575369
---

# 👍 简单递归

## 366 · 斐波纳契数列<mark style="color:blue;">（入门）</mark>

<mark style="color:red;">这个数列的第一项是0，第二项是1；这个数列从第三项开始，每一项都等于前两项之和。</mark>

### 题目要求

查找斐波纳契数列中第 N 个数。

斐波纳契数列的前10个数字是：

`0, 1, 1, 2, 3, 5, 8, 13, 21, 34 ...`

### 解决方案一（记忆递归）

{% embed url="https://www.runoob.com/java/method-fibonacci.html" %}

```java
class Solution {
    /**
     * @param n: an integer
     * @return an integer f(n)
     */
    public int fibonacci(int n) {
        // 记忆下来第一个数和第二个数
        int a = 0;
        int b = 1;
        // 通过for循环更新“前两个数”
        // 因为第三个数是前两个数之和，直觉以为是(i<=n-1)，但是是从0数起，即(i<=n-2 或 i<n-1)
        for (int i = 0; i < n - 1; i++) {
            int c = a + b;
            a = b;
            b = c;
        }
        return a;
    }
}
```

### 解决方案二（标准递归）

但这种方法在某些网站会显示“超时”。

```java
public static int fibonacci(int number) {
        if ((number == 0) || (number == 1))
            return number;
        else
            return fibonacci(number - 1) + fibonacci(number - 2);
    }
```

## 68 · 二叉树的后序遍历<mark style="color:green;">（简单）</mark>

### 题目要求

给出一棵二叉树，返回其节点值的后序遍历。

### 解决方案

常规后序遍历：先左再右再自己

```java
public class Solution {
    /**
     * @param root: A Tree
     * @return: Postorder in ArrayList which contains node values.
     */
    List<Integer> result = new ArrayList<>();
    public List<Integer> postorderTraversal(TreeNode root) {
        // write your code here
        if (root == null) {
            return result;
        } else {
            postorderTraversal(root.left);
            postorderTraversal(root.right);
            result.add(root.val);
        }
        return result;
    }
}
```

## 67 · 二叉树的中序遍历<mark style="color:green;">（简单）</mark>

### 题目要求

给出一棵二叉树,返回其中序遍历。

### 解决方案

```java
public class Solution {
    /**
     * @param root: A Tree
     * @return: Inorder in ArrayList which contains node values.
     */
    List<Integer> array = new ArrayList<>();
    public List<Integer> inorderTraversal(TreeNode root) {
        // write your code here
        if (root == null) {
            return array;
        } else {
            inorderTraversal(root.left);
            array.add(root.val);
            inorderTraversal(root.right);
        }
        return array;
    }
}
```

## 66 · 二叉树的前序遍历<mark style="color:green;">（简单）</mark>

### 题目要求

给出一棵二叉树，返回其节点值的前序遍历。

### 解决方案

```java
public class Solution {
    /**
     * @param root: A Tree
     * @return: Preorder in ArrayList which contains node values.
     */
    List<Integer> array = new ArrayList<>();
    public List<Integer> preorderTraversal(TreeNode root) {
        // write your code here
        if (root == null) {
            return array;
        } else {
            array.add(root.val);
            preorderTraversal(root.left);
            preorderTraversal(root.right);
        }
        return array;
    }
}
```



