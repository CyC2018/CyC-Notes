[Leetcode](https://leetcode.com/problems/grumpy-bookstore-owner/)

## fixed sliding window(for unsatisfied customers)

这道题还是比较容易想出O(N)的时间复杂度的解法的，但是下面这个方法虽然也是O(N)，但思想比较巧妙。关键就是对滑动窗口的解读不一样，这个解法对不满足的顾客建立了一个滑动窗口（大小为X），也就是有潜在可能被满足的顾客。用satisfied记录已经被满足的顾客，记录了后就不用管它了。用canSatisfied记录滑动窗口内的不满足的顾客的数量，窗口大小**固定**为X，从左到右滑过去记录最大出现的值，然后再加上已经满足的顾客satisfied数量就是我们的结果。

注意此方法对不满足的顾客建立滑动窗口，而不是已经满足的顾客。这道题给我们的启发是，滑动窗口的题目最关键的是怎么定义窗口，这个窗口里面记录的东西是有待改善的东西！如果是利益最大化，窗口里存的是可以改善的东西。如果是求什么字符串最大长度，那就是另一种思想，窗口大小最大化，窗口里存的就是满足题目限制条件的东西或者不满足限制条件的东西。

```java
class Solution {
    public int maxSatisfied(int[] customers, int[] grumpy, int X) {
        if (customers == null || customers.length == 0) return 0;
        int satisfied = 0, canSatisfied = 0, maxCanSatisfied = 0;
        for (int i = 0; i < customers.length; i++) {
            if (grumpy[i] == 0) satisfied += customers[i];
            else canSatisfied += customers[i];
            if (i >= X) {
                canSatisfied -= grumpy[i - X] * customers[i - X];
            }
            maxCanSatisfied = Math.max(maxCanSatisfied, canSatisfied);
        }
        return satisfied + maxCanSatisfied;
    }
}
```
