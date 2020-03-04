<!-- GFM-TOC -->
* [1. Missing Number](#1-缺失数字)
* [2. Find All Numbers Disappeared in an Array](#2-缺失数字)
* [3. Find the Duplicate Number](#3-寻找重复数)
* [4. Find All Duplicates in an Array](#4-数组中重复的数据)
* [5. First Missing Positive](#5-缺失的第一个正数)
<!-- GFM-TOC -->


https://zhuanlan.zhihu.com/p/90664857

# 1. 缺失数字

268\. Missing Number (Easy)

[Leetcode](https://leetcode.com/problems/missing-number/) / [力扣](https://leetcode-cn.com/problems/missing-number/)

https://github.com/grandyang/leetcode/issues/268
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

# 2. 找到所有数组中消失的数字

448\. Find All Numbers Disappeared in an Array (Easy)

[Leetcode](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/) / [力扣](https://leetcode-cn.com/problems/find-all-numbers-disappeared-in-an-array/)

https://github.com/grandyang/leetcode/issues/448
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

# 3. 寻找重复数

287\. Find the Duplicate Number (Medium)

[Leetcode](https://leetcode.com/problems/find-the-duplicate-number/) / [力扣](https://leetcode-cn.com/problems/find-the-duplicate-number/)

https://github.com/grandyang/leetcode/issues/287
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

# 4. 数组中重复的数据

442\. Find All Duplicates in an Array (Medium)

[Leetcode](https://leetcode.com/problems/find-all-duplicates-in-an-array/) / [力扣](https://leetcode-cn.com/problems/find-all-duplicates-in-an-array/)

https://github.com/grandyang/leetcode/issues/442
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

# 5. 缺失的第一个正数

41\. First Missing Positive (Hard)

[Leetcode](https://leetcode.com/problems/first-missing-positive/) / [力扣](https://leetcode-cn.com/problems/first-missing-positive/)

https://github.com/grandyang/leetcode/issues/41
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
