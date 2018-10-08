We are given `head`, the head node of a linked list containing unique integer values.

We are also given the list `G`, a subset of the values in the linked list.

Return the number of connected components in `G`, where two values are connected if they appear consecutively in the linked list.

Example 1:
	
	Input: 
	head: 0->1->2->3
	G = [0, 1, 3]
	Output: 2
	Explanation: 
	0 and 1 are connected, so [0, 1] and [3] are the two connected components.

Example 2:
	
	Input: 
	head: 0->1->2->3->4
	G = [0, 3, 1, 4]
	Output: 2
	Explanation: 
	0 and 1 are connected, 3 and 4 are connected, so [0, 1] and [3, 4] are the two connected components.

Note:

>1.If N is the length of the linked list given by head, 1 <= N <= 10000.  
>2.The value of each node in the linked list will be in the range [0, N - 1].  
>3.1 <= G.length <= 10000.  
>4.G is a subset of all values in the linked list.  

#注意点：
>1.使用哈希表存储G中的值，挨个对比
>
>2.做题时遇到的一个严重的错误在于数组初始化时，若没有令int hashtable[10000] = { 0 }，则hashtable中的数是随机的，这样在判断hashtable[head->val]时遇到了惨烈的错误。  数组通用赋初值 { 0 }。

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	int numComponents(struct ListNode* head, int* G, int GSize) {
	    int num = 0;
	    bool hashtable[10000] = { 0 };
	    for(int i = 0; i < GSize; i++){ hashtable[G[i]] = true; }
	    while(head){
	        if(hashtable[head->val]){
	            num++;
	            while(head->next && hashtable[head->next->val]) {
	                head = head->next; 
	            }
	        }
	        head = head->next;
	    }
	    return num;
	}