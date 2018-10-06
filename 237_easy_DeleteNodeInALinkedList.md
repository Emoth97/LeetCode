Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

Given linked list -- head = [4,5,1,9], which looks like following:

    4 -> 5 -> 1 -> 9

Example 1:

	Input: head = [4,5,1,9], node = 5
	Output: [4,1,9]
	Explanation: You are given the second node with value 5, the linked list
	             should become 4 -> 1 -> 9 after calling your function.

Example 2:
	
	Input: head = [4,5,1,9], node = 1
	Output: [4,5,9]
	Explanation: You are given the third node with value 1, the linked list
	             should become 4 -> 5 -> 9 after calling your function.

Note:

>The linked list will have at least two elements.  
>All of the nodes' values will be unique.  
>The given node will not be the tail and it will always be a valid node of the linked list.  
>Do not return anything from your function.

#注意点：
>1.与之前的题目不同，这道题只给出了要删除的结点。因此可以考虑用next结点的值覆盖该结点，并释放next（因为node也指向next）

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	void deleteNode(struct ListNode *node) {
	    struct ListNode *p = node->next;
	    node->val = p->val;
	    node->next = p->next;
	    free(p);
	}