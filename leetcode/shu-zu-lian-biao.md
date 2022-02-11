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

输入：nums = [1,2,3], k = 3
输出：2
[1, 2] -> 3
[3] -> 3
```

### 解决方案（前缀和）

{% hint style="info" %}
前缀和的核心是:`preSum[n] - preSum[n-1]，前缀和定义是：preSum[i]是指原数组[0..i-1]的所有元素的累加和`
{% endhint %}

以往我们会使用双指针的方法对所有可能的区间进行检索，若满足`preSum[i]-preSum[j] = k`则说明有连续的子数组的和为整数`k`，我们就将结果计数器加一。但是这需要两重循环，影响效率。**所以我们提出以下优化思路：**<mark style="color:green;">将上述公式移项得到</mark>`preSum[j] = preSum[i]-k`，这样就变成了“如果`preSum[j]`<mark style="color:red;">是0或者k本身</mark>，那么就说明我们找到了连续数组” 。<mark style="color:red;">并且我们将所有的前缀和都添加到HashMap中，key为前缀和本身，value是它出现的次数</mark>。这样我们就只需要一个for循环。

为什么可以这样说？假设`k=3`，某一轮`preSum[i] = 3`，那么此时preSum\[j]就是`3-3=0`，这就说明，前缀和累加到`nums[i-1]`这一位时，连续数组和刚好满足要求，符合题目条件。此时`count++`。这是Case 1.

当然，还有第二种情况，即Case2，如果某轮`preSum[i]-k`的差是`k`本身，则说明`preSum[i]`和`preSum[i-1]`之间刚好差了一个`k`。即这一轮`preSum[i]`中新加入元素`nums[i-1]`的值刚好和k一样，`nums[i-1]`它自己就独立满足条件。此时`count++`。

```
nums: [1, 2, 3], k = 3
preSum: [0, 1, 3, 6]
--------------
Case 1: preSum[i] - k = 0
preSum[2] = 3, k = 3, sum_j = 0
preSum[2] = nums[0] + nums[1] = 1 + 2 = 3 [Satisfy requirement]
--------------
Case 2: preSum[i] - k = k
preSum[3] = 6, k = 3, sum_j = 6 - 3 = 3
preSum[3] = nums[0] + nums[1] + nums[2] = preSum[2] + nums[2]
That is, An independent nums[2] also satisfy the requirement
```

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
            // 这是我们用来做“减法”的前缀和preSum[j]的变体
            // if (sum_i - sum_j == k) count++; 多项式移项
            int sum_j = sum_i - k;
            // 如果map的key里出现过和sumj一样的数值，我们就更新结果
            // "sumj一样的数值"就是被记录过的符合条件的前缀和(sum_i)
            if (preSum.containsKey(sum_j)) {
                resultCount = resultCount + preSum.get(sum_j);
            }
            // 每轮结束时，将当前这一轮的前缀和加入到hashmap并记录次数+1
            // getOrDefault()，返回某个特定key的value，若map不到这个key，则用default值替代
            preSum.put(sum_i, preSum.getOrDefault(sum_i, 0) + 1);
        } 

        return resultCount;
    }
}
```

## 1109. 航班预订统计<mark style="color:yellow;">（Medium）</mark>

这里有 `n` 个航班，它们分别从 `1` 到 `n` 进行编号。

有一份航班预订表 `bookings` ，表中第 `i` 条预订记录 `bookings[i] = [first, last, seats]` 意味着在从 `first` 到 `last` （**包含** `first` 和 `last` ）的 **每个航班** 上预订了 `seats` 个座位。

请你返回一个长度为 `n` 的数组 `answer`，里面的元素是每个航班预定的座位总数。

```
输入：bookings = [[1,2,10],[2,3,20],[2,5,25]], n = 5
输出：[10,55,45,25,25]
解释：
航班编号        1   2   3   4   5
预订记录 1 ：   10  10
预订记录 2 ：       20  20
预订记录 3 ：       25  25  25  25
总座位数：      10  55  45  25  25
因此，answer = [10,55,45,25,25]
```

### 解决方案（差分数组）

{% hint style="warning" %}
**前缀和**主要适⽤的场景是**原始数组不会被修改**的情况下，频繁查询某个区间的累加和。**差分数组**的主要适⽤场景是**频繁对原始数组的某个区间的元素进行增减**。
{% endhint %}

