Given a (singly) linked list with head node `root`, write a function to split the linked list into `k` consecutive linked list "parts".

The length of each part should be as equal as possible: no two parts should have a size differing by more than 1. This may lead to some parts being null.

The parts should be in order of occurrence in the input list, and parts occurring earlier should always have a size greater than or equal parts occurring later.

Return a List of ListNode's representing the linked list parts that are formed.

Examples 1->2->3->4, k = 5 // 5 equal parts [ [1], [2], [3], [4], null ]

Example 1:

	Input: 
	root = [1, 2, 3], k = 5
	Output: [[1],[2],[3],[],[]]
	Explanation:
	The input and each element of the output are ListNodes, not arrays.
	For example, the input root has root.val = 1, root.next.val = 2, \root.next.next.val = 3, and root.next.next.next = null.
	The first element output[0] has output[0].val = 1, output[0].next = null.
	The last element output[4] is null, but it's string representation as a ListNode is [].

Example 2:

	Input: 
	root = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], k = 3
	Output: [[1, 2, 3, 4], [5, 6, 7], [8, 9, 10]]
	Explanation:
	The input has been split into consecutive parts with size difference at most 1, and earlier parts are a larger size than the later parts.

Note:

>The length of `root` will be in the range `[0, 1000]`.  
>Each value of a node in the input will be an integer in the range `[0, 999]`.  
>`k` will be an integer in the range `[1, 50]`.

#注意点：
>1.注意审题和观察参数。  
>&nbsp;&nbsp;&nbsp;这道题有点坑，要注意到参数除了头结点、组数k以外还有个*returnSize。因为没注意到有returnSize这个参数导致输出一直为空。
>
>2.思路:先遍历一遍得到链表长度。通过链表长度和组数计算出每一组的长度以及长度要+1的组的个数。然后再遍历一次链表依次将结果写入结果数组中。
	
	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	/**
	 * Return an array of size *returnSize.
	 * Note: The returned array must be malloced, assume caller calls free().
	 */
	struct ListNode** splitListToParts(struct ListNode* root, int k, int* returnSize) {
	    struct ListNode *cur = root;
	    int len = 0;
	    for(; NULL != cur; len++, cur = cur->next);
	    cur = root;
	    int aver = len / k, more = len % k;
	    struct ListNode **parts = (struct ListNode **)malloc(k * sizeof(struct ListNode *)), *tmp;
	    for(int i = 0; i < k; i++) {
	        if(NULL == cur) { parts[i] = NULL; continue; }
	        parts[i] = cur;
	        if(0 < aver) {
	            for(int j = 1; j < aver; j++) { cur = cur->next; }
	            if(aver && i < more) { cur = cur->next; }
	        }
	        tmp = cur;
	        cur = cur->next;
	        tmp->next = NULL;
	    }
	    *returnSize = k;
	    return parts;
	}