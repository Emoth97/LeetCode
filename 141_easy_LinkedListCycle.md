Given a linked list, determine if it has a cycle in it.

Follow up:
Can you solve it without using extra space?


#注意点：
>1.这道题是快慢指针的经典应用。只需要设两个指针，一个每次走一步的慢指针和一个每次走两步的快指针，如果链表里有环的话，两个指针最终肯定会相遇。

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	bool hasCycle(struct ListNode *head) {
	    if(!head || !head->next) { return false; }
	    struct ListNode *p = head->next, *q = head;
	    while(p){
	        if(!p->next) { return false; }
	        if(p == q) { return true; }
	        p = p->next;
	        if(p == q) { return true;}
	        p = p->next;
	        q = q->next;
	    }
	    return p;
	}