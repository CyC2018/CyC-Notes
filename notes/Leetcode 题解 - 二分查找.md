<!-- GFM-TOC -->
* [69. Sqrt(x)](#1-求开方)
* [744. Find Smallest Letter Greater Than Target](#2-大于给定元素的最小元素)
* [540. Single Element in a Sorted Array](#3-有序数组的-single-element)
* [278. First Bad Version](#4-第一个错误的版本)
* [153. Find Minimum in Rotated Sorted Array](#5-旋转数组的最小数字)
* [327. Count of Range Sum](#6-查找区间)
* [35. Search Insert Position](#6-查找区间)
* [33. Search in Rotated Sorted Array](#6-查找区间)
* [81. Search in Rotated Sorted Array II](#6-查找区间)
* [34. Find First and Last Position of Element in Sorted Array](#6-查找区间)
* [4. Median of Two Sorted Arrays](https://github.com/yhx89757/CS-Notes/blob/master/notes/4.%20Median%20of%20Two%20Sorted%20Arrays.md)
<!-- GFM-TOC -->

五种常见二分查找题型大总结：

https://www.cnblogs.com/grandyang/p/6854825.html

二分查找终极模板：

https://leetcode-cn.com/problems/binary-search/solution/er-fen-cha-zhao-xiang-jie-by-labuladong/

## template

```java
int binary_search(int[] nums, int target) {
    int left = 0, right = nums.length - 1; 
    while(left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1; 
        } else if(nums[mid] == target) {
            // 直接返回
            return mid;
        }
    }
    // 直接返回
    return -1;
}

int left_bound(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] == target) {
            // 别返回，继续往左边找
            right = mid - 1;
        }
    }
    // 最后要检查 left 越界的情况，返回什么检查什么
    if (left >= nums.length || nums[left] != target)
        return -1;
    return left;
}


int right_bound(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] == target) {
            // 别返回，继续往右边找
            left = mid + 1;
        }
    }
    // 最后要检查 right 越界的情况，返回什么检查什么
    if (right < 0 || nums[right] != target)
        return -1;
    return right;
}
```
## special template

这种模板比较简单暴力，因为用while (left < right - 1) 每次都是左边界在与右边界正好相邻的时候停下来，然后做一个post processing后处理，两个if语句判断一下哪个边界是我们要找的答案。

```java
int binary_search(int[] nums, int target) {
    int left = 0, right = nums.length - 1; 
    while(left < right - 1) { // 这里留意
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid; // 这里留意
        } else if (nums[mid] > target) {
            right = mid; // 这里留意
        } else if(nums[mid] == target) {
            // 直接返回
            return mid;
        }
    }
    // 后处理
    if (nums[left] == target) return left;
    if (nums[right] == target) return right;
    return -1;
}
```
**正常实现**  

```text
Input : [1,2,3,4,5]
key : 3
return the index : 2
```

```java
public int binarySearch(int[] nums, int key) {
    int l = 0, h = nums.length - 1;
    while (l <= h) {
        int m = l + (h - l) / 2;
        if (nums[m] == key) {
            return m;
        } else if (nums[m] > key) {
            h = m - 1;
        } else {
            l = m + 1;
        }
    }
    return -1;
}
```

**时间复杂度**  

二分查找也称为折半查找，每次都能将查找区间减半，这种折半特性的算法时间复杂度为 O(logN)。

**m 计算**  

有两种计算中值 m 的方式：

- m = (l + h) / 2
- m = l + (h - l) / 2

l + h 可能出现加法溢出，也就是说加法的结果大于整型能够表示的范围。但是 l 和 h 都为正数，因此 h - l 不会出现加法溢出问题。所以，最好使用第二种计算法方法。

**未成功查找的返回值**  

循环退出时如果仍然没有查找到 key，那么表示查找失败。可以有两种返回值：

- -1：以一个错误码表示没有查找到 key
- l：将 key 插入到 nums 中的正确位置

**变种**  

二分查找可以有很多变种，实现变种要注意边界值的判断。例如在一个有重复元素的数组中查找 key 的最左位置的实现如下：

```java
public int binarySearch(int[] nums, int key) {
    int l = 0, h = nums.length - 1;
    while (l < h) {
        int m = l + (h - l) / 2;
        if (nums[m] >= key) {
            h = m;
        } else {
            l = m + 1;
        }
    }
    return l;
}
```

该实现和正常实现有以下不同：

- h 的赋值表达式为 h = m
- 循环条件为 l < h
- 最后返回 l 而不是 -1

在 nums[m] >= key 的情况下，可以推导出最左 key 位于 [l, m] 区间中，这是一个闭区间。h 的赋值表达式为 h = m，因为 m 位置也可能是解。

在 h 的赋值表达式为 h = m 的情况下，如果循环条件为 l <= h，那么会出现循环无法退出的情况，因此循环条件只能是 l < h。以下演示了循环条件为 l <= h 时循环无法退出的情况：

```text
nums = {0, 1, 2}, key = 1
l   m   h
0   1   2  nums[m] >= key
0   0   1  nums[m] < key
1   1   1  nums[m] >= key
1   1   1  nums[m] >= key
...
```

当循环体退出时，不表示没有查找到 key，因此最后返回的结果不应该为 -1。为了验证有没有查找到，需要在调用端判断一下返回位置上的值和 key 是否相等。

# 1. 求开方

69\. Sqrt(x) (Easy)

[Leetcode](https://leetcode.com/problems/sqrtx/description/) / [力扣](https://leetcode-cn.com/problems/sqrtx/description/)

```html
Input: 4
Output: 2

Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since we want to return an integer, the decimal part will be truncated.
```

一个数 x 的开方 sqrt 一定在 0 \~ x 之间，并且满足 sqrt == x / sqrt。可以利用二分查找在 0 \~ x 之间查找 sqrt。

对于 x = 8，它的开方是 2.82842...，最后应该返回 2 而不是 3。在循环条件为 left <= right 并且循环退出时，right 总是比 left 小 1，也就是说 right = 2，left = 3，因此最后的返回值应该为 right 而不是 left。

这道题额外要注意的是，要先求出sqrt = x / mid，否则如果直接用mid * mid和x来比的话，mid * mid乘积很有可能超出int正数范围变成负数。两种解决方法，一种提前求出sqrt，另一种是所有变量全改为long，最后再转回int作为答案返回。

```java
class Solution {
    public int mySqrt(int x) {
        if (x <= 1) return x;
        int left = 0, right = x;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            int sqrt = x / mid;
            if (mid == sqrt) return mid;
            else if (mid < sqrt) left = mid + 1;
            else right = mid - 1;
        }
        if (left * left == x) return left;
        return right;
    }
}
```

# 2. 大于给定元素的最小元素

744\. Find Smallest Letter Greater Than Target (Easy)

[Leetcode](https://leetcode.com/problems/find-smallest-letter-greater-than-target/description/) / [力扣](https://leetcode-cn.com/problems/find-smallest-letter-greater-than-target/description/)

```html
Input:
letters = ["c", "f", "j"]
target = "d"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "k"
Output: "c"
```

题目描述：给定一个有序的字符数组 letters 和一个字符 target，要求找出 letters 中大于 target 的最小字符，如果找不到就返回第 1 个字符。

```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        int left = 0, right = letters.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (letters[mid] == target) left = mid + 1;
            else if (letters[mid] < target) left = mid + 1;
            else right = mid - 1;
        }
        return left < letters.length ? letters[left] : letters[0];
    }
}
```

# 3. 有序数组的 Single Element

540\. Single Element in a Sorted Array (Medium)

[Leetcode](https://leetcode.com/problems/single-element-in-a-sorted-array/description/) / [力扣](https://leetcode-cn.com/problems/single-element-in-a-sorted-array/description/)

```html
Input: [1, 1, 2, 3, 3, 4, 4, 8, 8]
Output: 2
```

题目描述：一个有序数组只有一个数不出现两次，找出这个数。

要求以 O(logN) 时间复杂度进行求解，因此不能遍历数组并进行异或操作来求解，这么做的时间复杂度为 O(N)。

令 index 为 Single Element 在数组中的位置。在 index 之后，数组中原来存在的成对状态被改变。如果 m 为偶数，并且 m + 1 < index，那么 nums[m] == nums[m + 1]；m + 1 >= index，那么 nums[m] != nums[m + 1]。

从上面的规律可以知道，如果 nums[m] == nums[m + 1]，那么 index 所在的数组位置为 [m + 2, h]，此时令 l = m + 2；如果 nums[m] != nums[m + 1]，那么 index 所在的数组位置为 [l, m]，此时令 h = m。

因为 h 的赋值表达式为 h = m，那么循环条件也就只能使用 l < h 这种形式。

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int left = 0, right = nums.length - 1;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (mid % 2 == 1) {
                mid--;  // 保证 left/right/mid 都在偶数位，使得查找区间大小一直都是奇数
            }
            if (nums[mid] == nums[mid + 1]) {
                left = mid + 2;
            } else {
                right = mid;
            }
        }
        return nums[left];
    }
}
```

# 4. 第一个错误的版本

278\. First Bad Version (Easy)

[Leetcode](https://leetcode.com/problems/first-bad-version/description/) / [力扣](https://leetcode-cn.com/problems/first-bad-version/description/)

题目描述：给定一个元素 n 代表有 [1, 2, ..., n] 版本，在第 x 位置开始出现错误版本，导致后面的版本都错误。可以调用 isBadVersion(int x) 知道某个版本是否错误，要求找到第一个错误的版本。

相当于模板里寻找左边界，因为一定有解，所以不用最后检查右指针的合法性。

```java
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int left = 1, right = n;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (isBadVersion(mid) == false) left = mid + 1;
            else right = mid - 1;
        }
        return left;
    }
}
```


# 5. 旋转数组的最小数字

153\. Find Minimum in Rotated Sorted Array (Medium)

[Leetcode](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/) / [力扣](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/description/)

```html
Input: [3,4,5,1,2],
Output: 1
```

这道题left和right相邻时停下来是最省心的，不用check是否出界。

```java
class Solution {
    public int findMin(int[] nums) {
        int left = 0;
        int right = nums.length - 1;
        while (left < right - 1) {
            int mid = left + (right - left) / 2;
            if (nums[mid] > nums[right]) {
                left = mid;
            } else {
                right = mid;
            }
        }
        return nums[left] < nums[right] ? nums[left] : nums[right];
    }
}
```

# 6. 查找区间

34\. Find First and Last Position of Element in Sorted Array

[Leetcode](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) / [力扣](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

```html
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]

Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

题目描述：给定一个有序数组 nums 和一个目标 target，要求找到 target 在 nums 中的第一个位置和最后一个位置。

可以用二分查找找出第一个位置和最后一个位置，但是寻找的方法有所不同，需要实现两个二分查找。我们将寻找  target 最后一个位置，转换成寻找 target+1 第一个位置，再往前移动一个位置。这样我们只需要实现一个二分查找代码即可。

代码直接套寻找左边界的模板代码即可。

细节上的思考，因为我们return的是left，所以找不到target只有三种情况：
1. target小于左边界，left是0。我们检测nums[first] != target可以知道。
2. target大于右边界，left是num.length。我们检测first >= nums.length可以知道。
3. target就在边界里，但是大小介于数组的相邻两个数之间。我们检测nums[first] != target可以知道。
所以上述三种情况下都要返回new int[]{-1, -1}。

再来讨论last，找target+1也有三种情况：
1. target+1小于左边界，left是0。这种情况first是通不过第一个if语句的，所以不用担心。
2. target+1大于右边界，left是num.length。这种情况如果first通过第一个if语句，就说明target存在且在右边界，此时last是nums.length - 1没问题。
3. target+1就在边界里，但是大小介于数组的相邻两个数之间。这种情况left肯定是在比target大的下一个数，所以此时last是最后一个target没问题。
所以不用处理last直接放到结果中去就可以了。

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        if (nums == null || nums.length == 0) return new int[]{-1, -1};
        int first = findFirst(nums, target);
        int last = findFirst(nums, target + 1) - 1;
        if (first >= nums.length || nums[first] != target) {
            return new int[]{-1, -1};
        } else {
            return new int[]{first, last};
        }
    }
    
    private int findFirst(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                right = mid - 1;
            } else if (nums[mid] > target) {
                right = mid - 1; 
            } else {
                left = mid + 1;
            }
        }
        return left;
    }
}
```


<div align="center"><img width="320px" src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/githubio/公众号二维码-2.png"></img></div>
