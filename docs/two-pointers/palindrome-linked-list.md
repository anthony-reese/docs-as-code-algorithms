# 234. Palindrome Linked List

## Problem Statement
Given the `head` of a singly linked list, return `true` if it is a palindrome or `false` otherwise.

---

## Approach:  Two Pointers

Use two pointers to find the middle of the list, reverse the second half, and compare both halves for equality.

### Finding the Middle:

- Use two pointers (slow and fast) to identify the middle of the linked list. The slow pointer moves one step at a time, while fast moves two steps. When fast reaches the end, slow will be at the middle.

### Reversing the Second Half:

- Reverse the portion of the linked list starting from the middle. This allows for an in-place comparison of values.

### Comparing Both Halves:

- Compare the first half of the linked list to the reversed second half. If all values match, the list is a palindrome.

---

/**\
 &nbsp;\* Definition for singly-linked list.\
 &nbsp;\* struct ListNode {\
 &nbsp;\*     int val;\
 &nbsp;\*     ListNode *next;\
 &nbsp;\*     ListNode( ) : val(0), next(nullptr) { }\
 &nbsp;\*     ListNode(int x) : val(x), next(nullptr) { }\
 &nbsp;\*     ListNode(int x, ListNode *next) : val(x), next(next) { }\
&nbsp;\* };\
&nbsp;\*/

```cpp
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        if (!head || !head->next) return true;

        ListNode* slow = head;
        ListNode* fast = head;
        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
        }
            
        ListNode* prev = nullptr;
        ListNode* current = slow;
        while (current) {
            ListNode* temp = current->next;
            current->next = prev;
            prev = current;
            current = temp;
        }

        ListNode* left = head;
        ListNode* right = prev;
        while (right) {
            if (left->val != right->val) {
                return false;
            }
            left = left->next;
            right = right->next;                    
        }            
        return true;
    }
};
```

## Complexity

- Time Complexity: 𝑂(𝑛) — 
    The list is traversed multiple times:

    - To find the middle of the list.

    - To reverse the second half.

    - To compare the two halves.

- Space Complexity: 𝑂(1) — No additional space is used other than pointers.

## Conclusion
This in-place solution checks for palindrome efficiently with linear time and constant space.