---
description: Array and Loop
cover: >-
  https://images.unsplash.com/photo-1641062245493-b242af3ff5bb?crop=entropy&cs=srgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHJhbmRvbXx8fHx8fHx8fDE2NDE0MzA3MTY&ixlib=rb-1.2.1&q=85
coverY: 0
---

# 👍 数组与循环

## 485 · 生成给定大小的数组<mark style="color:blue;">（入门）</mark>

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

## 484 · 交换数组两个元素<mark style="color:blue;">（入门）</mark>

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

## 463 · 整数排序<mark style="color:blue;">（入门）</mark>

### 题目要求

给一组整数，按照升序排序，使用选择排序，冒泡排序，插入排序或者任何 O(n2) 的排序算法。

```
样例  1:
	输入:  [3, 2, 1, 4, 5]
	输出:  [1, 2, 3, 4, 5]
	
	样例解释: 
	返回排序后的数组
```

### 解决方案

选择排序：两个指针，第一个指基准，第二个找最小，找到最小时交换基准和最小，然后继续寻找

```java
public class Solution {
    /**
     * 使用选择排序
     * @param A: an integer array
     * @return: nothing
     */
    public void sortIntegers(int[] array) {
        // write your code here
        for (int i = 0; i < array.length; i++) {
            int minimum = i;
            for (int j = i; j < array.length; j++) {
                if (array[j] < array[minimum]) {
                    minimum = j;
                }
            }
            swap(array, i, minimum);
        }
    }

    private static void swap(int[] arr, int currentIndex, int minIndex) {
        // 将当前值和最小值交换
        int temp = arr[currentIndex];
        arr[currentIndex] = arr[minIndex];
        arr[minIndex] = temp;
    }
}
```

## 214 · 数组的最大值<mark style="color:blue;">（入门）</mark>

### 题目要求

给一个浮点数数组，求数组中的最大值。

```
输入:  [1.0, 2.1, -3.3]
输出: 2.1	
样例解释: 返回最大的数字
```

### 解决方案

就是普通的找最大值：记录下初始最大值（默认index=0），从index=1开始找，如果有当前值比最大值大，就更新这个最大值。遍历完整个数组之后返回这个最大值。

```java
public class Solution {
    /**
     * @param A: An integer
     * @return: a float number
     */
    public float maxOfArray(float[] A) {
        // write your code here
        int maxIndex = 0; 
        for (int i = 1; i < A.length; i++) {
            if (A[i] > A[maxIndex]) {
                maxIndex = i;
            }
        }
        return A[maxIndex];
    }
}
```

## 25 · 打印X<mark style="color:blue;">（入门）</mark>

### 题目要求

输入一个正整数`N`， 你需要按样例的方式返回一个字符串列表。

```
Input: n = 5
Output: ["X   X", " X X ", "  X  ", " X X ", "X   X"]
Refer to:
X   X 
 X X  
  X   
 X X  
X   X 
```

### 解决方案

```java
public class Solution {
    public List<String> printX(int n) {     
        ArrayList<String> res=new ArrayList<>();//创建一个存放String类型属性的ArrayList，名称为res
        char[] line=new char[n];//创建一个长度为n的字符型数组line
        for(int i=0;i<n;i++){//外循环遍历正整数n的次数
            for(int j=0;j<n;j++){//该循环为了辅助初始化字符型数组中的每个属性
                line[j]=' ';//初始化字符型数组中的每个属性
            }
            line[i]='X';//左边对应位置赋值X
            line[n-i-1]='X';//右边对应位置赋值X
            res.add(String.valueOf(line));//将得到的line转换成字符串的形式增加到ArrayList
        }
        return res;//返回ArrayList
    }
}
```

## 298 · 寻找素数<mark style="color:blue;">（入门）</mark>

### 题目要求

输出n以内所有的素数。

```
输入：5
输出：[2, 3, 5]
```

### 解决方案

参考网页：

{% embed url="https://zhidao.baidu.com/question/47414759.html" %}

