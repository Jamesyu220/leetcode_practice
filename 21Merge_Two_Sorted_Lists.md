Python:  
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def mergeTwoLists(self, list1, list2):
        """
        :type list1: Optional[ListNode]
        :type list2: Optional[ListNode]
        :rtype: Optional[ListNode]
        """
        cur = dummy = ListNode()
        while True:
            if list1 is None:
                cur.next = list2
                break
            if list2 is None:
                cur.next = list1
                break
            if list1.val <= list2.val:
                cur.next = list1
                list1 = list1.next
            elif list1.val > list2.val:
                cur.next = list2
                list2 = list2.next
            cur = cur.next    
                
        return dummy.next
```        
