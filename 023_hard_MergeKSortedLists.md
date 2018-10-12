Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

Example:

Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6

#注意点：
>1.多路归并排序，只需二分归并到最后即可。
>
>2.注意输入为空时的情况，即**lists为NULL，此时若返回lists[0]会报错（因为没有该指针），所以要加判断listsSize的语句。


	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode* mergeTwoLists(struct ListNode *l1, struct ListNode *l2) {
	    struct ListNode *l = (struct ListNode *)malloc(sizeof(struct ListNode)), *tmp = l;
	    while(NULL != l1 && NULL != l2) {
	        if(l1->val < l2->val) { 
	            l->next = l1; 
	            l1 = l1->next;
	            l = l->next;
	        } else {
	            l->next = l2;
	            l2 = l2->next;
	            l = l->next;
	        }
	    }
	    l->next = NULL != l1 ? l1 : l2;
	    l = tmp->next;
	    free(tmp);
	    return l;
	}
	struct ListNode* mergeKLists(struct ListNode** lists, int listsSize) {
	    if(!listsSize) { return NULL; }
	    for(; listsSize/2 > 0; listsSize = listsSize / 2 + listsSize % 2) {
	        for(int i = 0; i < listsSize/2; i++) { 
	            lists[i] = mergeTwoLists(lists[i], lists[listsSize - i - 1]);
	        }
	    }
	    return lists[0];
	}