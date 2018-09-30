Reverse a singly linked list.

Example:
	
	Input: 1->2->3->4->5->NULL
	Output: 5->4->3->2->1->NULL

Follow up:

A linked list can be reversed either iteratively or recursively. Could you implement both?

#注意点：
>1.非递归可以考虑使用头插法建立新的链表，占用O(n)的空间  
>2.非递归也可以考虑对于每一次循环都颠倒当前和之前的位置，需要一个tmp辅助指针，占用O(1)的空间  
>3.对于递归，定义辅助指针p指向head后一个位置。首先需要遍历到链表末尾，使head指向末尾元素，p指向head后一个元素（即NULL），此时newhead即为新的头节点。然后依次修改p指向head。



递归

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode* reverseListRe(struct ListNode* head) {
		if(head == NULL || head->next == NULL) return head;
		struct ListNode *p=head->next;
		head->next=NULL;
		struct ListNode *newhead=reverseListRe(p);
		p->next=head;
		return newhead;
	}

非递归

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode* reverseList(struct ListNode* head) {
	    struct ListNode *res, *tmp, *l = head;
	    res = NULL;
	    while(l){
	        tmp = l;
	        l = l->next;
	        tmp->next = res;
	        res = tmp;
	    }
	    return res;
	}