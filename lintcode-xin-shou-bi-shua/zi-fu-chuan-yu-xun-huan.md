---
description: String and Loop
cover: >-
  https://images.unsplash.com/photo-1641409802543-bccc19f683ed?crop=entropy&cs=srgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHJhbmRvbXx8fHx8fHx8fDE2NDE3NjIwMzY&ixlib=rb-1.2.1&q=85
coverY: -289.92944194996795
---

# 👍 字符串与循环

## 241 · 转换字符串到整数（容易版）<mark style="color:blue;">（入门）</mark>

### 题目要求

给一个字符串, 转换为整数。你可以假设这个字符串是一个有效整数的字符串形式， 且范围在32位整数之间。

### 解决方案

```java
public class Solution {
    /**
     * @param target: A string
     * @return: An integer
     */
    public int stringToInteger(String target) {
        // write your code here
        return Integer.valueOf(target);
    }
}
```

## 146 · 大小写转换 II<mark style="color:blue;">（入门）</mark>

### 题目要求

将一个字符串中的小写字母转换为大写字母。不是字母的字符不需要做改变。

```
输入: str = "aBc"
输出: "ABC"
```

### 解决方案

```java
public class Solution {
    /**
     * @param letters: A string
     * @return: A string
     */
    public String lowercaseToUppercase2(String letters) {
        // write your code here
        return letters.toUpperCase();
    }
}
```

## 13 · 字符串查找<mark style="color:blue;">（入门）</mark>

### 题目要求

对于一个给定的 `source` 字符串和一个 `target` 字符串，你应该在 source 字符串中找出 target 字符串出现的第一个位置(从`0`开始)。如果不存在，则返回 `-1`。

```
source = "abcdabcdefg"
target = "bcd"
output = 1
```

### 解决方案

以source中的每一个字符为一轮的基准，对**这个字符向后的一段字符**和**目标字符**进行匹配。要是都匹配上了，就返回当前这轮基准字符的index。

```java
public class Solution {
    /**
     * @param source: 
     * @param target: 
     * @return: return the index
     */
    public int strStr(String source, String target) {
        // Write your code here
        int indexSource;
        int isContains = -1;
        // 处理特殊情况
        if (source.length() == 0 & target.length() == 0) {
            return 0;
        } else if (source.length() != 0 & target.length() == 0) {
            return 0;
        }
        // 以原数组字母为基准进行遍历
        for (int i = 0; i < source.length(); i++) {
            indexSource = i; // 未来一轮匹配中原字符串的起始位置
            int indexTarget = 0; // 重置未来一轮匹配中目标字符串的起始位置
            int counter = 1; // 未来一轮匹配的计数器
            boolean match = false;
            // 当计数器小于等于目标字符串长度时
            while (counter <= target.length()) {
                // 如果本轮原字符串位置大于其长度，则直接返回-1
                if (indexSource > source.length() - 1) {
                    return -1;
                }
                // 所本轮二者匹配上了，就给一个true
                if (source.charAt(indexSource)==target.charAt(indexTarget)) {
                    match = true;
                } else {
                    match = false;
                }
                // 如果有一个没匹配上，就直接结束，否则更新第一次匹配上的位置，这里的i只受当前外层for-loop控制
                // 外层for-loop的i是匹配的起始位置，就相当于第一次匹配上的位置
                if (match == false) {
                    break;
                } else {
                    isContains = i;
                }
                // 更新搜索index，counter
                indexSource++;
                indexTarget++;
                counter++;
            }
            // 如果全部顺利匹配上，就停止当前循环
            if (isContains != -1 & match != false) {
                break;
            } else {
                isContains = -1;
            }
        }
        return isContains;
    }
}
```

### 解决方案（标准）<mark style="color:purple;">（需要复习）</mark>

```java
class Solution {
    public int strStr(String source, String target) {
        // 特殊情况
        if (source == null || target == null) {
            return -1;
        }
        
        for (int i = 0; i < source.length() - target.length() + 1; i++) {
            int j = 0;
            for (j = 0; j < target.length(); j++) {
                if (source.charAt(i + j) != target.charAt(j)) {
                    break;
                }
            }
            // finished loop, target found
            if (j == target.length()) {
                return i;
            }
        }
        return -1;
    }
}
```

## 1535 · 转换成小写字母<mark style="color:green;">（简单）</mark>

### 题目要求

