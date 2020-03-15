[Leetcode](https://leetcode.com/problems/rotate-array/)

## cyclic replacement

1. 从第一个数开始，往右跳k个位置把那个位置的数覆盖掉，被覆盖掉的数用临时变量存起来，再用临时变量里的数从原先位置跳k个位置去覆盖其他数，一直循环下去。
2. 这个做法有个问题是，当数组长度正好能被k整除时，一次while循环是不够的，因为有些位置无论如何也无法到达，比如下面这个例子：
[1,2,3,4,5,6], k = 2
这个循环一直在位置0,2,4这几个位置转移，而无法到达其他位置；一个解决方法是在这个循环外层套一个大循环，这个大循环遍历数组的每个元素(事实上，最坏情况也就是遍历数组一半的元素)。
内层循环每执行一轮，就有一个元素被挪到了正确的位置，称这为一次操作，当内层循环执行完时，我们考察操作次数是否等于数组长度，如果等于就可以结束大循环。
上面的实现，虽然嵌套了两层循环，但实际上每个元素只被访问了一次（内层的循环要么一次做完整个数组，要么互不干扰）。
3. 注意我们这里用两个temp，temp1表示上次被挤出来的值，temp2保存下一次将要被挤出来的值，再把上次被挤出来的值temp1覆盖到下次的位置上，最后再更新temp1=temp2。
4. 时间复杂度O(N)，空间复杂度O(1)。

```java
class Solution {
    public void rotate(int[] nums, int k) {
        k = k % nums.length;
        int cnt = 0;
        for (int i = 0; i < nums.length; i++) {
            int cur = i, temp1 = nums[i], temp2;
            do {
                // every time we put one element into the right position
                // and meanwhile put the element in that position into the temperory space
                int next = (cur + k) % nums.length; 
                temp2 = nums[next];
                nums[next] = temp1;
                // next time we will put the element in the temp space into its right position
                cur = next;
                temp1 = temp2;
                cnt++;
            } while (cur != i);
            if (cnt == nums.length) break;
        }
    }
}
```
recursion way
```java
class Solution {
    private int cnt = 0;
    public void rotate(int[] nums, int k) {
        k %= nums.length;
        // start of the loop
        int start = 0;
        // pointer
        int cur = start;
        // get into the recursion
        helper(nums, k, start, cur, nums[cur]);
    }
    
    private void helper(int[] nums, int k, int start, int cur, int temp1) {
        if (cnt == nums.length || k == 0) return;
        // the next position
        int next = (cur + k) % nums.length;
        // save that value before covering it
        int temp2 = nums[next];
        // cover it with previous value
        nums[next] = temp1;
        // update previous value
        temp1 = temp2;
        // update pointer
        cur = next;
        // increase the counter, each recursion we put a number into its target position
        cnt++;
        // if there's a loop we start with the next position, also update pointer and temp1
        if (cur == start) {
            start++;
            cur = start;
            temp1 = nums[cur];
        }
        // go to the next recursion
        helper(nums, k, start, cur, temp1);
    }
}
```

## triple reverse

1. 这道题其实还有种类似翻转字符的方法，思路是先把整个数组翻转一下，再把前k个数字翻转一下，最后把后n-k个数字翻转一下。
2. 时间复杂度O(N)，空间复杂度O(1)。

原始数组                  : 1 2 3 4 5 6 7    (k=3)
反转所有数字后             : 7 6 5 4 3 2 1
反转前 k 个数字后          : 5 6 7 4 3 2 1
反转后 n-k 个数字后        : 5 6 7 1 2 3 4 --> 结果

```java
class Solution {
    public void rotate(int[] nums, int k) {
        k %= nums.length;
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }
    
    private void reverse(int[] nums, int i, int j) {
        while (i < j) {
            int temp = nums[i];
            nums[i] = nums[j];
            nums[j] = temp;
            i++;
            j--;
        }
    }
}
```

## in-place swap into subproblem

[1,2,3,4,5,6,7,8] k=3

1. 看k是否大于数组长度，如果大于则取余数，因为两者旋转结果是一样的。
2. 第一轮for循环先把后k位跟最前面k位swap一下，这样前面k位就正确了，之后不用管了。
[6,7,8,1,2,3,4,5]
3. 中间的数+后面的数组成一个新的子问题，这个问题的关键在于，刚才把前k位换到后k位去了，相当于什么？相当于把前k位像左旋转k次一样的效果！那么一串数字向左旋转k次等价于像右旋转n-k次！这就可以转化为一个子问题，用同样的解法去解这个子问题。
4. 现在为了解决这个新的子问题，我们更新数组长度n=n-k,因为前面k位已经正确了，剩下的长度就是这个。再更新start为start+k,从中间的数开始。
5. 既然我们更新了n，在下一轮for循环之前依然要跟新k=k%n，那么就要检查一下n不为0，k也不为0，再继续。
6. 下一轮for循环从中间数开始，但是，就像刚才分析的那样，我们这回要从新的start开始，向右旋转n-k次，然后因为我们用的是swap而不是真的旋转，我们又会生成一个新的子问题。
7. 如此循环直到n的长度为1或0，或者k为0为止，就不必再旋转，问题解决。
8. 时间复杂度因为每次循环都会把最后k个数放到正确的位置（这也就是我们为什么每次for循环后把n=n-k的原因），所以只需要n-1次swap即可，所以时间复杂度为O(n)。
9. 空间复杂度为O(1)很明显没有创建其他数组。

[出处](https://leetcode.com/problems/rotate-array/discuss/54263/3-lines-of-c-in-one-pass-using-swap)

Rotating k steps to the right would move the last (n-k) elements to the front, so [6,7,8] are moved to their final position in the 1st iteration.

Now, since [6,7,8] are fixed, we only have to consider about other elements (i.e. [4,5,1,2,3]), that is why (n-=k, nums+=k).
Since we have swapped the first three elements [1,2,3] to the end of the array (It is equal to rotate [1,2,3,4,5] n-k times) in the 1st iteration, we need to rotate it back (i.e. k times) to meet our goal.

Rotating [4,5,1,2,3] to the right k times is a subproblem to the original problem, so the explanation is similar to the above. Just repeat the subproblem until there is no more element to swap.

Note: Rotating k steps to the right is equal to rotate k+n steps to the right. That is the reason for k %= n;

```java
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        int start = 0;
        while (n != 0 && (k %= n) != 0) {
            for (int i = 0; i < k; i++) {
                swap(nums, start + i, start + n - k + i);
            }
            n -= k;
            start += k;
        }
    }
    
    private void swap(int[] nums, int p1, int p2) {
        int temp = nums[p1];
        nums[p1] = nums[p2];
        nums[p2] = temp;
    }
}
```
其实可以把for循环里面的start+n换成nums.length，因为是等价的，每次start加k的同时n会减去k，其实想想也对，每次我们尝试把后面k个右移到前面去，但是我们用swap而不是真正的移，所以还得再尝试“移”。
```java
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        int start = 0;
        while (n != 0 && (k %= n) != 0) {
            for (int i = 0; i < k; i++) {
                swap(nums, start + i, nums.length - k + i);
            }
            n -= k;
            start += k;
        }
    }
    
    private void swap(int[] nums, int p1, int p2) {
        int temp = nums[p1];
        nums[p1] = nums[p2];
        nums[p2] = temp;
    }
}
```
这个方法用recursion也许更容易理解
```java
class Solution {
    public void rotate(int[] nums, int k) {
        recursiveSwap(nums, k, 0, nums.length);
    }
    private void recursiveSwap(int[] nums, int k, int start, int n) {
        k %= n;
        if (k != 0) {
            for (int i = 0; i < k; i++) {
                swap(nums, start + i, nums.length - k + i);
            }
            recursiveSwap(nums, k, start + k, n - k);
        }
    }
    private void swap(int[] nums, int p1, int p2) {
        int temp = nums[p1];
        nums[p1] = nums[p2];
        nums[p2] = temp;
    }
}
```
