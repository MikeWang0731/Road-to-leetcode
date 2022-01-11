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
}
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

## 807 · 回文数 II<mark style="color:green;">（简单）</mark>

### 题目要求

判断一个非负整数 `n` 的二进制表示是否为回文数。

```
输入: n = 3
输出: True
解释:
3 的二进制表示为：11。

输入: n = 6
输出: False
解释:
6 的二进制表示为：110。
```

### 解决方案&#x20;

```java
public class Solution {
    /**
     * @param n: non-negative integer n.
     * @return: return whether a binary representation of a non-negative integer n is a palindrome.
     */
    public boolean isPalindrome(int n) {
        // Write your code here
        // Step 1: 十进制转换为二进制char类型Array
        String decimal = Integer.toBinaryString(n);
        char[] decimalChar = decimal.toCharArray();
        // Step 2: 设置左起和右起两个指针，默认结果为false
        int left = 0, right = decimalChar.length - 1;
        boolean result = false;
        // Step 3: 开始循环判断，两个指针分别向中间靠拢
        while (left <= right) {
            // 如果有一个匹配不上就直接返回false，或者所有的都能匹配上才返回true
            if (decimalChar[left]==decimalChar[right]) {
                result = true;
            } else {
                return false;
            }
            left += 1;
            right -= 1;
        }

        return result;
    }
}
```

## 768 · 杨辉三角<mark style="color:green;">（简单）</mark><mark style="color:purple;">(需要复习)</mark>

### 题目要求

给一整数 `n`, 返回杨辉三角的前 `n 行`。

```
输入 : n = 4
输出 :
[
 [1]
 [1,1]
 [1,2,1]
 [1,3,3,1]
]
```

### 解决方案<mark style="color:green;">（标准解决）</mark>

```java
public class Solution {
    /**
     * @param n: a Integer
     * @return: the first n-line Yang Hui's triangle
     */
    public List<List<Integer>> calcYangHuisTriangle(int n) {
        List<List<Integer> > res = new ArrayList<>();
        int i, j;
        if (n == 0) {
            return res;
        }
        
        for (i = 0; i < n; ++i) {
            List<Integer> t = new ArrayList<Integer>();
            t.add(1);   
            for (j = 1; j < i; ++j) {
                t.add(res.get(i - 1).get(j - 1) + res.get(i - 1).get(j));    
            }
            
            if (i > 0) {
                t.add(1);
            }
            res.add(t);
        }
        return res;
    }
}
```

## 767 · 翻转数组<mark style="color:green;">（简单）</mark>

### 题目要求

原地翻转给出的数组 `nums`。<mark style="color:red;">不可以开辟额外的数组空间！</mark>

```
输入 : nums = [1,2,5]
输出 : [5,2,1]
```

### 解决方案

同样是双指针思想来解决问题

```java
public class Solution {
    /**
     * @param nums: a integer array
     * @return: nothing
     */
    public void reverseArray(int[] nums) {
        // write your code here
        // 如果是长度为0或1的数组，就没必要继续进行操作
        if (nums.length == 0 || nums.length == 1) {
            return;
        }
        // 设置两个指针
        int left = 0, right = nums.length - 1;
        // 对两个指针所在位置的值进行交换
        // left <= right: 这是因为要保证奇数个元素时依旧可以对所有元素进行操作
        while (left <= right) {
            int temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;
            // 更新下一轮left和right的位置
            left += 1;
            right -= 1;
        }
    }
}
```

## 539 · 移动零<mark style="color:green;">（简单）</mark>

### 题目要求

给一个数组 _nums_ 写一个函数将 `0` 移动到数组的最后面，非零元素保持原数组的顺序。必须在原数组上操作，最小化操作数。

```
输入: nums = [0, 1, 0, 3, 12],
输出: [1, 3, 12, 0, 0].
```

### 解决方案（我自己的）

类似于冒泡算法，将0“冒泡”到最后，<mark style="color:red;">但这个算法不是最优解！</mark>&#x20;

