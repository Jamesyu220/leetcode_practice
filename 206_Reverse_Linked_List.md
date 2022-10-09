Given the head of a singly linked list, reverse the list, and return the reversed list.  

Code:  
```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(!head || !head -> next) return head;
        ListNode *next_1 = head -> next;
        ListNode *next_2 = next_1 -> next;
        next_1 -> next = head;
        head -> next = NULL;
        head = next_1;
        while(true) {            
            if(!next_2) return head;
            next_1 = next_2;
            next_2 = next_2 -> next;
            next_1 -> next = head;
            head = next_1;
        }
    }
};
```
Runtime: 14 ms, faster than 34.28% of C++ online submissions for Reverse Linked List.  
Memory Usage: 8.4 MB, less than 40.90% of C++ online submissions for Reverse Linked List.  