实现函数 `ToLowerCase()`，该函数接收一个字符串参数 str，并将该字符串中的大写字母转换成小写字母，之后返回新的字符串。

```
输入: "LOVELY"
输出: "lovely"
```

### 解决方案

找到大写字母和其对应的小写字母的ASCII码差值，利用差值进行将“大写”运算到“小写”

```java
public class Solution {
    /**
     * @param str: the input string
     * @return: The lower case string
     */
    public String toLowerCase(String str) {
        // Write your code here
        // ASCII码先大写后小写
        int offset = 'a' - 'A'; // A-a和Z-z之间差的是一样的
        StringBuilder builder = new StringBuilder();
        // for循环遍历所有字母
        for (char letter : str.toCharArray()) {
            char lowerOne;
            // 如果有大写
            if (letter >= 'A' & letter <= 'Z') {
                // 就用ascii码运算得到小写字母，并保存到lowerOne
                lowerOne = (char)(letter + offset);
                builder.append(lowerOne);
            } else {
                builder.append(letter);
            }
        }
        return builder.toString();
    }
}
```

## 1343 · 两字符串和<mark style="color:green;">（简单）</mark>

### 题目要求

给定两个仅含数字的字符串，你需要返回一个由各个位之和拼接的字符串。

```
输入:
A = "99"
B = "111"
输出: "11010"
解释: 因为 9 + 1 = 10, 9 + 1 = 10, 0 + 1 = 1,连接之后的结果是 "11010"
```

### 解决方案

将A和B补齐成相同长度的两个字符串，然后再按位运算

```java
public class Solution {
    /**
     * @param A: a string
     * @param B: a string
     * @return: return the sum of two strings
     */
    public String SumofTwoStrings(String A, String B) {
        // write your code here
        // 处理特殊情况：AB均空，AB有一方不空
        if (A.equals("") & B.equals("")) {
            return "";
        } else if (A.equals("")) {
            return B;
        } else if (B.equals("")) {
            return A;
        }
        // 用stringbuilder保存结果
        StringBuilder builder = new StringBuilder();
        // 都转换为char类型数组
        char[] charA = A.toCharArray();
        char[] charB = B.toCharArray();
        // 将AB都转换为一样长度的数组，欠缺长度的那一方前面用0补齐（"123" -> "00123"）
        int lengthA = charA.length, lengthB = charB.length;
        if (lengthA > lengthB) {
            charB = fillToSameLength(charB, lengthA);
        } else if (lengthA < lengthB) {
            charA = fillToSameLength(charA, lengthB);
        }
        // 从后向前逐位进行加法，并将结果添加到builder的最前面
        for (int i = charA.length-1; i >= 0; i--) {
            builder.insert(0, String.valueOf(Character.getNumericValue(charA[i]) + Character.getNumericValue(charB[i])));
        }
        // 返回builder
        return builder.toString();
        
    }

    private static char[] fillToSameLength(char[] original, int wantedLength){
        // 新数组用于保存最终结果
        char[] newArray = new char[wantedLength];
        // 计算出需要补0的个数
        int zeroCount = wantedLength - original.length;
        // 在数组前面进行补0
        for (int i = 0; i < zeroCount; i++) {
            newArray[i] = '0';
        }
        // 将原数组内容复制到最后一位0的后面
        System.arraycopy(original, 0, newArray, zeroCount, original.length);
        return newArray;
    }
}
```

### 解决方案二

先处理AB不同长度的那一部分，再处理相同长度的

```java
public String SumofTwoStrings(String A, String B) {
        StringBuilder sb = new StringBuilder();
        
        // 先处理A和B不一般长的一段
        if (A.length() > B.length()) {
            sb.append(A.substring(0, A.length() - B.length()));
            A = A.substring(A.length() - B.length());
        } else {
            sb.append(B.substring(0, B.length() - A.length()));
            B = B.substring(B.length() - A.length());
        }
        
        // 再处理一般长的一段
        for (int i = 0; i < A.length(); i++) {
            char digitA = A.charAt(i);
            char digitB = (i < B.length()) ? B.charAt(i) : '0';
            sb.append(getSum(digitA, digitB));
        }
        return sb.toString();
    }
    
    private String getSum(char digitA, char digitB) {
        int sum = (digitA - '0') + (digitB - '0');
        return String.valueOf(sum);
    }
```

## 936 · 首字母大写<mark style="color:green;">（简单）</mark>

### 题目要求

输入一个英文句子，将每个单词的第一个字母改成大写字母。