```java
public class Solution {
    /**
     * @param nums: an integer array
     * @return: nothing
     */
    public void moveZeroes(int[] nums) {
        // write your code here
        for (int i = 0; i < nums.length - 1; i++) {
            for (int j = i; j < nums.length - 1; j++) {
                if (nums[j] == 0) {
                    swap(nums, j, j + 1);
                }
            }
        }
    }

    private void swap(int[] arr, int indexA, int indexB) {
        int temp = arr[indexA];
        arr[indexA] = arr[indexB];
        arr[indexB] = temp;
    }
}
```

### 解决方案（<mark style="color:green;">排名第一</mark>）

```java
public class Solution {
    /**
     * @param nums an integer array
     * @return nothing, do this in-place
     */
    public void moveZeroes(int[] nums) {
        // Write your code here
        int left = 0, right = 0;
        while (right < nums.length) {
            if (nums[right] != 0) {
                int temp = nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
                left++;
            }
            right++;
        }
    }
}
```

## 479 · 数组第二大数<mark style="color:green;">（简单）</mark>

### 题目要求

在数组中找到第二大的数。

```
输入：[1,3,2,4]
输出：3
```

### 解决方案（<mark style="color:purple;">最简单但非最佳</mark>）

```java
public class Solution {
    /**
     * @param nums: An integer array
     * @return: The second max number in the array.
     */
    public int secondMax(int[] nums) {
        // write your code here
        Arrays.sort(nums);
        int targetIndex = nums.length - 2;
        return nums[targetIndex];
    }
}
```



## 235 · 分解质因数<mark style="color:green;">（简单）</mark><mark style="color:purple;">(需要复习)</mark>

### 题目要求

将一个整数分解为若干质因数之乘积。

```
输入：660
输出：[2, 2, 3, 5, 11]
```

### 解决方案

质因数：每个合数都可以写成几个质数（也可称为素数）相乘的形式 ，这几个质数就都叫做这个合数的质因数。

* 从小到大遍历\[2,upperLimit]，若num能够被i整除则循环除以i直到不能被整除，每次除以i都向答案值数组增加一个i，因为是从小到大遍历，则必定只有质数能被取为因数
* upperLimit一般设定为$$num^2$$，因为一个数大于其根号的质因数最多只有一个，那么遍历其根号内的数可以将时间复杂度减小至根号n，若遍历完prime后该数不为1，则其值为最后一个质因数

```java
public class Solution {
    /**
     * @param num an integer
     * @return an integer array
     */
    public List<Integer> primeFactorization(int num) {
        List<Integer> factors = new ArrayList<Integer>();
        for (int i = 2; i * i <= num; i++) {
            while (num % i == 0) {
                num = num / i;
                factors.add(i);
            }
        }
        //若最后剩余数不为1，则为最后一个质因数
        if (num != 1) {
            factors.add(num);
        }   
        return factors;
    }
}
```

## 407 · 加一<mark style="color:green;">（简单）</mark><mark style="color:purple;">（有难度）</mark>

### 题目要求

给定一个非负数，表示一个数字数组，在该数的基础上+1，返回一个新的数组。

该数字按照数位高低进行排列，最高位的数在列表的最前面。

```
输入：[1,2,3]
输出：[1,2,4]

输入：[9,9,9]
输出：[1,0,0,0]
```

### 解决方案

```java
public class Solution {
    /**
     * @param digits: a number represented as an array of digits
     * @return: the result
     */
    public int[] plusOne(int[] digits) {
        
        // 加一的“1”
        int extra = 1;
        // 对于数组从后向前取
        for (int i = digits.length - 1; i >= 0; i--) {
            // 每一位都要加一
            int sum = digits[i] + extra;
            // 这一位的值由(sum/10)的余数计算而来
            // if 1~9 -> 1~9 ; if 10 -> 0
            digits[i] = sum % 10;
            // 这里的sum/10决定了只有发生“进位”时(sum=10)才能进入下一次循环判断前一位数是否需要更新
            extra = sum / 10;
            // 如果不进位(extra为0，例如8/10=0)，就直接跳出循环
            if (extra == 0) {
                break;
            }
        }
        // 接上面：如果没有进位发生，就直接结束程序
        if (extra == 0) {
            return digits;
        }
        // 如果原数组全都进位了(999->1000)，新数组的长度则加一
        // 若全都进位，则上面的for-loop产生三个0，并且extra为1，不满足extra为0的情况，所以length + 1
        int[] result = new int[digits.length + 1];
        // 新数组的第一位填充1
        result[0] = 1;
        return result;
    }
}
```

