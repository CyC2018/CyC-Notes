<!-- GFM-TOC -->
* [1. LinkedList Cycle](#1-环形链表)
* [2. Linked List Cycle II](#2-环形链表 II)
* [3. Happy Number](#3-快乐数)
* [4. Middle of the LinkedList](#4-链表的中间结点)
<!-- GFM-TOC -->


https://zhuanlan.zhihu.com/p/90664857

# 1. 环形链表

141\. LinkedList Cycle (Easy)

[Leetcode](https://leetcode.com/problems/linked-list-cycle/) / [力扣](https://leetcode-cn.com/problems/linked-list-cycle/)

```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null) return false;
        ListNode p1 = head;
        ListNode p2 = head.next;
        while (p1 != null && p2 != null && p2.next != null) {
            if (p1 == p2) {
                return true;
            }
            p1 = p1.next;
            p2 = p2.next.next;
        }
        return false;
    }
}
```

# 2. 环形链表 II
	
142\. Linked List Cycle II (Medium)

[Leetcode](https://leetcode.com/problems/linked-list-cycle-ii/) / [力扣](https://leetcode-cn.com/problems/linked-list-cycle-ii/)


```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode fast = head, slow = head;
        while (true) {
            if (fast == null || fast.next == null) return null;
            fast = fast.next.next;
            slow = slow.next;
            if (fast == slow) break;
        }
        fast = head;
        while (slow != fast) {
            slow = slow.next;
            fast = fast.next;
        }
        return fast;
    }
}
```

# 3. 快乐数

202\. Happy Number (Easy)

[Leetcode](https://leetcode.com/problems/happy-number/) / [力扣](https://leetcode-cn.com/problems/happy-number/)

方法：使用“快慢指针”思想找出循环：“快指针”每次走两步，“慢指针”每次走一步，当二者相等时，即为一个循环周期。此时，判断是不是因为1引起的循环，是的话就是快乐数，否则不是快乐数。

注意：此题不建议用集合记录每次的计算结果来判断是否进入循环，因为这个集合可能大到无法存储；另外，也不建议使用递归，同理，如果递归层次较深，会直接导致调用栈崩溃。不要因为这个题目给出的整数是int型而投机取巧。

```java
class Solution {
public:
    int bitSquareSum(int n) {
        int sum = 0;
        while(n > 0)
        {
            int bit = n % 10;
            sum += bit * bit;
            n = n / 10;
        }
        return sum;
    }
    
    bool isHappy(int n) {
        int slow = n, fast = n;
        do{
            slow = bitSquareSum(slow);
            fast = bitSquareSum(fast);
            fast = bitSquareSum(fast);
        }while(slow != fast);
        
        return slow == 1;
    }
};
```

# 4. 链表的中间结点
	
876\. Middle of the Linked List (Easy)

[Leetcode](https://leetcode.com/problems/middle-of-the-linked-list/) / [力扣](https://leetcode-cn.com/problems/middle-of-the-linked-list/)


```java
public ListNode middleNode(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;
}
```
