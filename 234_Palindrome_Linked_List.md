Given the head of a singly linked list, return true if it is a palindrome or false otherwise.  

Example 1:  
```
Input: head = [1,2,2,1]
Output: true
```
Example 2:  
```
Input: head = [1,2]
Output: false
```

Code:  
```c++
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
    bool isPalindrome(ListNode* head) {
        ListNode *fast, *slow;
        fast = head;
        slow = head;
        if(!slow -> next) return head;
        while(fast && fast -> next) {
            fast = fast -> next -> next;
            slow = slow -> next;
        }
        ListNode* second_head = reverseList(slow);
        return equalList(head, second_head);
    }
    ListNode* reverseList(ListNode* head) {
        if(!head -> next) return head;
        ListNode* new_head = reverseList(head -> next);
        head -> next -> next = head;
        head -> next = NULL;
        return new_head;
    }
    bool equalList(ListNode* p, ListNode* q) {
        if(!p || !q) return true;
        if(p -> val != q -> val) return false;
        return equalList(p -> next, q -> next);
    }
};
```

Runtime: 256 ms, faster than 61.14% of C++ online submissions for Palindrome Linked List.  
Memory Usage: 116.4 MB, less than 69.25% of C++ online submissions for Palindrome Linked List.
