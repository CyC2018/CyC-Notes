[Leetcode](https://leetcode.com/problems/longest-repeating-character-replacement/)

## int array(char-frequency) + sliding window

这道题给我们了一个字符串，说我们有k次随意置换任意字符的机会，让我们找出最长的重复字符的字符串。这道题跟之前那道 Longest Substring with At Most K Distinct Characters 很像，都需要用滑动窗口 Sliding Window 来解。我们首先来想，如果没有k的限制，让我们求把字符串变成只有一个字符重复的字符串需要的最小置换次数，那么就是字符串的总长度减去出现次数最多的字符的个数。如果加上k的限制，我们其实就是求满足(**子字符串的长度减去出现次数最多的字符个数**)<=k的最大子字符串长度即可，搞清了这一点，我们也就应该知道怎么用滑动窗口来解了吧。

还有一点最关键的是，当滑动窗口的左边界向右移动了后，窗口内的相同字母的最大个数貌似可能会改变啊，为啥这里不用更新maxCnt呢？这是个好问题，原因是此题让求的是最大合法窗口，maxCnt物理意义是相当于到目前为止，某个字符出现的最大频率。其他滑动窗口题的解法是会缩小左边界的，这道题有点不同，因为缩小左边界再更新maxCnt会很麻烦（可以是可以，就是要遍历所有存在count数组里的值）。现在我这个代码的逻辑是，只要窗口不合法，我懒得缩小左边界，我直接向右平移，保留窗口的大小，虽然平移之后有可能不合法，但是再平移几次我也许能遇到个合法的，甚至找到更大的频率，扩大我的窗口大小！（因为扩大窗口的唯一办法是maxCnt+k，k永远不变的，我只要能找到一段子串中有更大的maxCnt，我的窗口就**有可能**扩大，因为我还需要k个不同字符在窗口里）。

下面是论坛里的解释：

Many people know the problem can be reiterated as :
"longest substring where (length - max occurrence) <= k"
The key point is we are focusing on "longest".
So assume we initially found a valid substring, what do we do next?

Still valid even appended by one more char——then we are happy, just expand the window
It became invalid. But at this time, do we have to shrink the window?
——No, we shift the whole window rightwards by one unit. So that the length is unchanged.
The reason for that is , any index smaller than original "start", will never have the chance to lead a longer valid substring than current length of our window.
Do we need to update max in time?
——No. Once again, we focus on "longest". The length of valid substring is determined by what?
Max Occurrence + k
We only need to update max occurrence when it becomes larger, because only that can we generate a longer valid substring.
If we can't surpass the historic max occurrence, then we can not generate a longer valid substring from current "start", I mean the new windows's left bound. To some extend, this becomes a game to find max occurrence.
Or , a better understanding is:
"A game to eliminate inferior 'left bounds'.

We just maintain the window with a size that holds the maximum length of substring we have found so far
the key point is tracking the max frequency and compare the size of CURRENT largest window - maxFrequency with k.

```java
class Solution {
    public int characterReplacement(String s, int k) {
        if (s == null || s.length() == 0) return 0;
        if (k >= s.length()) return s.length();
        int[] count = new int[26];
        int left = 0, right = 0, res = 0, maxCnt = 0;
        while (right < s.length()) {
            count[s.charAt(right) - 'A']++;
            maxCnt = Math.max(maxCnt, count[s.charAt(right) - 'A']);
            right++;
            while (right - left - maxCnt > k) {
                count[s.charAt(left) - 'A']--;
                left++;
            }
            res = Math.max(res, right - left);
        }
        return res;
    }
}
```