## 220 · 冰雹猜想<mark style="color:green;">（简单）</mark>

### 题目要求

数学家们曾提出一个著名的猜想——冰雹猜想。 对于任意一个自然数N，如果N是偶数，就把它变成N / 2； 如果N是奇数，就把它变成 3 \* N+1。 按照这个法则运算下去，最终必然得1。 试问，该数通过几轮变换，会变成1呢？

```
输入： 
4
输出： 
2
解释： 
第一轮：4/2=2
第二轮：2/2=1
答案为2
```

### 解决方案

这个题不难，判断一下奇数偶数，分别进行计算就可以了。当num=1的时候循环停止。计数器需要从0开始，因为需要进行完首轮奇偶判断才能定义为“一次”。

```java
public class Solution {
    /**
     * @param num: an integer
     * @return: return an integer
     */
    public int getAnswer(int num) {
        int count = 0;

        while (num != 1) {
            if (num % 2 == 0) {
                num = num / 2;
            } else {
                num = 3 * num + 1;
            }
            
            count += 1;
        }

        return count;
    }
}
```

## 53 · 翻转字符串<mark style="color:green;">（简单）</mark>

### 题目要求

给定一个字符串，逐个翻转字符串中的每个单词。

```
s = "the sky is blue"
"blue is sky the"
```

### 解决方案

```java
public class Solution {
    /*
     * @param s: A string
     * @return: A string
     */
    public String reverseWords(String s) {
        // write your code here
        if (s == "") {
            return s;
        }
        // 按照空格分隔，允许多次匹配空格(错误示范：.split(" "))
        String[] afterSplit = s.trim().split("\\s+");
        // 删除每个单词后的标点（如果有）
        for (String string : afterSplit) {
            string = string.replaceAll("([a-z]+)[?:!.,;]*", "$1");
        }
        // 双指针做前后交换，实现翻转
        int left = 0, right = afterSplit.length - 1;

        while (left <= right) {
            String temp = afterSplit[left];
            afterSplit[left] = afterSplit[right];
            afterSplit[right] = temp;

            left++;
            right--;
        }
        // 将反转后的array中的每个元素添加到builder
        StringBuilder builder = new StringBuilder();
        for (String str : afterSplit) {
            builder.append(str).append(" ");
        }
        // 删除最后一个空格并return
        return builder.toString().trim();
    }
}
```

## 50 · 数组剔除元素后的乘积题目要求<mark style="color:green;">（简单）</mark>

给定一个整数数组`A`。\
定义$$B[i] = A[0] * ... * A[i-1] * A[i+1] * ... * A[n-1]B[i]=A[0]∗...∗A[i−1]∗A[i+1]∗...∗A[n−1]$$ 计算`B`的时候请不要使用除法。请输出`B`。

```
A = [1,2,3]
Output = [6,3,2]
B[0] = A[1] * A[2] = 6; B[1] = A[0] * A[2] = 3; B[2] = A[0] * A[1] = 2
```

### 解决方案

暴力枚举，计算所有情况

```java
public class Solution {
    /*
     * @param nums: Given an integers array A
     * @return: A long long array B and B[i]= A[0] * ... * A[i-1] * A[i+1] * ... * A[n-1]
     */
    public List<Long> productExcludeItself(List<Integer> nums) {
        // 建立一个list保存答案
        List<Long> resultB = new ArrayList<>();

        // 一些特殊情况的判断
        // Case 1：无元素
        if (nums.size() == 0) {
            resultB.add(new Integer(1).longValue());
            return resultB;
        } 
        // case 2：只有一个元素（元素为0或其他）
        if (nums.size() == 1 & nums.get(0) != 0) {
            resultB.add(new Integer(nums.get(0)).longValue());
            return resultB;
        } else if (nums.size() == 1 & nums.get(0) == 0) {
            resultB.add(new Integer(1).longValue());  // 其实这里并不是特别理解为什么有且只有一个元素0要返回1
            return resultB;
        }
        // 暴力枚举：遍历数组里的所有数字，找到对于每个数字而言的所有情况
        for (int currentIndex = 0; currentIndex < nums.size(); currentIndex++) {
            long result = 1;  // 保存对于这个数字而言的答案
            // 求出除了当前数字所有数字的乘积
            for (int calIndex = 0; calIndex < nums.size(); calIndex++) {
                if (calIndex == currentIndex) continue;
                result = result * nums.get(calIndex);
            }
            // 加入到答案list
            resultB.add(result);
        }
        return resultB;
    }
}
```

