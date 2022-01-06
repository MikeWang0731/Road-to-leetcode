---
description: Judge Statements
cover: >-
  https://images.unsplash.com/photo-1639387438195-ca9325a04ba1?crop=entropy&cs=srgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHJhbmRvbXx8fHx8fHx8fDE2NDE0MzA3MTY&ixlib=rb-1.2.1&q=85
coverY: -404.1928934010152
---

# 👍 判断语句

## 478 · 简单计算器<mark style="color:blue;">（入门）</mark>

### 题目要求

给出两个整数 _a_ , _b_ ,以及一个操作符 _opeator，返回运算结果_

```java
a = 1
b = 2
operator = +

result = 3
```

### 解决方案

用switch判断操作符的类型

```java
public class Calculator {
    /**
     * @param a: An integer
     * @param operator: A character, +, -, *, /.
     * @param b: An integer
     * @return: The result
     */
    public int calculate(int a, char operator, int b) {
        // write your code here
        switch(operator){
            case '+':
                return a + b;
            case '-':
                return a - b;
            case '*':
                return a * b;
            case '/':
                return (int)(a / b);
        }
        return 0;
    }
}
```

## 283 · 三数之中的最大值<mark style="color:blue;">（入门）</mark>

### 题目要求

给三个整数，求他们中的最大值。

```
样例  1:
	输入:  num1 = 1, num2 = 9, num3 = 0
	输出: 9
	
	样例解释: 
	返回三个数中最大的数。

样例 2:
	输入:  num1 = 1, num2 = 2, num3 = 3
	输出: 3
	
	样例解释: 
	返回三个中最大的数字。
```

### 解决方案

先比较前两个，选出“最大”；再用“最大”和第三个比。

```java
public class Solution {
    /**
     * @param num1: An integer
     * @param num2: An integer
     * @param num3: An integer
     * @return: an interger
     */
    public int maxOfThreeNumbers(int num1, int num2, int num3) {
        // write your code here
        int max = 0;
        if (num1 > num2) {
            max = num1;
        } else {
            max = num2;
        }
        if (max > num3) {
            return max;
        }
        return num3;
    }
}
```

## 145 · 大小写转换<mark style="color:blue;">（入门）</mark>

### 题目要求

将一个字符由小写字母转换为大写字母

```
输入: 'a'
输出: 'A'
```

### 解决方案

首先将char类型转换为String，再通过String的`toUpperCase()`方法将小写转大写

```java
public class Solution {
    /**
     * @param character: a character
     * @return: a character
     */
    public char lowercaseToUppercase(char character) {
        // write your code here
        String str = String.valueOf(character);
        return str.toUpperCase().charAt(0);
    }
}
```

## 23 · 判断数字与字母字符<mark style="color:blue;">（入门）</mark>

### 题目要求

给出一个字符`c`，如果它是一个数字或字母，返回`true`，否则返回`false`。

### 解决方案

如果c在a-z或A-Z或0-9之间，就返回true。

```java
public class Solution {
    /**
     * @param c: A character.
     * @return: The character is alphanumeric or not.
     */
    public boolean isAlphanumeric(char c) {
        // write your code here
        return (c >= 'a' & c <= 'z') || (c >= 'A' & c <= 'Z') || (c >= '0' & c <= '9');
    }
}
```

## 1141 · 月份天数<mark style="color:green;">（简单）</mark>

### 题目要求

给定年份和月份，返回这个月的天数。

```
输入: 
2020 
2
输出: 
29
```

### 解决方案

一定一定要注意**闰年的判断方式**！

1. 普通年份能被4整除，且不能被100整除的，是闰年。（如2004年就是闰年）
2. 世纪年份能被400整除的是闰年。（如2000年是闰年，1900年不是闰年）

```java
public class Solution {
    /**
     * @param year: a number year
     * @param month: a number month
     * @return: Given the year and the month, return the number of days of the month.
     */
    public int getTheMonthDays(int year, int month) {
        // write your code here
        boolean TwentyNineDaysInFeb = false;
        // 年号除以四，没余是闰年 -> 这是不完全的！！！
        if (year % 400 == 0 || (year % 4 == 0 && year % 100 != 0)) {
            TwentyNineDaysInFeb = true;
        }

        switch (month) {
            case 1: return 31;
            case 2: 
                if (TwentyNineDaysInFeb) {
                    return 29;
                } else {
                    return 28;
                }
            case 3: return 31;
            case 4: return 30;
            case 5: return 31;
            case 6: return 30;
            case 7: return 31;
            case 8: return 31;
            case 9: return 30;
            case 10: return 31;
            case 11: return 30;
            case 12: return 31;
        }

        return 0;
    }
}
```

## 766 · 闰年<mark style="color:green;">（简单）</mark>

### 题目要求

判断给出的年份 `n` 是否为闰年. 如果 `n` 为闰年则返回 `true`

```
输入 : n = 2008
输出 : true
```

### 解决方案

这一题跟上一题的核心思想是一样的

```java
public class Solution {
    /**
     * @param n: a number represent year
     * @return: whether year n is a leap year.
     */
    public boolean isLeapYear(int n) {
        // write your code here
        if (n % 400 == 0 || (n % 4 == 0 && n % 100 != 0)) {
            return true;
        }
        return false;
    }
}
```