{% hint style="info" %}
差分数组是指新建一个数组`diff[]`用于<mark style="color:green;">记录原数组</mark><mark style="color:green;">`nums[]`</mark><mark style="color:green;">的每个元素之间的差值</mark>。例如`nums = [8, 5, 9, 6 ,1]`，那么`diff = [8, -3, 4, -3, -5]`。通过观察`diff[]`我们发现`diff`和`nums`的首元素都是相同的，这是因为首元素没有前序元素，没有办法记录差值。但是，`diff`中从第二个元素开始，记录的就是<mark style="color:green;">`nums`</mark><mark style="color:green;">第二个元素减去第一个元素的差值</mark>，即`diff[i] = nums[i] - nums[i-1]`。

\---------------------

`diff[1] = -3 = nums[1] - nums[0] = 5 - 8 = -3`

\---------------------

同理，我们也可以通过`diff`数组反推出原数组或更新差值后的数组，我们将结果保存至新数组`result[]`中，其中`result`的首元素和`diff`的首元素保持一致。<mark style="color:green;">`result`</mark><mark style="color:green;">数组从第二个元素开始就是</mark><mark style="color:green;">`result`</mark><mark style="color:green;">的前一个元素加上</mark><mark style="color:green;">`diff`</mark><mark style="color:green;">中的差值</mark>，即不断用之前的累加和加上新元素和上一个元素的差值来求出新的元素的值。即`result[i] = result[i-1] + diff[i]`。

\---------------------

`result = [8, 0, 0, 0, 0]`

`result[1] = result[0] + diff[1] = 8 + (-3) = 5`

So, new `result = [8, 5, 0, 0, 0]`

\---------------------

在差分数组`diff`处理区间元素增减时，我们并不需要`for`循环对元素差值逐个操作，这是因为如果某个差值`diff[i]`变大(e.g., 1->3)，在反推结果数组时，会<mark style="color:green;">导致这个</mark><mark style="color:green;">`diff[i]`</mark><mark style="color:green;">所对应的结果</mark><mark style="color:green;">`result[i]`</mark><mark style="color:green;">及它之后的所有数字都会增大，</mark><mark style="color:green;">`即nums[i..]都会增加val。`</mark>所以我们要<mark style="color:green;">在区间结束的后一位差值</mark><mark style="color:green;">`diff[i+1]`</mark><mark style="color:green;">上减去这个差值的变化</mark><mark style="color:green;">`val，`</mark><mark style="color:green;">这样才能保证</mark><mark style="color:green;">`diff[i+1]之后的数字不会变化`</mark>`。`即 `diff[i] = diff[i] + val; diff[j+1] = diff[j+1] - val;`

\---------------------

`diff = [8, -3, 4, -3, -5] -> nums从第2到4增加2 -> [8, -1, 4, -3, -7]`

`result = [8, 7, 11, 8, 1] / nums = [8, 5, 9, 6, 1]`
{% endhint %}

```java
class Solution {
    // 差分数组内部类
    class Difference {
        int[] diffArray;

        // 构建差分数组
        public Difference(int[] arr) throws IllegalArgumentException {
            if (arr.length <= 0) {
                throw new IllegalArgumentException("Length <= 0!");
            }
            diffArray = new int[arr.length];
            diffArray[0] = arr[0];
            for (int i = 1; i < arr.length; i++) {
                diffArray[i] = arr[i] - arr[i - 1];
            }
        }

        // 处理数组区间值增减(这里的index从0开始，val可以为负)
        public void increment(int index_i, int index_j, int val) {
            diffArray[index_i] += val;
            if (index_j + 1 < diffArray.length) {
                diffArray[index_j + 1] -= val;
            }
        }

        // 返回结果数组
        public int[] result() {
            int[] result = new int[diffArray.length];
            result[0] = diffArray[0];
            for (int i = 1; i < diffArray.length; i++) {
                result[i] = result[i - 1] + diffArray[i];
            }
            return result;
        }
    }

    public int[] corpFlightBookings(int[][] bookings, int n) {
        // 初始化arr = [0,0,0,0,0]
        // 五个0分别代表航班1-5的初始售出座位数
        int[] arr = new int[n];
        Difference difference = new Difference(arr);
        // 拿到bookings中每个子数组，
        for (int[] booking : bookings) {
            // 这里减一是因为航班序号从1开始，但是数组下标从0开始
            int index_i = booking[0] - 1;
            int index_j = booking[1] - 1;
            int val = booking[2];
            difference.increment(index_i, index_j, val);
        }

        return difference.result();
    }
}
```

