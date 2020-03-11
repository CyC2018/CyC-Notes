[Leetcode](https://leetcode.com/problems/minimum-window-substring/)

## int array + sliding window

左闭右开区间[left, right)

```java
class Solution {
    public String minWindow(String s, String t) {
        if (s == null || t == null || s.length() == 0 || t.length() == 0) return "";
        int left = 0, right = 0, cnt = 0, minLeft = -1, minLen = Integer.MAX_VALUE;
        int[] hash = new int[128];
        for (char c : t.toCharArray()) hash[c]++;
        while (right < s.length()) {
            if (hash[s.charAt(right)] > 0) cnt++;
            hash[s.charAt(right)]--;
            right++;
            while (cnt == t.length()) {
                if (minLen > right - left) {
                    minLen = right - left;
                    minLeft = left;
                }
                if (hash[s.charAt(left)] >= 0) cnt--;
                hash[s.charAt(left)]++;
                left++;
            }
        }
        return minLeft == -1 ? "" : s.substring(minLeft, minLeft + minLen);
    }
}
```
