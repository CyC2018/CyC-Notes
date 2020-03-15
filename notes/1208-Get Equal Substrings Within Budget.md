[Leetcode](https://leetcode.com/problems/get-equal-substrings-within-budget/)

## curCost + sliding window

前面几个滑动窗口的题目做过之后会觉得这道题非常简单，直接用滑动窗口框住满足要求（curCost <= maxCost）的子字符串就行了，不满足要求就不断缩小左边界。

```java
class Solution {
    public int equalSubstring(String s, String t, int maxCost) {
        if (s == null || s.length() == 0) return 0;
        int left = 0, right = 0, curCost = 0, res = 0;
        while (right < s.length()) {
            curCost += Math.abs(s.charAt(right) - t.charAt(right));
            right++;
            while (curCost > maxCost) {
                curCost -= Math.abs(s.charAt(left) - t.charAt(left));
                left++;
            }
            res = Math.max(res, right - left);
        }
        return res;
    }
}
```
