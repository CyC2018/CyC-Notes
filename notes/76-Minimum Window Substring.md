[Leetcode](https://leetcode.com/problems/minimum-window-substring/)

## int array + sliding window

左闭右开区间，右指针不管怎样每次都往右移动的，直到区间合法，也就是cnt大小为t的长度大小，然后开始缩小左区间，看看最短能多短。
要记在心里的一点是，对于右指针来说，hash数组里只要对应的数大于0，那么窗口里的该字符还不够，cnt++。对于左指针来说，hash数组里只要对应数大于等于0，这个字符肯定在t里。还有一点要注意的是，有时候窗口里的该字符虽然在t里，但是由于窗口里该字符数量超过t里该字符数量，也是有可能被减到负数的。这就是为什么我们一定需要有cnt的原因！cnt记录的是在滑动窗口里有多少个**有效**字符！（多余的被减成负数了，就不会对cnt有任何影响了）
但是！不在t里的字符无论何时在hash数组里的数都不可能大于0！（进入窗口变负数，出窗口变回0）

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
                if (minLen > right - left) { // [left, right)
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
