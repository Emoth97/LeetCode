Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.

Example 1:
	
	Input: 1->2->3->4->5->NULL
	Output: 1->3->5->2->4->NULL

Example 2:
	
	Input: 2->1->3->5->6->4->7->NULL
	Output: 2->3->6->7->1->5->4->NULL

Note:

>The relative order inside both the even and odd groups should remain as it was in the input.  
>The first node is considered odd, the second node even and so on ...

#注意点：
>1.设置两个指针，一个指向奇数位置的结点，另一个指向偶数位置的结点。
>
>2.遍历结束时要将奇数指针（此时指向最后一个奇数结点）的next设置为第一个偶数结点，偶数指针（此时指向最后一个偶数结点）的next设置为NULL！

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode* oddEvenList(struct ListNode* head) {
	    if(NULL == head || NULL == head->next) { return head; }
	    struct ListNode *odd = head, *even = head->next, *cur = head->next->next, *tmp = even;
	    for(int i = 3; NULL != cur; i++, cur = cur->next) {
	        if(1 == i % 2) {
	            odd->next = cur;
	            odd = cur;
	        } else {
	            even->next = cur;
	            even = cur;
	        }
	    }
	    odd->next = tmp;
	    even->next = NULL;
	    return head;
	}

