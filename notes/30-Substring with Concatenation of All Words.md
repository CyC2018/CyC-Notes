[Leetcode](https://leetcode.com/problems/substring-with-concatenation-of-all-words/)

## hashmap(char-frequency) + hashmap(word-frequency) + counter + sliding window

直接套用模板！
先往右扩展通过不断检测cnt判断是否已经找到所有需要的字符，然后左端缩小来找到正好对应words里所有字符出现频率的字符串（因此长度也必须刚好相等），再isValid检测是否是word拼接起来的。
因为每个字长一样，所以isValid函数变得简单了，不然会很麻烦。

```java
class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> res = new ArrayList<>();
        if (s == null || s.length() == 0 || words == null || words.length == 0) return res;
        HashMap<Character, Integer> hash1 = new HashMap<>();
        HashMap<String, Integer> hash2 = new HashMap<>();
        HashMap<String, Integer> hash3;
        for (String w : words) {
            for (char c : w.toCharArray()) {
                hash1.put(c, hash1.getOrDefault(c, 0) + 1);
            }
            hash2.put(w, hash2.getOrDefault(w, 0) + 1);
        }
        hash3 = new HashMap(hash2);
        int left = 0, right = 0, cnt = 0;
        int numChars = words[0].length() * words.length;
        while (right < s.length()) {
            if (hash1.containsKey(s.charAt(right)) && hash1.get(s.charAt(right)) > 0) cnt++;
            hash1.put(s.charAt(right), hash1.getOrDefault(s.charAt(right), 0) - 1);
            right++;
            while (cnt == numChars) {
                if (right - left == numChars && isValid(s.substring(left, right), words[0].length(), hash3)) {
                    res.add(left);
                }
                hash3 = new HashMap(hash2);
                if (hash1.containsKey(s.charAt(left)) && hash1.get(s.charAt(left)) >= 0) cnt--;
                hash1.put(s.charAt(left), hash1.getOrDefault(s.charAt(left), 0) + 1);
                left++;
            }
        }
        return res;
    }
    private boolean isValid(String substr, int wordLen, HashMap<String, Integer> hash3) {
        int start = 0;
        while (start + wordLen <= substr.length()) {
            String subSubstr = substr.substring(start, start + wordLen);
            if (hash3.containsKey(subSubstr)) {
                if (hash3.get(subSubstr) == 1) hash3.remove(subSubstr);
                else hash3.put(subSubstr, hash3.get(subSubstr) - 1);
            } else {
                return false;
            }
            start += wordLen;
        }
        return true;
    }
}
```

## 