## 46 · 主元素<mark style="color:green;">（简单）</mark>

### 题目要求

给定一个整型数组，找出主元素，它在数组中的出现次数大于数组元素个数的二分之一。

```
数组 = [1, 1, 1, 1, 2, 2, 2]
output = 1
```

### 解决方案一 （我自己 - 使用HashMap）

```java
public class Solution {
    /*
     * @param nums: a list of integers
     * @return: find a  majority number
     */
    public int majorityNumber(List<Integer> nums) {
        // write your code here
        // <key,value>：key是唯一的，代表数字，value代表次数
        HashMap<Integer,Integer> map = new HashMap<>();
        for (int number : nums) {
            if (map.containsKey(number)) {
                // 如果出现过就更新value
                map.put(number, map.get(number) + 1);
            } else {
               map.put(number, 1); 
            }
        }
        // 找到最大的value
        int maxShowUp = Collections.max(map.values());
        // 保存最大value所在的index
        int maxIndex = 0;
        // 遍历values，找到index
        for (int values : map.values()) {
            if (values == maxShowUp) break;
            maxIndex += 1;
        }
        // 遍历keys，找到最大value对应的key
        int maxKey = 0;
        int count = 0;
        for (int key: map.keySet()) {
            if (count == maxIndex) {
                maxKey = key;
            }
            count++;
        }

        return maxKey;
    }
}
```

### 解决方案二 （使用排序 - 最简单）

可以排序的情况下，代码只需要两行&#x20;

因为占1/2以上的数一定是主元素，数组中间那个数也一定是它

时间复杂度 $$O(nlogn)$$空间复杂度$$O(1)$$

```java
public class Solution {
    /*
     * @param nums: a list of integers
     * @return: find a  majority number
     */
    public int majorityNumber(List<Integer> nums) {
        Collections.sort(nums);
        return nums.get(nums.size()/2);
    }
}
```

### 解决方案三 （标准方案）

这相当于遍历数组中的所有元素，只要元素出现的次数够多，它的count在经历过众多加减之后依旧大于0

```java
public class Solution {

    public int majorityNumber(List<Integer> nums) {
        
        int currentMajor = 0;
        int count = 0;
        
        for(Integer num : nums) {
            if(count == 0) {
                currentMajor = num;
            }
            
            if(num == currentMajor) {
                count++;
            } else {
                count--;
            }
        }
        
        return currentMajor;
    }
}
```

## 9 · Fizz Buzz 问题<mark style="color:green;">（简单）</mark>

### 题目要求

给定整数 _n_ ，按照如下规则打印从 _1_ 到 _n_ 的每个数：

* 如果这个数被3整除，打印`fizz`。
* 如果这个数被5整除，打印`buzz`。
* 如果这个数能同时被`3`和`5`整除，打印`fizz buzz`。
* 如果这个数既不能被 `3` 整除也不能被 `5` 整除，打印数字`本身`。

```
input = 15
[
  "1", "2", "fizz",
  "4", "buzz", "fizz",
  "7", "8", "fizz",
  "buzz", "11", "fizz",
  "13", "14", "fizz buzz"
]
```

### 解决方案

注意条件的判断顺序，例如：15一旦被判断为可以被3或被5整除，那么就不会被判断为可以同时被整除！

条件要由小到大写！

```java
public class Solution {
    /**
     * @param n: An integer
     * @return: A list of strings.
     */
    public List<String> fizzBuzz(int n) {
        // write your code here
        List<String> result = new ArrayList<>();
        for (int element = 1; element <= n; element++) {
            if (element % 3 == 0 & element % 5 == 0) {
                result.add("fizz buzz");
            } else if (element % 3 == 0 || element % 5 == 0) {
                String input = element % 3 == 0 ? "fizz":"buzz";
                result.add(input);
            } else {
                result.add(String.valueOf(element));
            }
        }
        return result;
    }
}
```
