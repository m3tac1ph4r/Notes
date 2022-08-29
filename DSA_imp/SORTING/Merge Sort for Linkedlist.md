# Merge Sort For Linkedlist

Given the `head` of a linked list, return _the list after sorting it in **ascending order**_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/14/sort_list_1.jpg)

**Input:** head = [4,2,1,3]
**Output:** [1,2,3,4]

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/09/14/sort_list_2.jpg)

**Input:** head = [-1,5,3,4,0]
**Output:** [-1,0,3,4,5]

**Example 3:**

**Input:** head = []
**Output:** []



### Approach (Using Merge Sort) :

1. Find middle of linkedlist using tortoise and haier approach
2. Then divide linkedlist in two halves left=start and right=mid->next. Then make mid->next to NULL
3. Do same recursively for left and right
4. Then merge left and right linkedlist


```cpp
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
    ListNode* findMid(ListNode* head)
    {  
        ListNode* slow=head;
        ListNode* fast=head->next;
        
        while(fast!=NULL and fast->next!=NULL)
        {
            slow=slow->next;
            fast=fast->next->next;
        }
        return slow;
    }
    ListNode* merge(ListNode* left,ListNode* right)
    {
        
        if(left==NULL)
            return right;
        if(right==NULL)
            return left;
        
        ListNode* ans=new ListNode(-1);
        ListNode* temp=ans;
        while(left!=NULL and right!=NULL)
        {
            if(left->val<right->val)
            {
                temp->next=left;
                temp=left;
                left=left->next;
            }
            else
            {
                temp->next=right;
                temp=right;
                right=right->next;
            }
        }
        
        while(left!=NULL)
        {
            temp->next=left;
            temp=left;
            left=left->next;
        }
        
        while(right!=NULL)
        {
            temp->next=right;
            temp=right;
            right=right->next;
        }
        
        ans=ans->next;
        return ans;
    }
    ListNode* mergeSort(ListNode* head)
    {
        if(head==NULL || head->next==NULL)
            return head;
        
        ListNode* mid=findMid(head);
        ListNode* left=head;
        ListNode* right=mid->next;
        mid->next=NULL;
        
        left=mergeSort(left);
        right=mergeSort(right);
        
        ListNode* result=merge(left,right);
        return result;
    }
    
	// main function
    ListNode* sortList(ListNode* head) {
        return mergeSort(head);
    }
};
```


### Question :
https://leetcode.com/problems/sort-list/

### Reference :
https://youtu.be/rM5EEA_rbNY