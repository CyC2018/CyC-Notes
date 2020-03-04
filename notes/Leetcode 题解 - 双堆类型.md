<!-- GFM-TOC -->
* [1. Find Median from Data Stream](#1-数据流的中位数)
* [2. Sliding Window Median](#2-滑动窗口中位数)
* [3. IPO](#3-IPO)
<!-- GFM-TOC -->


https://zhuanlan.zhihu.com/p/90664857

# 1. 数据流的中位数

295\. Find Median from Data Stream (Hard)

[Leetcode](https://leetcode.com/problems/find-median-from-data-stream/) / [力扣](https://leetcode-cn.com/problems/find-median-from-data-stream/)

https://github.com/grandyang/leetcode/issues/295
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

# 2. 滑动窗口中位数

480\. Sliding Window Median (Hard)

[Leetcode](https://leetcode.com/problems/sliding-window-median/) / [力扣](https://leetcode.com/problems/sliding-window-median/)

https://github.com/grandyang/leetcode/issues/480
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

# 3. IPO

502\. IPO (Hard)

[Leetcode](https://leetcode.com/problems/ipo/) / [力扣](https://leetcode-cn.com/problems/ipo/)

https://github.com/grandyang/leetcode/issues/502
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
