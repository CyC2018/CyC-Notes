[Leetcode](https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/)

## int array + sliding window

1. 查看当前数组相应位置的正负性来判断是否在p字符串里，新进入窗口的字符一直在p中，窗口才会展开，否则一直缩小到负长度。
2. 每次循环查看窗口大小right-left是否等于p.length()来判断是否是一个合法的窗口。
3. 窗口左闭右开[left, right)
4. 时间复杂度O(N)，空间复杂度O(1)。

```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> res = new ArrayList<>();
        if (s == null || p == null || s.length() == 0 || p.length() == 0) return res;
        int[] hash = new int[128];
        for (int i = 0; i < p.length(); i++) hash[p.charAt(i)]++;
        int left = 0, right = 0; // [l,r) is window
        while (right < s.length()) {
            if (hash[s.charAt(right)] >= 1) { // this char is in p, expand the window
                hash[s.charAt(right)]--;
                right++;
            } else {                          // this char is not in p, shrink the window
                hash[s.charAt(left)]++;
                left++;
            }
            if (right - left == p.length()) res.add(left);
        }
        return res;
    }
}
```
