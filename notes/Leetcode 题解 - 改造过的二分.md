<!-- GFM-TOC -->
* [1. Find Smallest Letter Greater Than Target](#1-寻找比目标字母大的最小字母)
* [2. Ceiling of a Number (medium)](#2-两数平方和)
* [3. Next Letter (medium)](#3-反转字符串中的元音字符)
* [4. Number Range (medium)](#4-回文字符串)
* [5. Search in a Sorted Infinite Array (medium)](#5-归并两个有序数组)
* [6. Minimum Difference Element (medium)](#6-判断链表是否存在环)
* [7. Bitonic Array Maximum (easy)](#7-最长子序列)
454. 4Sum II
<!-- GFM-TOC -->


https://zhuanlan.zhihu.com/p/90664857

# 1. 寻找比目标字母大的最小字母

744\. Find Smallest Letter Greater Than Target (Easy)

[Leetcode](https://leetcode.com/problems/find-smallest-letter-greater-than-target/) / [力扣](https://leetcode-cn.com/problems/find-smallest-letter-greater-than-target/)

https://github.com/grandyang/leetcode/issues/102
```java
public int[] twoSum(int[] numbers, int target) {
    if (numbers == null) return null;
    int i = 0, j = numbers.length - 1;
    while (i < j) {
        int sum = numbers[i] + numbers[j];
        if (sum == target) {
            return new int[]{i + 1, j + 1};
        } else if (sum < target) {
            i++;
        } else {
            j--;
        }
    }
    return null;
}
```

# 2. 二叉树的层次遍历2

107\. Binary Tree Level Order Traversal II (Easy)

[Leetcode](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/) / [力扣](https://leetcode-cn.com/problems/binary-tree-level-order-traversal-ii/)

https://github.com/grandyang/leetcode/issues/107
```java
 public boolean judgeSquareSum(int target) {
     if (target < 0) return false;
     int i = 0, j = (int) Math.sqrt(target);
     while (i <= j) {
         int powSum = i * i + j * j;
         if (powSum == target) {
             return true;
         } else if (powSum > target) {
             j--;
         } else {
             i++;
         }
     }
     return false;
 }
```

# 3. 二叉树的锯齿形层次遍历

103\. Binary Tree Zigzag Level Order Traversal (Medium)

[Leetcode](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/) / [力扣](https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/)

https://github.com/grandyang/leetcode/issues/103
```java
class Solution {
    public int findDuplicate(int[] nums) {
        int slow = nums[0], fast = nums[nums[0]];
        while (slow != fast) {
            slow = nums[slow];
            fast = nums[nums[fast]];
        }
        fast = 0;
        while (slow != fast) {
            slow = nums[slow];
            fast = nums[fast];
        }
        return slow;
    }
}
```

# 4. N叉树的层序遍历

429\. N-ary Tree Level Order Traversal (Medium)

[Leetcode](https://leetcode.com/problems/n-ary-tree-level-order-traversal/) / [力扣](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)

https://github.com/grandyang/leetcode/issues/429
```java
 public boolean judgeSquareSum(int target) {
     if (target < 0) return false;
     int i = 0, j = (int) Math.sqrt(target);
     while (i <= j) {
         int powSum = i * i + j * j;
         if (powSum == target) {
             return true;
         } else if (powSum > target) {
             j--;
         } else {
             i++;
         }
     }
     return false;
 }
```

# 5. 二叉树的最小深度

111\. Minimum Depth of Binary Tree (Easy)

[Leetcode](https://leetcode.com/problems/minimum-depth-of-binary-tree/) / [力扣](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)

https://github.com/grandyang/leetcode/issues/111
```java
 public boolean judgeSquareSum(int target) {
     if (target < 0) return false;
     int i = 0, j = (int) Math.sqrt(target);
     while (i <= j) {
         int powSum = i * i + j * j;
         if (powSum == target) {
             return true;
         } else if (powSum > target) {
             j--;
         } else {
             i++;
         }
     }
     return false;
 }
```

# 6. 二叉树的层平均值

637\. Average of Levels in Binary Tree (Easy)

[Leetcode](https://leetcode.com/problems/average-of-levels-in-binary-tree/) / [力扣](https://leetcode-cn.com/problems/average-of-levels-in-binary-tree/)

https://github.com/grandyang/leetcode/issues/637
```java
 public boolean judgeSquareSum(int target) {
     if (target < 0) return false;
     int i = 0, j = (int) Math.sqrt(target);
     while (i <= j) {
         int powSum = i * i + j * j;
         if (powSum == target) {
             return true;
         } else if (powSum > target) {
             j--;
         } else {
             i++;
         }
     }
     return false;
 }
```
