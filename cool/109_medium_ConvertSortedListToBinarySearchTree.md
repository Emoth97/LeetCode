Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

Example:

	Given the sorted linked list: [-10,-3,0,5,9],
	
	One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:
	
	      0
	     / \
	   -3   9
	   /   /
	 -10  5


#注意点：
>1.这道题实质上是考二分查找的。对于链表使用快慢指针查找中值，中值即为根节点，从中值分为两部分，左边链表即为左子树，右边链表即为右子树。递归计算即可。


	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	/**
	 * Definition for a binary tree node.
	 * struct TreeNode {
	 *     int val;
	 *     struct TreeNode *left;
	 *     struct TreeNode *right;
	 * };
	 */
	struct TreeNode* sortedListToBST(struct ListNode* head) {
	    if(NULL == head) { return NULL; }
	    if(NULL == head->next ) {
	        struct TreeNode *tree = (struct TreeNode *)malloc(sizeof(struct TreeNode));
	        tree->val = head->val;
	        tree->left = NULL;
	        tree->right = NULL;
	        return tree;
	    }
	    struct ListNode *fast = head, *slow = head, *last = slow;
	    while(fast->next && fast->next->next) {
	        last = slow;
	        fast = fast->next->next;
	        slow = slow->next;
	    }
	    fast = slow->next;
	    last->next = NULL;
	    struct TreeNode *tree = (struct TreeNode *)malloc(sizeof(struct TreeNode));
	    tree->val = slow->val;
	    if (head != slow) { tree->left = sortedListToBST(head); }
	    else { tree->left = NULL; }
	    tree->right = sortedListToBST(fast);
	    return tree;
	}