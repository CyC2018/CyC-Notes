<!-- GFM-TOC -->
* [1. Path Sum](#1-路径总和)
* [2. Path Sum II](#2-路径总和2)
* [3. Path Sum III](#3-路径总和3)
* [4. Sum Root to Leaf Numbers](#4-求根到叶子节点数字之和)
* [5. Delete Leaves With a Given Value](#5-删除给定值的叶子节点)
* [6. Binary Tree Maximum Path Sum](#6-二叉树中的最大路径和)
* [7. Stamping The Sequence](#7-戳印序列)
<!-- GFM-TOC -->


https://zhuanlan.zhihu.com/p/90664857

# 1. 路径总和

112\. Path Sum (Easy)

[Leetcode](https://leetcode.com/problems/path-sum/) / [力扣](https://leetcode-cn.com/problems/path-sum/)

https://github.com/grandyang/leetcode/issues/112
```java
class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) {
            return false;
        }
        sum -= root.val;
        if (root.left == null && root.right == null && sum == 0) return true;
        return hasPathSum(root.left, sum) || hasPathSum(root.right, sum);
    }
}
```

# 2. 路径总和2

113\. Path Sum II (Medium)

[Leetcode](https://leetcode.com/problems/path-sum-ii/) / [力扣](https://leetcode-cn.com/problems/path-sum-ii/)

https://github.com/grandyang/leetcode/issues/113
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

# 3. 路径总和3

437\. Path Sum III (Easy)

[Leetcode](https://leetcode.com/problems/path-sum-iii/) / [力扣](https://leetcode.com/problems/path-sum-iii/)

https://github.com/grandyang/leetcode/issues/437
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

# 4. 求根到叶子节点数字之和

129\. Sum Root to Leaf Numbers (Medium)

[Leetcode](https://leetcode.com/problems/sum-root-to-leaf-numbers/) / [力扣](https://leetcode-cn.com/problems/sum-root-to-leaf-numbers/)

https://github.com/grandyang/leetcode/issues/129
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

# 5. 删除给定值的叶子节点

1325\. Delete Leaves With a Given Value (Medium)

[Leetcode](https://leetcode.com/problems/delete-leaves-with-a-given-value/) / [力扣](https://leetcode-cn.com/problems/delete-leaves-with-a-given-value/)

https://github.com/grandyang/leetcode/issues/1325
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

# 6. 二叉树中的最大路径和

124\. Binary Tree Maximum Path Sum (Hard)

[Leetcode](https://leetcode.com/problems/binary-tree-maximum-path-sum/) / [力扣](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/)

https://github.com/grandyang/leetcode/issues/124
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

# 7. 戳印序列

936\. Stamping The Sequence (Hard)

[Leetcode](https://leetcode.com/problems/stamping-the-sequence/) / [力扣](https://leetcode-cn.com/problems/stamping-the-sequence/)

https://github.com/grandyang/leetcode/issues/936
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
