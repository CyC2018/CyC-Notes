[Leetcode](https://www.lintcode.com/problem/longest-substring-with-at-most-two-distinct-characters/description)

## hashmap(char-frequency) + counter(distinct chars) + sliding window

做滑动窗口的题的时候，最关键的是理解hashmap代表什么，cnt代表什么。

```java
public class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        int res = 0;
        HashMap<Character, Integer> hash = new HashMap<>();
        int left = 0, right = 0, cnt = 0;
        while (right < s.length()) {
            if (!hash.containsKey(s.charAt(right))) cnt++;
            hash.put(s.charAt(right), hash.getOrDefault(s.charAt(right), 0) + 1);
            right++;
            while (cnt > 2) {
                if (hash.get(s.charAt(left)) == 1) {
                    cnt--;
                    hash.remove(s.charAt(left));
                } else {
                    hash.put(s.charAt(left), hash.getOrDefault(s.charAt(left), 0) - 1);
                }
                left++;
            }
            res = Math.max(res, right - left);
        }
        return res;
    }
}
```
