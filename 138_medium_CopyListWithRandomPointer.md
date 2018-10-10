A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

#注意点：
>1.难点在于random指针的处理。考虑使用哈希表存储。
>
>2.彩蛋：经过多次运算，得出若哈希函数为h(x)=x，哈希表大小最少要开到20099。

	/**
	 * Definition for singly-linked list with a random pointer.
	 * struct RandomListNode {
	 *     int label;
	 *     struct RandomListNode *next;
	 *     struct RandomListNode *random;
	 * };
	 */
	struct RandomListNode *copyRandomList(struct RandomListNode *head) {
	    struct RandomListNode *newhead = (struct RandomListNode *)malloc(sizeof(struct RandomListNode)), *cur = head, *curnew = newhead;
	    struct RandomListNode *hashtable[20099];
	    while(NULL != cur) {
	        curnew->next = (struct RandomListNode *)malloc(sizeof(struct RandomListNode));
	        curnew = curnew->next;
	        curnew->label = cur->label;
	        hashtable[curnew->label + 10049] = curnew;
	        cur = cur->next;
	    }
	    curnew->next = NULL;
	    curnew = newhead->next;
	    cur = head;
	    while(NULL != curnew) {
	        if(NULL == cur->random) { curnew->random = NULL; }
	        else { curnew->random = hashtable[cur->random->label + 10049];}
	        cur = cur->next;
	        curnew = curnew->next;
	    }
	    curnew = newhead->next;
	    free(newhead);
	    return curnew;
	}

>3.在查看别人的submission时发现了一个神奇的解法：  
>（1）先将每个结点复制一遍，将复制结点作为当前结点的后继插入链表中  
>（2）复制random指针。复制结点的random结点即为原结点的random结点的next结点。  
>（3）剥离复制结点。即恢复原始结点和复制结点的next指针。  
>讲真，这个方法真的是太妙了！  
>代码如下：

	/**
	 * Definition for singly-linked list with a random pointer.
	 * struct RandomListNode {
	 *     int label;
	 *     struct RandomListNode *next;
	 *     struct RandomListNode *random;
	 * };
	 */
	  
	struct RandomListNode *copyRandomList(struct RandomListNode *head) {
	    struct RandomListNode* temp_original = head, *temp_new = NULL;
	    struct RandomListNode* head_new = NULL;
	
	    if(!head) return NULL;
	
	    while(temp_original != NULL) {
	        temp_new = (struct RandomListNode*) malloc(sizeof(struct RandomListNode));
	        temp_new->label = temp_original->label;
	        temp_new->next = temp_original->next;
	        temp_new->random = temp_original->random;
	        temp_original->next = temp_new;
	        temp_original = temp_new->next;
	    }
	
	    temp_original = head;
	    head_new = head->next;
	    temp_new = head_new;
	
	    while(temp_new != NULL) {
	    	if (temp_new->random)
	    		temp_new->random = temp_new->random->next;
	        if (temp_new->next == NULL)
	        	break;
	        temp_new = temp_new->next->next;
	    }
	    temp_new = head_new;
	
	    while (temp_original != NULL) {
	        temp_original->next = temp_new->next;
	        if(temp_original->next == NULL) break;
	        temp_new->next = temp_original->next->next;
	        temp_original = temp_original->next;
	        temp_new = temp_new->next;
	    }
	
	    return head_new;
	}