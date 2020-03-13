<!-- GFM-TOC -->
* [438-Find All Anagrams in a String](https://github.com/yhx89757/CS-Notes/blob/master/notes/438-Find%20All%20Anagrams%20in%20a%20String.md)
* [76-Minimum Window Substring](https://github.com/yhx89757/CS-Notes/blob/master/notes/76-Minimum%20Window%20Substring.md)
* [3-Longest Substring Without Repeating Characters](https://github.com/yhx89757/CS-Notes/blob/master/notes/3-Longest%20Substring%20Without%20Repeating%20Characters.md)
* [30-Substring with Concatenation of All Words](https://github.com/yhx89757/CS-Notes/blob/master/notes/30-Substring%20with%20Concatenation%20of%20All%20Words.md)
* [159-Longest Substring with At Most Two Distinct Characters](https://github.com/yhx89757/CS-Notes/edit/master/notes/159-Longest%20Substring%20with%20At%20Most%20Two%20Distinct%20Characters.md)
* [340-Longest Substring with At Most K Distinct Characters](https://github.com/yhx89757/CS-Notes/edit/master/notes/340-Longest%20Substring%20with%20At%20Most%20K%20Distinct%20Characters.md)
* [395-Longest Substring with At Least K Repeating Characters](https://github.com/yhx89757/CS-Notes/blob/master/notes/395-Longest%20Substring%20with%20At%20Least%20K%20Repeating%20Characters.md)
* [424-Longest Repeating Character Replacement](https://github.com/yhx89757/CS-Notes/blob/master/notes/424-Longest%20Repeating%20Character%20Replacement.md)
* [1052-Grumpy Bookstore Owner](https://github.com/yhx89757/CS-Notes/blob/master/notes/1052-Grumpy%20Bookstore%20Owner.md)
* [1208-Get Equal Substrings Within Budget](https://github.com/yhx89757/CS-Notes/blob/master/notes/1208-Get%20Equal%20Substrings%20Within%20Budget.md)
* [567-Permutation in String](https://github.com/yhx89757/CS-Notes/blob/master/notes/567-Permutation%20in%20String.md)
<!-- GFM-TOC -->

https://zhuanlan.zhihu.com/p/90664857

https://www.jianshu.com/p/869f6d00d962

https://leetcode.com/problems/find-all-anagrams-in-a-string/discuss/92007/Sliding-Window-algorithm-template-to-solve-all-the-Leetcode-substring-search-problem.


## template
```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> res = new ArrayList<>();
        // check special cases
        if (s == null || p == null || s.length() == 0 || p.length() == 0) return res;
        // create an int hashing array
        int[] hash = new int[128];
        // optional, initialize this int array
        for (char c : p.toCharArray()) hash[c]++;
        // define left, right pointer and counter, the counter has different meaning in different questions
        int left = 0, right = 0, cnt = 0;
        // always start with a while loop
        while (right < s.length()) {
            // first check the char by the right pointer, see if we need to increase the counter
            if (hash[s.charAt(right)] > 0) cnt++;
            // decrease the corresponding position in hash array
            hash[s.charAt(right)]--;
            // make right pointing to the next char to be judged, so the window is [left, right) beyond this point
            right++;
            // use another while loop to see if we need to shrink the left side of the window by checking the counter
            while (cnt == p.length()) {
                // optional, see if we need to update the result here
                if (right - left == p.length()) res.add(left);
                // before shrinking the left side, see if we need to decrease the counter
                if (hash[s.charAt(left)] >= 0) cnt--;
                // increase and recovering the position in hash array
                hash[s.charAt(left)]++;
                // make left pointing to the next, finally, if the counter is back to normal, we will be pointing to the valid char
                left++;
            }
        }
        // return the result
        return res;
    }
}
```

