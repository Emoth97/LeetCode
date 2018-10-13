Given a singly linked list, return a random node's value from the linked list. Each node must have the same probability of being chosen.

Follow up:
What if the linked list is extremely large and its length is unknown to you? Could you solve this efficiently without using extra space?

Example:

	// Init a singly linked list [1,2,3].
	ListNode head = new ListNode(1);
	head.next = new ListNode(2);
	head.next.next = new ListNode(3);
	Solution solution = new Solution(head);
	
	// getRandom() should return either 1, 2, or 3 randomly. Each element should have equal probability of returning.
	solution.getRandom();

#注意点：
>1.从链表中取随机值，要注意不能用srand，否则结果会与比对的值不同。
>
>2.有一种更快的解法是定义了两个ListNode*，分别指向头部和中部。这种方法在查找时要比一般的从头查找更快。
	
	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	typedef struct Solution{
	    struct ListNode *head, *mid;
	    int len;
	} Solution;
	
	/** @param head The linked list's head.
	        Note that the head is guaranteed to be not null, so it contains at least one node. */
	Solution* solutionCreate(struct ListNode* head) {
	    struct Solution *solution = (struct Solution *)malloc(sizeof(struct Solution));
	    solution->head = head;
	    solution->mid = head;
	    solution->len = 0;
	    while(head && head->next) {
	        solution->mid = solution->mid->next;
	        head = head->next->next;
	        solution->len += 2;
	    }
	    if(head) { solution->len++; }
	    return solution;
	}
	
	/** Returns a random node's value. */
	int solutionGetRandom(Solution* obj) {
	    int num = rand() % obj->len;
	    struct ListNode *tmp = obj->head;
	    if(num >= obj->len/2) {
	        num -= obj->len/2;
	        tmp = obj->mid;
	    }
	    while(num--){ tmp = tmp->next; }
	    return tmp->val;
	}
	
	void solutionFree(Solution* obj) {
	    free(obj);
	}
	
	/**
	 * Your Solution struct will be instantiated and called as such:
	 * struct Solution* obj = solutionCreate(head);
	 * int param_1 = solutionGetRandom(obj);
	 * solutionFree(obj);
	 */