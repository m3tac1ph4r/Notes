#  Add Two Numbers

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**

![[add_two_numbers_ex.png]]

**Input:** l1 = [2,4,3], l2 = [5,6,4]
**Output:** [7,0,8]
**Explanation:** 342 + 465 = 807.

**Example 2:**

**Input:** l1 = [0], l2 = [0]
**Output:** [0]

**Example 3:**

**Input:** l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
**Output:** [8,9,9,9,0,0,0,1]


### Notes

- **Dummy Head (`ans`):** A placeholder node that acts as the start of our result list. It helps us avoid checking if the list is empty every time we add a digit.
- **Carry:** An integer to hold the "extra" value when a sum is 10 or greater.    
- **Pointers:** `l1` and `l2` move through the input lists, while `head` builds the new list.


1. **The Common Part:** Loop through both lists simultaneously. Add digits + carry. If the sum is $\ge 10$, set `carry = 1` and keep the remainder.
2. **The Leftovers:** If one list is longer than the other, keep looping through the remaining digits of that list (don't forget to keep adding the carry!).
3. **The Final Check:** If there is still a carry of `1` left after both lists are finished, create one last node for it (e.g., $99 + 1$ needs that extra node for the $100$).
4. **The "Return":** We return `ans.next` because the very first node (`-1`) was just a placeholder.


- **Time Complexity:** $O(n)$ — You only visit each node once.    
- **Space Complexity:** $O(n)$ — You create a new list for the answer.

```java
̌class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode head = new ListNode(-1, null);
        ListNode ans=head;
        int carry = 0, sum = 0, rem = 0;
        while (l1 != null && l2 != null) {
            sum = l1.val + l2.val + carry;
            ListNode nextNode = null;
            if (sum >= 10) {
                rem = sum % 10;
                carry = 1;
                nextNode = new ListNode(rem, null);
            } else {
                rem = 0;
                carry = 0;
                nextNode = new ListNode(sum, null);
            }
            head.next = nextNode;
            head=head.next;
            l1 = l1.next;
            l2 = l2.next;
        }

        while (l1 != null) {
            sum = l1.val + carry;
            ListNode nextNode = null;
            if (sum >= 10) {
                rem = sum % 10;
                carry = 1;
                nextNode = new ListNode(rem, null);
            } else {
                rem = 0;
                carry = 0;
                nextNode = new ListNode(sum, null);
            }
            head.next = nextNode;
            head=head.next;
            l1 = l1.next;
        }

        while (l2 != null) {
            sum = l2.val + carry;
            ListNode nextNode = null;
            if (sum >= 10) {
                rem = sum % 10;
                carry = 1;
                nextNode = new ListNode(rem, null);
            } else {
                rem = 0;
                carry = 0;
                nextNode = new ListNode(sum, null);
            }
            head.next = nextNode;
            head=head.next;
            l2 = l2.next;
        }

        if(carry==1){
            ListNode nextNode=new ListNode(1,null);
            head.next=nextNode;
        }

        return ans.next;
    }
}
```


### Link
https://leetcode.com/problems/add-two-numbers/