[Leetcode](https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/)

## int array(char-frequency) + mask(check if any frequency less than k) + sliding window(left side fixed)

首先声明这个不是最优解法，这个用一个for循环遍历窗口的左边界，然后再不断扩展右边界，遇到满足条件的更新结果，时间复杂度O(N^2)，空间复杂度O(1)。
这道题的难点就在于，如何检查每个窗口里的元素都出现k次！如果你用hashmap存储，你每次检查的时候还得把int array或者hashmap用O(26)=O(1)的时间重新扫描一遍每个字符的出现频率，如果用了mask，出现等于或超过k次的字符在对应bit位直接设置为0，否则为1，这样每次只要检查mask是否为0即可，这个技巧很耐用！

这叫右增大窗口，并不是真正的滑动窗口。但是这个解法用for循环遍历左边界并不是最节省时间的方法。因为这个方法外面的for loop跟s的长度有关，把时间复杂度弄成了平方级别的，下面一个方法告诉我们如何把这个for loop从O(N)级别转化成O(1)级别，从而把整个算法降成O(N)级别。

```java
class Solution {
    public int longestSubstring(String s, int k) {
        if (s == null || s.length() == 0 || k > s.length()) return 0;
        int res = 0;
        for (int i = 0; i < s.length(); i++) {
            int left = i, right = i, mask = 0;
            int[] hash = new int[26];
            while (right < s.length()) {
                hash[s.charAt(right) - 'a']++;
                if (hash[s.charAt(right) - 'a'] >= k) mask &= ~(1 << (s.charAt(right) - 'a'));
                else mask |= (1 << (s.charAt(right) - 'a'));
                right++;
                if (mask == 0) res = Math.max(res, right - left);
            }
        }
        return res;
    }
}
```

## int array(char-frequency) + for loop(unique chars) + sliding window

跟以往滑动窗口解法有所不同，加了一层for循环遍历从1到26。第一个循环查找只包含有一种字符的子串，第二个循环查找只包含两种不同字符的子串...这样最多包含26种不同字符。curUnique记录当前有多少种不同字符在滑动窗口里，maxUnique记录最多能在滑动窗口里包含的不相同字符数。

为什么要加这个for loop循环呢？我个人认为，第一个是给我们滑动窗口左边界缩小找到了理由，第二个是跟上一种解法相比，从另一个角度看问题，把for loop从**跟s长度相关O(N)级别**巧妙转化成了**跟不同字符个数相关O(1)级别**的时间复杂度。

**其实看到这里，我们发现了滑动窗口的题目最关键的是什么时候缩小左边界，有的时候根据题目里的限制条件缩小左边界，有的时候像这道题，需要我们自己创造或者添加限制条件，而右边界都是每个循环都增长的我们不用管它。**

```java
class Solution {
    public int longestSubstring(String s, int k) {
        if (s == null || s.length() == 0 || k > s.length()) return 0;
        int res = 0;
        for (int maxUnique = 1; maxUnique <= 26; maxUnique++) {
            int left = 0, right = 0, curUnique = 0;
            int[] hash = new int[26];
            while (right < s.length()) {
                boolean valid = true;
                if (hash[s.charAt(right) - 'a'] == 0) curUnique++;
                hash[s.charAt(right) - 'a']++;
                right++;
                while (curUnique > maxUnique) {
                    if (hash[s.charAt(left) - 'a'] == 1) curUnique--;
                    hash[s.charAt(left) - 'a']--;
                    left++;
                }
                for (int i = 0; i < 26; i++) {
                    if (hash[i] > 0 && hash[i] < k) valid = false;
                }
                if (valid == true) res = Math.max(res, right - left);
            }
        }
        return res;
    }
}
```

## divide and conquer(recursion)

分治法，分割有效子字符串。事先统计好每个字符出现的次数放在数组里，然后遍历每个字符串字母，两种情况：
1. 如果该字符总出现次数小于k，那就包含该字符的子字符串不可能有效，所以以该字符为中点分割，左边所有字符串再用此函数递归下去（注意左边**可能是有效的**，所以我们还需要用递归），继续向右遍历。
2. 如果该字符总出现次数大于或等于k，继续向右遍历。

如果整个字符串都没发现不合法字符，valid始终是true，那就返回整个字符串长度，这个也是base case。

要注意一点是每层递归都需要后处理（post processing），上一次不合法字符出现位置到字符串结尾也需要用递归检测一下，不要漏掉了。

这里关键的一点是，当分割字符串时候，左边并不能保证有效，所以我们还要递归左边，虽然左边所有字符总出现次数大于等于k，但是也有可能一部分在右边，从而使左边无效的，无效的话左边递归下去再次生成统计数组会发现该字符不合法，会把它剔除掉。其实这个分治思想在这题的体现是不断剔除不合法字符，检测剩余字符串的过程。

```java
class Solution {
    public int longestSubstring(String s, int k) {
        int start = 0, res = 0;
        int[] hash = new int[128];
        boolean valid = true;
        for (char c : s.toCharArray()) hash[c]++;
        for (int i = 0; i < s.length(); i++) {
            if (hash[s.charAt(i)] < k) {
                res = Math.max(res, longestSubstring(s.substring(start, i), k));
                valid = false;
                start = i + 1;
            }
        }
        if (valid == false) {
            res = Math.max(res, longestSubstring(s.substring(start, s.length()), k));
        }
        return valid == true ? s.length() : res;
    }
}
```
