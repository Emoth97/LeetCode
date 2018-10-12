Given a linked list, rotate the list to the right by k places, where k is non-negative.

Example 1:
	
	Input: 1->2->3->4->5->NULL, k = 2
	Output: 4->5->1->2->3->NULL
	Explanation:
	rotate 1 steps to the right: 5->1->2->3->4->NULL
	rotate 2 steps to the right: 4->5->1->2->3->NULL

Example 2:
	
	Input: 0->1->2->NULL, k = 4
	Output: 2->0->1->NULL
	Explanation:
	rotate 1 steps to the right: 2->0->1->NULL
	rotate 2 steps to the right: 1->2->0->NULL
	rotate 3 steps to the right: 0->1->2->NULL
	rotate 4 steps to the right: 2->0->1->NULL

#注意点：
>1.思路：循环链表，要考虑到循环的次数多于链表长度的情况。因此可以先遍历一次链表获取长度，基于长度获得要移动的次数。然后通过速度相同的快慢指针再遍历一次链表并修改指针指向即可。

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode* rotateRight(struct ListNode* head, int k) {
	    int count = 0;
	    struct ListNode *fast = head, *slow = head;
	    while(fast) { count++; fast = fast->next; }
	    if(!count) { return NULL; }
	    int shift = k % count;
	    fast = head;
	    while(shift--) {
	        fast = fast->next;
	    }
	    while(fast->next) {
	        fast = fast->next;
	        slow = slow->next;
	    }
	    fast->next = head;
	    fast = slow->next;
	    slow->next = NULL;
	    return fast;
	}