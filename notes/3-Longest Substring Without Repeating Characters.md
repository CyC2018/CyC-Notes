[Leetcode](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

## hashmap(char-last index) + sliding window

1. 建立hashmap，每个字符对应其最后出现位置的index。
2. 建立滑动窗口，两个指针，left为-1，rgiht为0，这样是左开右闭区间(left, right]，所以最后的时候可以更新窗口大小为right-left。
3. right指针每向右移动一个字符，两种情况，有重复和无重复。有重复：检查该字符是否已经出现过（在hashmap里）并且在滑动窗口里（上次出现位置大于left指针），有重复则更新left指针到其上次出现的位置（因为左闭右开区间，所以虽然left指向它，但它不在滑动窗口里，这样保证了left始终为当前边界的前一个位置）。无重复：那就啥都不用干（不更新left指针）。这样我们始终保持滑动窗口是合法的，没有重复字符。
4. 在hashmap里更新right当前字符的位置作为最后一次出现的位置。
5. 计算当前滑动窗口的大小并更新最大长度。

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> map = new HashMap<>();
        int res = 0;
        for (int left = -1, right = 0; right < s.length(); right++) { // (left, right]
            char c = s.charAt(right);
            // if find repeating char, update left to the last index of that char in the string
            left = map.containsKey(c) ? Math.max(map.get(c), left) : left;
            // update the current char to its newest index
            map.put(c, right);
            // the window is always valid, so we always update the max result
            res = Math.max(res, right - left); // len = right - left because of (left, right]
        }
        return res;
    }
}
```

## int array + sliding window

这里我们可以建立一个128长度大小的整型数组来代替hashmap，这样做的原因是ASCII表共能表示256个字符，但是由于键盘只能表示128个字符，所以用128也行，然后全部初始化为-1，这样的好处是不用像之前的hashmap一样要查找当前字符是否存在映射对了，对于每一个遍历到的字符，直接用其在数组中的值来更新left。

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int[] arr = new int[128];
        Arrays.fill(arr, -1);
        int res = 0;
        for (int left = -1, right = 0; right < s.length(); right++) { // (left, right]
            char c = s.charAt(right);
            // if find repeating char, update left to the last index of that char in the string
            left = Math.max(left, arr[c]);
            // update the current char to its newest index
            arr[c] = right;
            // the window is always valid, so we always update the max result
            res = Math.max(res, right - left); // len = right - left because of (left, right]
        }
        return res;
    }
}
```

## hashset + sliding window

下面这种解法使用了 HashSet，核心算法和上面的很类似，把出现过的字符都放入 HashSet 中，遇到 HashSet 中没有的字符就加入 HashSet 中并更新结果 res，如果遇到重复的，则从左边开始删字符，直到删到重复的字符停止。

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        Set<Character> set = new HashSet<>();
        int res = 0;
        for (int left = -1, right = 0; right < s.length(); right++) { // (left, right]
            char c = s.charAt(right);
            // if find repeating char, update left to the last index of that char in the string
            while (set.contains(c)) {
                left++;
                set.remove(s.charAt(left));
            }
            // update the current char to its newest index
            set.add(c);
            // the window is always valid, so we always update the max result
            res = Math.max(res, right - left); // len = right - left because of (left, right]
        }
        return res;
    }
}
```
