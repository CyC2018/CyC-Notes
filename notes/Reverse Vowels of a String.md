[Leetcode](https://leetcode.com/problems/reverse-vowels-of-a-string/)

## two pointers
```java
class Solution {
    private final HashSet<Character> set = new HashSet<>(
        Arrays.asList('a','e','i','o','u','A','E','I','O','U'));
    public String reverseVowels(String s) {
        if (s == null) return null;
        int left = 0, right = s.length() - 1;
        char[] res = new char[s.length()];
        while (left <= right) {
            if (!set.contains(s.charAt(left))) {
                res[left] = s.charAt(left);
                left++;
            } else if (!set.contains(s.charAt(right))) {
                res[right] = s.charAt(right);
                right--;
            } else {
                res[left] = s.charAt(right);
                res[right] = s.charAt(left);
                left++;
                right--;
            }
        }
        return new String(res);
    }
}
```
