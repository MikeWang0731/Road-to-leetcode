---
description: Basic Recursive
cover: >-
  https://images.unsplash.com/photo-1639625555610-63f16b664434?crop=entropy&cs=srgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHJhbmRvbXx8fHx8fHx8fDE2NDE4NzI2ODE&ixlib=rb-1.2.1&q=85
coverY: 366.5811417575369
---

# ð ç®åéå½

## 366 Â· ææ³¢çº³å¥æ°å<mark style="color:blue;">ï¼å¥é¨ï¼</mark>

<mark style="color:red;">è¿ä¸ªæ°åçç¬¬ä¸é¡¹æ¯0ï¼ç¬¬äºé¡¹æ¯1ï¼è¿ä¸ªæ°åä»ç¬¬ä¸é¡¹å¼å§ï¼æ¯ä¸é¡¹é½ç­äºåä¸¤é¡¹ä¹åã</mark>

### é¢ç®è¦æ±

æ¥æ¾ææ³¢çº³å¥æ°åä¸­ç¬¬ N ä¸ªæ°ã

ææ³¢çº³å¥æ°åçå10ä¸ªæ°å­æ¯ï¼

`0, 1, 1, 2, 3, 5, 8, 13, 21, 34 ...`

### è§£å³æ¹æ¡ä¸ï¼è®°å¿éå½ï¼

{% embed url="https://www.runoob.com/java/method-fibonacci.html" %}

```java
class Solution {
    /**
     * @param n: an integer
     * @return an integer f(n)
     */
    public int fibonacci(int n) {
        // è®°å¿ä¸æ¥ç¬¬ä¸ä¸ªæ°åç¬¬äºä¸ªæ°
        int a = 0;
        int b = 1;
        // éè¿forå¾ªç¯æ´æ°âåä¸¤ä¸ªæ°â
        // å ä¸ºç¬¬ä¸ä¸ªæ°æ¯åä¸¤ä¸ªæ°ä¹åï¼ç´è§ä»¥ä¸ºæ¯(i<=n-1)ï¼ä½æ¯æ¯ä»0æ°èµ·ï¼å³(i<=n-2 æ i<n-1)
        for (int i = 0; i < n - 1; i++) {
            int c = a + b;
            a = b;
            b = c;
        }
        return a;
    }
}
```

### è§£å³æ¹æ¡äºï¼æ åéå½ï¼

ä½è¿ç§æ¹æ³å¨æäºç½ç«ä¼æ¾ç¤ºâè¶æ¶âã

```java
public static int fibonacci(int number) {
        if ((number == 0) || (number == 1))
            return number;
        else
            return fibonacci(number - 1) + fibonacci(number - 2);
    }
```

## 68 Â· äºåæ çååºéå<mark style="color:green;">ï¼ç®åï¼</mark>

### é¢ç®è¦æ±

ç»åºä¸æ£µäºåæ ï¼è¿åå¶èç¹å¼çååºéåã

### è§£å³æ¹æ¡

å¸¸è§ååºéåï¼åå·¦åå³åèªå·±

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

## 67 Â· äºåæ çä¸­åºéå<mark style="color:green;">ï¼ç®åï¼</mark>

### é¢ç®è¦æ±

ç»åºä¸æ£µäºåæ ,è¿åå¶ä¸­åºéåã

### è§£å³æ¹æ¡

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

## 66 Â· äºåæ çååºéå<mark style="color:green;">ï¼ç®åï¼</mark>

### é¢ç®è¦æ±

ç»åºä¸æ£µäºåæ ï¼è¿åå¶èç¹å¼çååºéåã

### è§£å³æ¹æ¡

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