1. 这个句子可能并不是一个符合语法规则的句子。
2. 句子长度小于等于`100`。
3. 除了句子的开头，其余字母均为小写

```
输入: s =  "i want to get an accepted"
输出: "I Want To Get An Accepted"

输入: s =  "i jidls    mdijf  i  lsidj  i p l   "
输出: "I Jidls    Mdijf  I  Lsidj  I P L   "
```

### 解决方案

除开特殊情况，按照“单词开头前必有空格”的规律找到每个单词的第一个字母，并利用ASCII码运算将小写转换到大写

```java
public class Solution {
    /**
     * @param s: a string
     * @return: a string after capitalizes the first letter
     */
    public String capitalizesFirst(String s) {
        // Write your code here
        // 判断：是遇到的第一个字母吗？
        boolean meetFirstLetter = false;
        // 特殊情况：为空或为一个空格，直接返回
        if (s.equals("") || s.equals(" ")) return s;
        // 转换为char数组
        char[] charArr = s.toCharArray();
        // 循环遍历数组里的每一个元素
        for (int i = 0; i < charArr.length; i++) {
            // 如果是“首个元素”或者“当前元素的前一个是空格”，那么就说明当前位置是新单词的首个元素
            if (i == 0 || charArr[i-1] == ' ') {
                // 如果这个元素是个字母，并且是小写，就设meetFirstLetter为true
                if ((charArr[i] >= 'a' & charArr[i] <= 'z')) {
                    meetFirstLetter = true;
                }
            } else {
                meetFirstLetter = false;
            }
            // 如果meetFirstLetter为true，就用ascii码运算将小写转到大写
            if (meetFirstLetter) {
                // 'a'比'A'要大，所以(a-A)就是小写到大写的差值，需要类型转换
                charArr[i] = (char)(charArr[i] - ('a' - 'A'));
            }
        }
        return String.valueOf(charArr);
    }
}
```

## 491 · 回文数<mark style="color:green;">（简单）</mark>

### 题目要求

判断一个正整数是不是回文数。

回文数的定义是，将这个数反转之后，得到的数仍然是同一个数。

```
输入：1232
输出：false
解释：
1232!=2321
```

### 解决方案

经典的双指针问题

```java
public class Solution {
    /**
     * @param num: a positive number
     * @return: true if it's a palindrome or false
     */
    public boolean isPalindrome(int num) {
        // write your code here
        // 特殊情况： 只有一位数字
        if (num >= 0 & num < 10) return true;
        // 将数字拆散放到char数组
        char[] charArr = String.valueOf(num).toCharArray();
        // 定义左右指针
        int left = 0, right = charArr.length - 1;
        // 默认是回文数
        // boolean match = true;
        // 开始遍历
        while (left <= right) {
            // 只要有一个匹配不上，直接结束运行并返回false；
            if (charArr[left] != charArr[right]) {
                return false;
            }
            left++;
            right--;
        }
        // 如果没有报错，顺利结束，就返回true
        return true;
    }
}
```

## 133 · 最长单词<mark style="color:green;">（简单）</mark>

### 题目要求

给一个词典，找出其中所有最长的单词。

```
样例 1:
	输入:   {
		"dog",
		"google",
		"facebook",
		"internationalization",
		"blabla"
		}
	输出: ["internationalization"]
	
样例 2:
	输入: {
		"like",
		"love",
		"hate",
		"yes"		
		}
	输出: ["like", "love", "hate"]
```

### 解决方案

第一次遍历找到**最长的长度**和**每个单词的长度**。第二次遍历将所有符合最长长度的单词全部弄出来。

```java
public class Solution {
    /*
     * @param dictionary: an array of strings
     * @return: an arraylist of strings
     */
    public List<String> longestWords(String[] dictionary) {
        // write your code here
        // 特殊情况：dictionary为空或者就一个单词，那么就直接返回
        if (dictionary.length == 0 || dictionary.length == 1) return Arrays.asList(dictionary);
        // 创建一个list用于保存结果
        List<String> result = new ArrayList<>();
        // 创建一个用于存储每个单词长度的数组
        int[] lengthRecord = new int[dictionary.length];
        // 最大长度
        int max = 0;
        // 遍历dictionary中的每个单词，记录每个单词的长度以及找出最大长度
        for (int i = 0; i < dictionary.length; i++) {
            lengthRecord[i] = dictionary[i].length();
            if (lengthRecord[i] > max) max = lengthRecord[i];
        }
        // 找出和最大长度一样的所有单词
        for (int i = 0; i < lengthRecord.length; i++) {
            if (lengthRecord[i] == max) {
                result.add(dictionary[i]);
            }
        }

        return result;
    }
}
```

