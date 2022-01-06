---
description: Basic Data Type
coverY: 0
---

# 👍 基础数据结构

## 37 · 反转一个三位整数<mark style="color:blue;">（入门）</mark>

### 题目要求

翻转一个只有三位数的整数

```
Input: 123
Output: 321
```

```
Input = 900
Output = 9
```

### 解决方案一（不完美）

我的想法是将数字解析为char类型array，然后反向读取数组里面的每一个元素，将结果添加到新的字符串。最后将字符串解析为Int型数据。

```java
public int reverseInteger(int number) {

        // 将数字转换为字符串类型
        String numStr = String.valueOf(number);
        System.out.println("numArr = " + numStr);

        // 将字符串转换为char array
        char[] numCharArr = numStr.toCharArray();
        System.out.println("Char Array:" + Arrays.toString(numCharArr));

        // 定义一个变量接收反转后结果
        StringBuilder reverseResult = new StringBuilder();
        // 从数组的最后一位开始取，逐个向前遍历，将每个遍历到的元素添加到reverseResult
        for (int i = numCharArr.length - 1; i >= 0; i--) {
            reverseResult.append(numCharArr[i]);
        }

        // 将字符型转换为整数型
        return Integer.parseInt(reverseResult.toString());
    }
```

### 解决方案二（标准）

通过运算分别获取百位，十位和个位，然后倒着相加

```java
public class Solution {
    /*
     * @param number: A 3-digit number.
     * @return: Reversed number.
     */
    public int reverseInteger(int number) {
        // write your code here
        //获得个位数
        int num1 = number % 10;
        //获得十位数
        int num2 = (number / 10) % 10;
        //获得百位数
        int num3 = ((number / 10) / 10) % 10;
        //相加
        return num3 + num2 * 10 + num1 * 100;
    }
}
```

例如，number = 321。

个位数：321 % 10 = 1

十位数：(321 / 10) = 32     32 % 10 = 2

百位数： (321 / 10) / 10 = 3     3 % 10 = 3

## 1 · A + B 问题<mark style="color:blue;">（入门）</mark>

### 题目要求

返回两个数相加的和

```
Sample:
a = 2
b = 1

Result:
3
```

### 解决方案一（标准）

就是最普通的 `return a+b`

```java
public int aplusb(int a, int b) {
        // write your code here
        return a + b;
    }
```

### 解决方案二

位运算

```java
public int aplusb(int a, int b) {
        // 主要利用异或运算来完成 
        // 异或运算有一个别名叫做：不进位加法
        // 那么a ^ b就是a和b相加之后，该进位的地方不进位的结果
        // 然后下面考虑哪些地方要进位，自然是a和b里都是1的地方
        // a & b就是a和b里都是1的那些位置，a & b << 1 就是进位
        // 之后的结果。所以：a + b = (a ^ b) + (a & b << 1)
        // 令a' = a ^ b, b' = (a & b) << 1
        // 可以知道，这个过程是在模拟加法的运算过程，进位不可能
        // 一直持续，所以b最终会变为0。因此重复做上述操作就可以
        // 求得a + b的值。
        while (b != 0) {
            int _a = a ^ b;
            int _b = (a & b) << 1;
            a = _a;
            b = _b;
        }
        return a;
    }
```

## 1300 · 巴什博弈<mark style="color:green;">（简单）</mark>

### 题目要求

你正在和朋友玩一个游戏：桌子上有一堆石头，每一次你们都会从中拿出1到3个石头。拿走最后一个石头的人赢得游戏。游戏开始时，你是先手。

假设两个人都绝对理性，都会做出最优决策。给定石头的数量，判断你是否会赢得比赛。

举例：有四个石头，那么你永远不会赢得游戏。不管拿几个，最后一个石头一定会被你的朋友拿走。

```
输入：n = 4 
输出：False
解析：先手取走1,2或者3，对方都会取走最后一个

输入：n = 5 
输出：True
解析：先手拿1个，必胜
```

### 解决方案

分析题目我们可以发现，如果场上的石头数量可以被四整除（取余数为０），则一定会输。那么我们就可以认为 `if (stone % 4 == 0) return false;`

```java
public boolean canWinBash(int n) {
        // Write your code here
        if(n % 4==0) return false;
        return true;
    }
```

## 764 · 计算圆周长和面积<mark style="color:green;">（简单）</mark>

### 题目要求

给定一个整数`r`代表一个圆的半径。\
你的任务是返回一个数组。\
其中数组的第一个元素代表圆的周长，数组的第二个元素代表圆的面积。

```
输入 : r = 2
输出 : [12.56, 12.56]
```

### 解决方案

这个就非常常规

```java
public double[] calculate(int r) {
        double PI = 3.14;
        // write your code here
        double round = 2 * PI * r;
        double area = PI * r * r;

        return new double[]{round, area};
    }
```
