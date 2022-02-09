---
description: Array and Linked List
cover: >-
  https://images.unsplash.com/photo-1641921402984-80bb92e69e6e?crop=entropy&cs=srgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHJhbmRvbXx8fHx8fHx8fDE2NDQzNzg1NzU&ixlib=rb-1.2.1&q=85
coverY: 0
---

# 💡 数组/链表

## Intro

数组链表的主要算法技巧是<mark style="color:orange;">双指针</mark>，双指针⼜分为<mark style="color:orange;">中间向两端扩散的双指针</mark>、<mark style="color:orange;">两端向中间收缩的双指针</mark>、<mark style="color:orange;">快慢指针</mark>。此外，数组还有<mark style="color:orange;">前缀和和差分数组</mark>也属于必知必会的算法技巧。

## 303. 区域和检索 - 数组不可变<mark style="color:green;">（Easy）</mark>

给定一个整数数组  `nums`，处理以下类型的多个查询:

计算索引 `left` 和 `right` （包含 `left` 和 `right`）之间的 `nums` 元素的 **和** ，其中 `left <= right`

```
输入：
["NumArray", "sumRange", "sumRange", "sumRange"]
[[[-2, 0, 3, -5, 2, -1]], [0, 2], [2, 5], [0, 5]]
输出：
[null, 1, -1, -3]
解释：
[0,2] -> [-2,0,3] -> (-2)+0+3 = 1
[2,5] -> [3,-5,2,-1] -> 3+(-5)+2+(-1) = -1
```

### 解决方案（我自己）

使用for循环对数组元素进行遍历，因为已经给定了左右边界，所以直接从左边界开始取值，取到右边界结束就可以

```java
class NumArray {

    int[] nums;

    public NumArray(int[] nums) {
        this.nums = nums;
    }

    public int sumRange(int left, int right) {
        int sum = 0;
        // 从left开始取，取到right结束
        for (int i = left; i <= right; i++) {
            sum = sum + nums[i];
        }
        return sum;
    }
}
```

**但是**，这样的效率是很低的，因为测试案例中要运行很多次`sumRange()`方法，这就使得for循环会一次又一次的运行，速度很慢。因此，我们要避免在sumRange中使用for循环，怎么办？

{% hint style="info" %}
这里可以使用**“前缀和”**，即**prefix sum**技巧。前缀和是说新建一个数组，新数组的每个位置记录原数组的这个位置之前的和。

Original: \[3, 5, 2, -2, 4, 1]

preSum: \[0, 3, 8, 10, 8 ,12, 13]

\----------------

preSum\[0] = inital zero

preSum\[1] = 3 + 0 = 3

preSum\[2] = 5 + 3 + 0 = 8
{% endhint %}

有了前缀和这个技巧，我们就可以用`preSum[right+1] - preSum[left]`来得到某个区间的和。例如上述数组，我们求\[2, 4]这个区间，就可以用`preSum[5] - preSum[3]`来得到结果，是4。这是因为，**\[2, 4]区间的和就是\[0, 4]区间的和减去\[0, 2]区间的和**，刚好和前缀和的性质相符。

<mark style="color:purple;">二维数组也可以用这个性质，关键点是建立以原点为核心的数组来保存结果。</mark>

### 解决方案（前缀和）

```java
class NumArray {

    int[] preSum;

    public NumArray(int[] nums) {
        preSum = new int[nums.length + 1];
        // 这里从1开始是因为第一位要保持为0
        for (int i = 1; i < preSum.length; i++) {
            // preSum[i]是nums[0..i-1]的和
            // nums[0..i-1] = preSum[i-1] + nums[i-1]
            // preSum[i-1]就是nums[0..i-2]的和
            preSum[i] = preSum[i - 1] + nums[i - 1];
        }
    }

    public int sumRange(int left, int right) {
        return preSum[right + 1] - preSum[left];
    }
}
```

## 560. 和为 K 的子数组<mark style="color:yellow;">（Medium）</mark>

给你一个整数数组 `nums` 和一个整数 `k` ，请你统计并返回该数组中和为 `k` **** 的连续子数组的个数。

```
输入：nums = [1,1,1], k = 2
输出：2
[1*,1*,1] -> 第一组
[1,1*,1*] -> 第二组
```

### 解决方案（前缀和）

{% hint style="info" %}
前缀和的核心是
{% endhint %}

```java
class Solution {

    public int subarraySum(int[] nums, int k) {
        // key: <Sum, 出现次数>
        HashMap<Integer, Integer> preSum = new HashMap<>();
        // 计数：子数组的个数
        int resultCount = 0;
        // 原数组用于记录前缀和的变量(nums[0..i])
        int sum_i = 0;
        // base zero init
        preSum.put(0, 1);
        // 遍历nums中的全部元素
        for (int i = 0; i < nums.length; i++) {
            // 当前一轮的前缀和
            sum_i = sum_i + nums[i];
            // 这是我们想找的前缀和的变体sum_j
            // if (sum_i - sum_j == k) count++; 多项式移项
            int sum_j = sum_i - k;
            // 如果map里出现过我们想要的结果，我们就更新结果
            if (preSum.containsKey(sum_j)) {
                resultCount = resultCount + preSum.get(sum_j);
            }
            // 每轮结束时，将当前的前缀和加入到hashmap并记录次数+1
            // getOrDefault()，返回某个特定key的value，若map不到这个key，则用default值替代
            preSum.put(sum_i, preSum.getOrDefault(sum_i, 0) + 1);
        }

        return resultCount;
    }
}
```
