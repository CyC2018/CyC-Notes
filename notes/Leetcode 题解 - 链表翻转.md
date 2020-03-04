<!-- GFM-TOC -->
* [1. Reverse Linked List](#1-反转链表)
* [2. Reverse Linked List II](#2-反转链表2)
* [3. Reverse Nodes in k-Group](#3-K个一组翻转链表)
<!-- GFM-TOC -->

https://zhuanlan.zhihu.com/p/90664857

# 1. 反转链表

206\. Reverse Linked List (Easy)

[Leetcode](https://leetcode.com/problems/reverse-linked-list/) / [力扣](https://leetcode-cn.com/problems/reverse-linked-list/)

https://github.com/grandyang/leetcode/issues/206
```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode cur = head;
        while (cur != null) {
            ListNode temp = cur.next;
            cur.next = prev;
            prev = cur;
            cur = temp;
        }
        return prev;
    }
}
```

# 2. 反转链表2

92\. Reverse Linked List II (Medium)

[Leetcode](https://leetcode.com/problems/reverse-linked-list-ii/) / [力扣](https://leetcode-cn.com/problems/reverse-linked-list-ii/)

https://github.com/grandyang/leetcode/issues/92
```java
 public boolean judgeSquareSum(int target) {
     if (target < 0) return false;
     int i = 0, j = (int) Math.sqrt(target);
     while (i <= j) {
         int powSum = i * i + j * j;
         if (powSum == target) {
             return true;
         } else if (powSum > target) {
             j--;
         } else {
             i++;
         }
     }
     return false;
 }
```

# 3. K个一组翻转链表

25\. Reverse Nodes in k-Group (Hard)

[Leetcode](https://leetcode.com/problems/reverse-nodes-in-k-group/) / [力扣](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)

https://github.com/grandyang/leetcode/issues/25
```java
 public boolean judgeSquareSum(int target) {
     if (target < 0) return false;
     int i = 0, j = (int) Math.sqrt(target);
     while (i <= j) {
         int powSum = i * i + j * j;
         if (powSum == target) {
             return true;
         } else if (powSum > target) {
             j--;
         } else {
             i++;
         }
     }
     return false;
 }
```
