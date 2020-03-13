[Leetcode](https://www.lintcode.com/problem/longest-substring-with-at-most-k-distinct-characters/description)

## hashmap(char-frequency) + counter(distinct chars) + sliding window

做滑动窗口的题的时候，最关键的是理解hashmap代表什么，cnt代表什么。

```java
public class Solution {
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        if (s == null || k == 0 || s.length() == 0) return 0;
        if (k >= s.length()) return s.length();
        HashMap<Character, Integer> hash = new HashMap<>();
        int left = 0, right = 0, cnt = 0, res = 0;
        while (right < s.length()) {
            if (!hash.containsKey(s.charAt(right))) cnt++;
            hash.put(s.charAt(right), hash.getOrDefault(s.charAt(right), 0) + 1);
            right++;
            while (cnt > k) {
                if (hash.get(s.charAt(left)) == 1) {
                    cnt--;
                    hash.remove(s.charAt(left));
                } else {
                    hash.put(s.charAt(left), hash.get(s.charAt(left)) - 1);
                }
                left++;
            }
            res = Math.max(res, right - left);
        }
        return res;
    }
}
```

