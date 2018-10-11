Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

Example 1:
	
	Input: 1->2->3->3->4->4->5
	Output: 1->2->5

Example 2:
	 
	Input: 1->1->1->2->3
	Output: 2->3

#注意点：
>1.方便起见，还是增设一个头结点，简化判断逻辑。
>
>2.由于这道题是要删除重复的所有结点而不是保留一个，所以我们令游标结点指向被判断结点的前驱。这样删除的时候只需修改游标结点的next并释放重复结点的空间就可以了。
>
>3.最后别忘记释放增设头结点的空间。
	
	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode* deleteDuplicates(struct ListNode* head) {
	    struct ListNode *newhead = (struct ListNode *)malloc(sizeof(struct ListNode)), *cur = newhead, *tmp1, *tmp2;
	    newhead->next = head;
	    int val;
	    while(cur->next) {
	        val = cur->next->val;
	        tmp1 = cur->next->next;
	        if(tmp1 && tmp1->val == val) {
	            free(cur->next);
	            tmp2 = tmp1->next;
	            free(tmp1);
	            while(tmp2 && tmp2->val == val) {
	                tmp1 = tmp2;
	                tmp2 = tmp1->next;
	                free(tmp1);
	            }
	            cur->next = tmp2;
	        } else {
	            cur = cur->next;
	        }
	    }
	    cur = newhead->next;
	    free(newhead);
	    return cur;
	}