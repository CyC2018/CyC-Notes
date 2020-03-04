<!-- GFM-TOC -->
* [1. Find All Anagrams in a String](#1-找到字符串中所有字母异位词)
* [2. Minimum Window Substring](#2-最小覆盖子串)
* [3. Longest Substring Without Repeating Characters](#3-无重复字符的最长子串)
* [4. Substring with Concatenation of All Words](#4-串联所有单词的子串)
* [5. Longest Substring with At Most Two Distinct Characters](#5-至多包含两个不同字符的最长子串)
* [6. Longest Substring with At Most K Distinct Characters](#6-至多包含K个不同字符的最长子串)
<!-- GFM-TOC -->

https://zhuanlan.zhihu.com/p/90664857
https://www.jianshu.com/p/869f6d00d962
https://leetcode.com/problems/find-all-anagrams-in-a-string/discuss/92007/Sliding-Window-algorithm-template-to-solve-all-the-Leetcode-substring-search-problem.

# 1. 找到字符串中所有字母异位词

438\. Find All Anagrams in a String (Medium)

[Leetcode](https://leetcode.com/problems/find-all-anagrams-in-a-string/) / [力扣](https://leetcode-cn.com/problems/find-all-anagrams-in-a-string/)

```java
public class Solution {
    public List<Integer> findAnagrams(String s, String t) {
        List<Integer> result = new LinkedList<>();
        if(t.length()> s.length()) return result;
        Map<Character, Integer> map = new HashMap<>();
        for(char c : t.toCharArray()){
            map.put(c, map.getOrDefault(c, 0) + 1);
        }
        int counter = map.size();
        
        int begin = 0, end = 0;
        int head = 0;
        int len = Integer.MAX_VALUE;
        
        
        while(end < s.length()){
            char c = s.charAt(end);
            if( map.containsKey(c) ){
                map.put(c, map.get(c)-1);
                if(map.get(c) == 0) counter--;
            }
            end++;
            
            while(counter == 0){
                char tempc = s.charAt(begin);
                if(map.containsKey(tempc)){
                    map.put(tempc, map.get(tempc) + 1);
                    if(map.get(tempc) > 0){
                        counter++;
                    }
                }
                if(end-begin == t.length()){
                    result.add(begin);
                }
                begin++;
            }
            
        }
        return result;
    }
}
```

# 2. 最小覆盖子串

76\. Minimum Window Substring (Hard)

[Leetcode](https://leetcode.com/problems/minimum-window-substring/) / [力扣](https://leetcode-cn.com/problems/minimum-window-substring/)


```java
public class Solution {
    public String minWindow(String s, String t) {
        if(t.length()> s.length()) return "";
        Map<Character, Integer> map = new HashMap<>();
        for(char c : t.toCharArray()){
            map.put(c, map.getOrDefault(c,0) + 1);
        }
        int counter = map.size();
        
        int begin = 0, end = 0;
        int head = 0;
        int len = Integer.MAX_VALUE;
        
        while(end < s.length()){
            char c = s.charAt(end);
            if( map.containsKey(c) ){
                map.put(c, map.get(c)-1);
                if(map.get(c) == 0) counter--;
            }
            end++;
            
            while(counter == 0){
                char tempc = s.charAt(begin);
                if(map.containsKey(tempc)){
                    map.put(tempc, map.get(tempc) + 1);
                    if(map.get(tempc) > 0){
                        counter++;
                    }
                }
                if(end-begin < len){
                    len = end - begin;
                    head = begin;
                }
                begin++;
            }
            
        }
        if(len == Integer.MAX_VALUE) return "";
        return s.substring(head, head+len);
    }
}
```

# 3. 无重复字符的最长子串

3\. Longest Substring Without Repeating Characters (Medium)

[Leetcode](https://leetcode.com/problems/longest-substring-without-repeating-characters/) / [力扣](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)


```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> map = new HashMap<>();
        int begin = 0, end = 0, counter = 0, d = 0;

        while (end < s.length()) {
            // > 0 means repeating character
            //if(map[s.charAt(end++)]-- > 0) counter++;
            char c = s.charAt(end);
            map.put(c, map.getOrDefault(c, 0) + 1);
            if(map.get(c) > 1) counter++;
            end++;
            
            while (counter > 0) {
                //if (map[s.charAt(begin++)]-- > 1) counter--;
                char charTemp = s.charAt(begin);
                if (map.get(charTemp) > 1) counter--;
                map.put(charTemp, map.get(charTemp)-1);
                begin++;
            }
            d = Math.max(d, end - begin);
        }
        return d;
    }
}
```

# 4. 串联所有单词的子串

30\. Substring with Concatenation of All Words (Hard)

[Leetcode](https://leetcode.com/problems/substring-with-concatenation-of-all-words/) / [力扣](https://leetcode-cn.com/problems/substring-with-concatenation-of-all-words/)


```java
public class Solution {
    public List<Integer> findSubstring(String S, String[] L) {
        List<Integer> res = new LinkedList<>();
        if (L.length == 0 || S.length() < L.length * L[0].length())   return res;
        int N = S.length();
        int M = L.length; // *** length
        int wl = L[0].length();
        Map<String, Integer> map = new HashMap<>(), curMap = new HashMap<>();
        for (String s : L) {
            if (map.containsKey(s))   map.put(s, map.get(s) + 1);
            else                      map.put(s, 1);
        }
        String str = null, tmp = null;
        for (int i = 0; i < wl; i++) {
            int count = 0;  // remark: reset count 
            int start = i;
            for (int r = i; r + wl <= N; r += wl) {
                str = S.substring(r, r + wl);
                if (map.containsKey(str)) {
                    if (curMap.containsKey(str))   curMap.put(str, curMap.get(str) + 1);
                    else                           curMap.put(str, 1);
                    
                    if (curMap.get(str) <= map.get(str))    count++;
                    while (curMap.get(str) > map.get(str)) {
                        tmp = S.substring(start, start + wl);
                        curMap.put(tmp, curMap.get(tmp) - 1);
                        start += wl;
                        
                        //the same as https://leetcode.com/problems/longest-substring-without-repeating-characters/
                        if (curMap.get(tmp) < map.get(tmp)) count--;
                        
                    }
                    if (count == M) {
                        res.add(start);
                        tmp = S.substring(start, start + wl);
                        curMap.put(tmp, curMap.get(tmp) - 1);
                        start += wl;
                        count--;
                    }
                }else {
                    curMap.clear();
                    count = 0;
                    start = r + wl;//not contain, so move the start
                }
            }
            curMap.clear();
        }
        return res;
    }
}
```

# 5. 至多包含两个不同字符的最长子串

159\. Longest Substring with At Most Two Distinct Characters (Medium)

[Leetcode](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/) / [力扣](https://leetcode-cn.com/problems/longest-substring-with-at-most-two-distinct-characters/)


```java
public class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        Map<Character,Integer> map = new HashMap<>();
        int start = 0, end = 0, counter = 0, len = 0;
        while(end < s.length()){
            char c = s.charAt(end);
            map.put(c, map.getOrDefault(c, 0) + 1);
            if(map.get(c) == 1) counter++;//new char
            end++;
            while(counter > 2){
                char cTemp = s.charAt(start);
                map.put(cTemp, map.get(cTemp) - 1);
                if(map.get(cTemp) == 0){
                    counter--;
                }
                start++;
            }
            len = Math.max(len, end-start);
        }
        return len;
    }
}
```

# 6. 至多包含K个不同字符的最长子串

340\. Longest Substring with At Most K Distinct Characters (Hard)

[Leetcode](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/) / [力扣](https://leetcode-cn.com/problems/longest-substring-with-at-most-k-distinct-characters/)

Given a string, find the length of the longest substring T that contains at mostk distinct characters.
For example,Given s = “eceba” and k = 2,
T is "ece" which its length is 3.

```java
public class Solution {
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        if(s == null || s.length() == 0 || k <= 0) {
            return 0;
        }
        
        char[] ss = s.toCharArray();
        int[] scount = new int[256];
        int count = 0;
        int res = 0;
        int j = 0;
        // 同向双指针模板；
        for(int i = 0; i < s.length(); i++) {
            while(j < s.length() && count <= k) {
                // j move到即将要超过k的时候，停下来，scount[ss[j]]不做任何事情；
                // 等待下一次while循环，j就可以update了；
                if(scount[ss[j]] == 0) {
                    if(count == k){
                        break;
                    }
                    count++;
                }
                scount[ss[j]]++;
                j++;
            }
            
            res = Math.max(res, j - i);
            
            //update i;
            scount[ss[i]]--;
            if(scount[ss[i]] == 0) {
                count--;
            }
        }
        return res;
    }
}
```





