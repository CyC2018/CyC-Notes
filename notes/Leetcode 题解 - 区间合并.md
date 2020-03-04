<!-- GFM-TOC -->
* [1. Merge Intervals](#1-合并区间)
* [2. Insert Interval](#2-插入区间)
* [3. Interval List Intersections](#3-区间列表的交集)
* [4. My Calendar I](#4-我的日程安排表1)
<!-- GFM-TOC -->


https://zhuanlan.zhihu.com/p/90664857

# 1. 合并区间

56\. Merge Intervals (Medium)

[Leetcode](https://leetcode.com/problems/merge-intervals/) / [力扣](https://leetcode-cn.com/problems/merge-intervals/)

https://github.com/grandyang/leetcode/issues/56
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

# 2. 插入区间

57\. Insert Interval (Hard)

[Leetcode](https://leetcode.com/problems/insert-interval/) / [力扣](https://leetcode-cn.com/problems/insert-interval/)

https://github.com/grandyang/leetcode/issues/57
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

# 3. 区间列表的交集

986\. Interval List Intersections (Medium)

[Leetcode](https://leetcode.com/problems/interval-list-intersections/) / [力扣](https://leetcode-cn.com/problems/interval-list-intersections/)

https://leetcode-cn.com/problems/interval-list-intersections/solution/qu-jian-lie-biao-de-jiao-ji-by-leetcode/
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

# 4. 我的日程安排表1

729\. My Calendar I (Medium)

[Leetcode](https://leetcode.com/problems/my-calendar-i/) / [力扣](https://leetcode-cn.com/problems/my-calendar-i/)

https://github.com/grandyang/leetcode/issues/729
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
