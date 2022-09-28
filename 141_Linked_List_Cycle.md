Given head, the head of a linked list, determine if the linked list has a cycle in it.  

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer.  
Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.  

Return true if there is a cycle in the linked list. Otherwise, return false.  

Code:  
```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if(!head) return false;
        ListNode *fast, *slow;
        fast = head;
        slow = head;
        while(true) {
            if(fast -> next && fast -> next -> next) {
                fast = fast -> next -> next;
            }
            else return false;
            
            slow = slow -> next;
            
            if(fast == slow) return true;
        }    
    }
};
```
Runtime: 18 ms, faster than 54.67% of C++ online submissions for Linked List Cycle.  
Memory Usage: 8.1 MB, less than 58.26% of C++ online submissions for Linked List Cycle.  