## 1094. 拼车<mark style="color:yellow;">（Medium）</mark>

假设你是一位顺风车司机，车上最初有 `capacity` 个空座位可以用来载客。由于道路的限制，车 **只能** 向一个方向行驶（也就是说，**不允许掉头或改变方向**，你可以将其想象为一个向量）。

这儿有一份乘客行程计划表 `trips[][]`，其中 `trips[i] = [num_passengers, start_location, end_location]` 包含了第 `i` 组乘客的行程信息：

* 必须接送的乘客数量；
* 乘客的上车地点；
* 以及乘客的下车地点。

这些给出的地点位置是从你的 **初始** 出发位置向前行驶到这些地点所需的距离（它们一定在你的行驶方向上）。

请你根据给出的行程计划表和车子的座位数，来判断你的车是否可以顺利完成接送所有乘客的任务（当且仅当你可以在所有给定的行程中接送所有乘客时，返回 `true`，否则请返回 `false`）。

```
输入：trips = [[2,1,5],[3,3,7]], capacity = 4
输出：false

因为车上一共4个座位，从第1站上来2人到第5站下车，所以在1-4站之间车上一共有2个空座。然而，
第3站上来3个人，坐不下，超载，故false
```

{% hint style="info" %}
这道题的核心是判断到达每一站时车上的乘客会不会超载，计算每一站上车下车的人的数量，即对一个区间内的数组进行加减法，我们可以使用**差分数组**技巧。
{% endhint %}

### 解决方案（差分数组）

```java
class Solution {
    class Difference {
        int[] diffArray;

        public Difference(int[] arr) throws IllegalArgumentException {
            if (arr.length <= 0) {
                throw new IllegalArgumentException("Length <= 0");
            }
            diffArray = new int[arr.length];
            diffArray[0] = arr[0];
            for (int i = 1; i < arr.length; i++) {
                diffArray[i] = arr[i] - arr[i - 1];
            }
        }

        public void increament(int index_i, int index_j, int val) {
            diffArray[index_i] += val;
            if (index_j + 1 < diffArray.length) {
                diffArray[index_j + 1] -= val;
            }
        }

        public int[] result() {
            int[] result = new int[diffArray.length];
            result[0] = diffArray[0];
            for (int i = 1; i < diffArray.length; i++) {
                result[i] = result[i - 1] + diffArray[i];
            }
            return result;
        }
    }

    public boolean carPooling(int[][] trips, int capacity) {
        int[] arr = new int[1000];
        Difference difference = new Difference(arr);
        for (int[] singleTrip : trips) {
            // 为什么i不需要-1而j需要
            // 这是因为我们记录的是“乘客在车上的区间”
            // 从i站上车，此时乘客于i站存在于车上
            int index_i = singleTrip[1];
            // 于j站下车，到达j站时已经不在车上
            // 所以在车上的区间为[i..j-1]
            int index_j = singleTrip[2] - 1;
            int val = singleTrip[0];
            difference.increament(index_i, index_j, val);
        }

        // 将所有情况计算完查看最后的结果
        // arr记录着停靠每一站时车上的旅客数量
        arr = difference.result();

        for (int i = 0; i < arr.length; i++) {
            // 如果最终结果为超载，则不能顺利接送所有乘客
            // arr[i] = 在第i站时，车上有多少人
            if (arr[i] > capacity) {
                return false;
            }
        }
        return true;
    }
}
```

{% hint style="danger" %}
第36行`for`循环：为什么`i`不需要`-1`而`j`需要？这是因为我们记录的是“乘客在车上的区间”。某乘客从`i`站上车，此时乘客于`i`站开始存在于车上；后来该乘客于`j`站下车，到达`j`站时已经不在车上。所以在车上的区间为`[i..j-1]`。
{% endhint %}
