Given a binary tree, flatten it to a linked list in-place.

For example, given the following tree:

	    1
	   / \
	  2   5
	 / \   \
	3   4   6
The flattened tree should look like:

	1
	 \
	  2
	   \
	    3
	     \
	      4
	       \
	        5
	         \
	          6

#注意点：
>1.好题！
>
>2.这道题看输出是类似于二叉树的先序遍历的，所以考虑采用类似二叉树先序遍历的方法做。
>
>3.由于题目的函数只有一个输入，只有一个输入进行递归运算难度太大，所以重新写一个函数，不妨命名为recurse，输入为要进行运算的结点和该节点的下一个next节点。  
>（1）考虑下图这种情况（左右子树均不为空），输入为1和next。此时的操作是：  
>&nbsp;&nbsp;&nbsp;①1的右指针指向1的左子树（即以2为头结点的左子树）。  
>&nbsp;&nbsp;&nbsp;②对2进行递归调用recurse。对2的next节点为1的原始右节点5。  
>&nbsp;&nbsp;&nbsp;③对3进行递归调用recurse。对5的next节点为1的原始next节点。  
>&nbsp;&nbsp;&nbsp;④1的左指针置空。  
>
	    1
	   / \
	  2   5
>
>（2）考虑下图这种情况（左子树不为空，右子树为空），输入为2和next。此时的操作是：  
>&nbsp;&nbsp;&nbsp;①2的右指针指向2的左子树（即以3为头结点的左子树）。  
>&nbsp;&nbsp;&nbsp;②对3进行递归调用recurse。对3的next节点为2的原始next节点。  
>&nbsp;&nbsp;&nbsp;③1的左指针置空
>
      2
	 /
	3
>
>（3）考虑下图这种情况（左子树为空，右子树不为空），输入为5和next。此时的操作是：
>&nbsp;&nbsp;&nbsp;①对6进行递归调用recurse。对6的next节点为5的原始next节点。  
>&nbsp;&nbsp;&nbsp;②5的左指针置空（本步可选，因为5的左指针本来就是NULL）
>
	5
	 \
	  6
>
>（4）考虑下图这种情况（左右子树均为控），输入为6和next。此时的操作是：
>nbsp;&nbsp;&nbsp;①6的右指针指向next。
>nbsp;&nbsp;&nbsp;②6的左指针置空（本步可选，因为6的左指针本来就是NULL）
>
	6	
>
>4.由此可以看出这道题非常适合使用递归算法求解。下方代码分别是原始递归代码和精简后的代码。


	
	/**
	 * Definition for a binary tree node.
	 * struct TreeNode {
	 *     int val;
	 *     struct TreeNode *left;
	 *     struct TreeNode *right;
	 * };
	 */
	static void recurse_original(struct TreeNode* root, struct TreeNode *next) {
	    struct TreeNode *tmp;
	    if(root->left && root->right) {
	        tmp = root->right;
	        root->right = root->left;
	        recurse_original(root->right, tmp);
	        recurse_original(tmp, next);
	        root->left = NULL;
	    } else if(root->left && !root->right) {
	        root->right = root->left;
	        recurse_original(root->right, next);
	        root->left = NULL;
	    } else if(!root->left && root->right) {
	        recurse_original(root->right, next);
	    } else {
	        root->right = next;
	    }
	}
	static void recurse(struct TreeNode* root, struct TreeNode *next) {
	    struct TreeNode *tmp = root->right ? root->right : next;
	    if(root->left) { 
	        recurse(root->left, tmp);
	        root->right = root->left;
	    }
	    if(next != tmp) { recurse(tmp ,next); } 
	    else if(next && !root->left) { root->right = next; }
	    root->left = NULL;
	}
	void flatten(struct TreeNode* root) {
	    if(root){ recurse(root, NULL); }
	}