## 422 · 最后一个单词的长度<mark style="color:green;">（简单）</mark>

### 题目要求

给定一个字符串， 包含大小写字母、空格 `' '`，请返回其最后一个单词的长度。

如果不存在最后一个单词，请返回 `0` 。

```
输入："Hello World"
输出：5
```

### 解决方案

首先排查特殊情况，随后按空格对句子进行分隔，将结果保存到数组。求出数组内最后一个元素的长度。

```java
public class Solution {
    /**
     * @param s: A string
     * @return: the length of last word
     */
    public int lengthOfLastWord(String s) {
        // write your code here
        // 特殊情况：字符串为null，为空或为一个空格
        if (s == null || s == "" || s == " ") {
            return 0;
        }
        // 应用正则表达式进行字符串分割，按“一个或多个空格”进行匹配
        String[] afterSplit = s.split("\\s+");
        // 返回afterSplit中最后一个元素的长度
        return afterSplit[afterSplit.length-1].length();
    }
}
```

## 353 · 最大字母<mark style="color:green;">（简单）</mark>

### 题目要求

给定字符串S，找到最大的字母字符，其大写和小写字母均出现在S中，则返回此字母的大写，若不存在则返回"NO"。

```
输入: S = "admeDCAB"
输出: "D"

输入: S = "adme"
输出: "NO"
```

### 解决方案

先判断有没有大写存在，有的话就排序。从最大的大写字母所在位置向前遍历，对每个字母进行小写字母存在性的判断。

```java
public class Solution {
    /**
     * @param s: a string
     * @return: a string
     */
    public String largestLetter(String s) {
        // write your code here
        // 如果没有大写，直接返回
        if (!containsUpper(s)) return "NO";
        // 将字符串转换成char数组
        char[] charArr = s.toCharArray();
        // 对char数组进行排序 ("admeDCAB" -> "ABCDadem")
        Arrays.sort(charArr);
        // 记录“最大的”大写字母的index
        int maxUpperCase = 0;
        for (int i = 0; i < charArr.length; i++) {
            if (charArr[i] > 'Z') {
                maxUpperCase = i;
                break;
            }
        }

        // 从最大的大写字母开始向前遍历，如果能找到某个大写字母所对应的小写字母，那么它就是“最大字母”
        for (int i = maxUpperCase; i >= 0; i--) {
            // char + 32的意思是将ascii码从大写字母转换到小写字母（32是‘a’到‘A’的差值）
            if (s.indexOf(String.valueOf((char)(charArr[i] + 32))) != -1) {
                return String.valueOf(charArr[i]);
            }
        }
        // 没有就返回no
        return "NO";
    }

    // 判断是否含有大写
    private static boolean containsUpper(String s){
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (!Character.isLowerCase(c)) return true;
        }
        return false;
    }
}
```

## 8 · 旋转字符串<mark style="color:green;">（简单）</mark>

### 题目要求

给定一个字符串`str`和一个偏移量，根据偏移量`原地旋转`字符串(从左向右旋转)。

```
str = "abcdefg"
offset = 3
output = "efgabcd"
```

### 解决方案

三步翻转法

1. 不变的部分进行翻转
2. 变的部分进行翻转
3. 整体进行翻转

```java
/public class Solution {
    /**
     * @param str: an array of char
     * @param offset: an integer
     * @return: nothing
     */
    public void rotateString(char[] str, int offset) {
        // write your code here
        // 边界情况
        if (str == null || str.length == 0)
            return;
        // 求出真正有效的offset 
        offset = offset % str.length;
        // Step 1：不变的部分进行翻转 (abcd - dcba)
        reverse(str, 0, str.length - offset - 1);
        // Step 2：偏移的部分进行翻转 (efg - gfe)
        reverse(str, str.length - offset, str.length - 1);
        // Step 3：整体翻转 (dcbagfe - efgabcd)
        reverse(str, 0, str.length - 1);
    }
    
    private void reverse(char[] str, int start, int end) {
        for (int i = start, j = end; i < j; i++, j--) {
            char temp = str[i];
            str[i] = str[j];
            str[j] = temp;
        }
    }
}
```

