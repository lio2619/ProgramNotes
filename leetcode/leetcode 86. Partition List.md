
題目網址：[Partition List - LeetCode](https://leetcode.com/problems/partition-list/description/)
## 問題

#### 題目大綱

>Given the `head` of a linked list and a value `x`, partition it such that all nodes **less than** `x` come before nodes **greater than or equal** to `x`.
>You should **preserve** the original relative order of the nodes in each of the two partitions.

###### 1
**Input:** head = [1,4,3,2,5,2], x = 3
**Output:** [1,2,2,4,3,5]
###### 2
**Input:** head = [2,1], x = 2
**Output:** [1,2]
## 解法

這個問題是要把比X還要小的值移到前面，並且順序不能有變動

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def partition(self, head: Optional[ListNode], x: int) -> Optional[ListNode]:
        small, big = ListNode(0), ListNode(0)
        #因為之後會操作ListNode所以將ListNode複製過來
        smallCurr, bigCurr = small, big
        
        while head:
            if x > head.val:
                smallCurr.next = head
                smallCurr = smallCurr.next
            else:
                bigCurr.next = head
                bigCurr = bigCurr.next
            head = head.next

        bigCurr.next = None
        smallCurr.next = big.next
        return small.next
```

#leetcode #linkedlist #twopointer 