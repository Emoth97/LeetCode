Sort a linked list using insertion sort.

![wiki插入排序图示](https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif)

A graphical example of insertion sort. The partial sorted list (black) initially contains only the first element in the list.
With each iteration one element (red) is removed from the input data and inserted in-place into the sorted list
 

Algorithm of Insertion Sort:

Insertion sort iterates, consuming one input element each repetition, and growing a sorted output list.
At each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list, and inserts it there.
It repeats until no input elements remain.

Example 1:
	
	Input: 4->2->1->3
	Output: 1->2->3->4

Example 2:
	
	Input: -1->5->3->4->0
	Output: -1->0->3->4->5

#注意点：
>1.简单的链表插入排序题。为了简便起见可以考虑增设头结点。
>
>2.插入前要先寻找最长有序前缀序列，可以避免大量的无谓对比。
>
>3.新的代码技巧：  
>&nbsp;&nbsp;&nbsp;为了避免在if(cur == NULL)中发生漏写一个等号而将比较语句写错为赋值语句的愚蠢行为，推荐使用 NULL == cur 这样的写法。

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode* insertionSortList(struct ListNode* head) {
	    if(NULL == head) { return head; }
	    struct ListNode *newhead = (struct ListNode *)malloc(sizeof(struct ListNode));
	    newhead->next = head;
	    struct ListNode *tail = head, *pre, *cur, *tmp;
	    while(NULL != tail->next && tail->next->val >= tail->val) { tail = tail->next; }
	    cur = tail->next;
	    while(NULL != cur) {
	        pre = newhead;
	        while(pre != tail && pre->next->val < cur->val) { pre = pre->next; }
	        if(pre->next == cur){ tail = cur; }
	        else {
	            tail->next = cur->next;
	            cur->next = pre->next;
	            pre->next = cur;
	        }
	        cur = tail->next;
	    }
	    return newhead->next;
	}