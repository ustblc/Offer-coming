#### 链表中倒数的第K个结点

##### 题目描述

输入一个链表，输出该链表中倒数第k个结点。

<!--more-->

##### 法一：这一题是经典的双指针类的题目，如果做过找到链表中的中间结点，那么你一定对于这一题有相关的想法。我们还是采用快慢指针，让快指针先走(K - 1)步，（这里要注意的是，如果快指针还没走完K-1步，就成空指针了，也就意味着K的值大于链表的长度了，此时要直接返回null！）然后快慢指针同时走，那么等快指针走到最后一个结点，那么慢指针正好走到倒数第K的结点。

```java
public ListNode FindKthToTail(ListNode head,int k) {
    if (head == null || k <= 0) {
        return null;
    }
    ListNode slow = head;
    ListNode fast = slow;
    while (k > 1) {
        fast = fast.next;
        if (fast == null) {
            return null;
        }
        k--;
    }
    while(fast.next != null) {
        fast = fast.next;
        slow = slow.next;
    }
    return slow;
}
```

