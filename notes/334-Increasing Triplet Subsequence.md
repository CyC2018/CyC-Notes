[Leetcode](https://leetcode.com/problems/increasing-triplet-subsequence/)

## sort + counter

排序然后再数越来越大的数。时间O(NlogN)，空间O(1)。

## dynamic programming

这道题让我们求一个无序数组中是否有任意三个数字是递增关系的，我最先相处的方法是用一个dp数组，dp[i]表示在i位置之前小于等于nums[i]的数字的个数(包括其本身)，我们初始化dp数组都为1，然后我们开始遍历原数组，对当前数字nums[i]，我们遍历其之前的所有数字，如果之前某个数字nums[j]小于nums[i]，那么我们更新dp[i] = max(dp[i], dp[j] + 1)，如果此时dp[i]到3了，则返回true，若遍历完成，则返回false。
时间O(N^2)，空间O(N)。

```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
        if (nums == null || nums.length < 3) return false;
        int[] dp = new int[nums.length];
        Arrays.fill(dp, 1);
        for (int i = 0; i < nums.length; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                    if (dp[i] >= 3) return true;
                }
            }
        }
        return false;
    }
}
```
## forward-backward arrays

这种方法的虽然不满足常数空间的要求，但是作为对暴力搜索的优化，也是一种非常好的解题思路。这个解法的思路是建立两个数组，forward数组和backward数组，其中forward[i]表示[0, i]之间最小的数，backward[i]表示[i, n-1]之间最大的数，那么对于任意一个位置i，如果满足 forward[i] < nums[i] < backward[i]，则表示这个递增三元子序列存在，举个例子来看吧，比如：

foward:      8  3  3  1  1
nums:        8  3  5  1  6
backward:    8  6  6  6  6

我们发现数字5满足forward[i] < nums[i] < backward[i]，所以三元子序列存在。

```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
        if (nums == null || nums.length < 3) return false;
        int n = nums.length;
        int[] forward = new int[n];
        int[] backward = new int[n];
        forward[0] = nums[0];
        backward[n - 1] = nums[n - 1];
        // forward
        for (int i = 1; i < n; i++) {
            forward[i] = Math.min(forward[i - 1], nums[i]);
        }
        // backward
        for (int i = n - 2; i >= 0; i--) {
            backward[i] = Math.max(backward[i + 1], nums[i]);
        }
        // find valid triplet
        for (int i = 0; i < n; i++) {
            if (nums[i] > forward[i] && nums[i] < backward[i]) return true;
        }
        return false;
    }
}
```

## greedy

但是题目中要求我们O(n)的时间复杂度和O(1)的空间复杂度，上面的那种方法一条都没满足，所以白写了。我们下面来看满足题意的方法，这个思路是使用两个指针m1和m2，初始化为整型最大值，我们遍历数组，如果m1大于等于当前数字，则将当前数字赋给m1；如果m1小于当前数字且m2大于等于当前数字，那么将当前数字赋给m2，一旦m2被更新了，说明一定会有一个数小于m2，那么我们就成功的组成了一个长度为2的递增子序列，所以我们一旦遍历到比m2还大的数，我们直接返回ture。如果我们遇到比m1小的数，还是要更新m1，有可能的话也要更新m2为更小的值，毕竟m2的值越小，能组成长度为3的递增序列的可能性越大。

```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
        if (nums == null || nums.length == 0) return false;
        int firstMin = Integer.MAX_VALUE, secondMin = Integer.MAX_VALUE;
        for (int num : nums) {
            if (num <= firstMin) {
                firstMin = num;
            } else if (num <= secondMin) {
                secondMin = num;
            } else if (num > secondMin) {
                return true;
            }
        }
        return false;
    }
}
```
