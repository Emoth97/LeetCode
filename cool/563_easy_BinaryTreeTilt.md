Given a binary tree, return the tilt of the whole tree.

The tilt of a tree node is defined as the absolute difference between the sum of all left subtree node values and the sum of all right subtree node values. Null node has tilt 0.

The tilt of the whole tree is defined as the sum of all nodes' tilt.

Example:
	Input: 
	         1
	       /   \
	      2     3
	Output: 1
	Explanation: 
	Tilt of node 2 : 0
	Tilt of node 3 : 0
	Tilt of node 1 : |2-3| = 1
	Tilt of binary tree : 0 + 0 + 1 = 1

Note:

The sum of node values in any subtree won't exceed the range of 32-bit integer.  
All the tilt values won't exceed the range of 32-bit integer.

#注意点：
>1.用后序遍历来做，因为后序遍历的顺序是左-右-根，那么就会从叶结点开始处理，这样我们就能很方便的计算结点的累加和，同时也可以很容易的根据子树和来计算tilt。
	
	/**
	 * Definition for a binary tree node.
	 * struct TreeNode {
	 *     int val;
	 *     struct TreeNode *left;
	 *     struct TreeNode *right;
	 * };
	 */
	static int postorder(struct TreeNode* node, int *res) {
	    if (!node) return 0;
	    int leftSum = postorder(node->left, res);
	    int rightSum = postorder(node->right, res);
	    *res += abs(leftSum - rightSum);
	    return leftSum + rightSum + node->val;
	}
	
	int findTilt(struct TreeNode* root) {
	    int res = 0;
	    postorder(root, &res);
	    return res;
	}