```java
public class Solution {
    /**
     * @param n: an integer
     * @return: return all prime numbers within n.
     */
    public List<Integer> prime(int n) {
        // write your code here
        List<Integer> result = new ArrayList<>();
        boolean isPrime = true;
        // 因为结果要包含n这个数，所以是i<=n
        for (int i = 2; i <= n; i++) {
            for (int j = 2; j < i; j++) {
                if (i % j == 0) {
                    isPrime = false;
                }
            }
            if (isPrime) result.add(i);
            isPrime = true;
        }
        return result;
    }
}
```

## 297 · 寻找最大值<mark style="color:blue;">（入门）</mark>

### 题目要求

寻找 n 个数中的最大值。

```
输入：[1, 2, 3, 4, 5]
输出：5
```

### 解决方案

使用Collections里的`max()`方法

```java
public class Solution {
    /**
     * @param nums: the list of numbers
     * @return: return the maximum number.
     */
    public int maxNum(List<Integer> nums) {
        // write your code here
        int num = Collections.max(nums);
        return num;
    }
}
```

## 1334 · 旋转数组<mark style="color:green;">（简单）</mark>

### 题目要求

给定一个数组，将数组向右移动k步，其中k为非负数。

```
输入: [1,2,3,4,5,6,7], k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右旋转1步: [7,1,2,3,4,5,6]
向右旋转2步: [6,7,1,2,3,4,5]
向右旋转3步: [5,6,7,1,2,3,4]
```

### 解决方案 （我自己的）

分类讨论，切片复制，最后组合

<mark style="color:red;">注意：旋转的次数是可能大于数组长度的！！需要求出真正有效的旋转次数！！</mark>

```java
public class Solution {
    /**
     * @param nums: an array
     * @param k: an integer
     * @return: rotate the array to the right by k steps
     */
    public int[] rotate(int[] nums, int k) {
        // 如果数组只有一个数，不管旋转几次都是它自己，直接返回
        if (nums.length == 1) return nums;
        // 对于数组长度大于一的情况
        // 1. 旋转次数 < 数组长度: 正常处理
        // 2. 旋转次数 > 数组长度：对k和length进行取余数运算，计算出真正旋转的次数(例如，长度为7的数组旋转10次，前7次结束后还是它本身，真正有效果的为后三次 10 % 7 = 3)
        if (k > nums.length) {
            k = k % nums.length;
        }
        // 如果数组只有两个数，当k为1的时候就相当于交换；否则就还是它本身
        if (nums.length == 2 & k == 1) {
            swap(nums, 0, 1);
            return nums;
        } else if (nums.length == 2 & k != 1) {
            return nums;
        }
        // 切片：选择出要被旋转的
        int[] waitForRotate = Arrays.copyOfRange(nums, nums.length-k, nums.length);
        // 切片：选择出不变的(剩下的)那一些
        int[] unchanged =  Arrays.copyOfRange(nums, 0, nums.length-k);
        // 新建一个结果数组，将“被旋转”的复制进来，并且设定该数组长度为原数组的长度
        int[] result = Arrays.copyOf(waitForRotate, nums.length);
        // 将“剩下的”复制进“结果数组”，从“剩下的”index为0的地方开始复制，“结果数组”最后一位开始粘贴，复制的长度为“剩下的”数组的长度
        System.arraycopy(unchanged, 0, result, waitForRotate.length, unchanged.length);
        
        return result;
    }

    private static void swap(int[] arr, int a, int b) {
        int temp = arr[a];
        arr[a] = arr[b];
        arr[b] = temp;
    }
}
```

### 解决方案（<mark style="color:green;">排名第一</mark>）

```java
public class Solution {
    /**
     * @param nums: an array
     * @param k: an integer
     * @return: rotate the array to the right by k steps
     */
    public int[] rotate(int[] nums, int k) {
        // Write your code here
        int len = nums.length;
        k = k % len;
        int[] ret = new int[len];
        for (int i = 0; i < len; i++) {
            ret[i] = nums[(i + len - k) % len];
        }
        return ret;
    }
}
```

## Question Title

### 题目要求



### 解决方案&#x20;

## Question Title

### 题目要求



### 解决方案
