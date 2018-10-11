Sort a linked list in O(n log n) time using constant space complexity.

Example 1:
	
	Input: 4->2->1->3
	Output: 1->2->3->4
 
Example 2:
	
	Input: -1->5->3->4->0
	Output: -1->0->3->4->5

#注意点：
>1.第一种使用的方法有点投机，使用哈希表保存数据然后遍历哈希表。这种方法时间复杂度只与数据的范围有关，因此在本题的背景下是时间复杂度最优的算法，但空间复杂度要高一些。  
&nbsp;&nbsp;&nbsp;值得注意的是memset的使用，最后一个参数别忘了乘sizeof！
>
	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode* sortList(struct ListNode* head) {
	    struct ListNode *cur = head;
	    int min = 0, max = 0;
	    while(cur) {
	        max = max >= cur->val ? max : cur->val;
	        min = min < cur->val ? min : cur->val;
	        cur = cur->next;
	    }
	    int *hashtable = (int *)malloc(sizeof(int) * (max - min + 1));
	    memset(hashtable, 0, (max - min + 1) * sizeof(int));
	    cur = head;
	    while(cur) {
	        hashtable[cur->val - min]++;
	        cur = cur->next;
	    }
	    cur = head;
	    for(int i = 0; i < max - min + 1 && cur; ) {
	        if(hashtable[i] > 0){
	            hashtable[i]--;
	            cur->val = i + min;
	            cur = cur->next;
	        } else {
	            i++;
	        }
	    }
	    free(hashtable);
	    return head;
	}


>2.第二种是某大佬使用的希尔排序。思路是先将链表用数组表示，然后对数组使用希尔排序。


	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	int shellSort(int* arr, int n)
	{
	    for (int gap = n/2; gap > 0; gap /= 2)
	    {
	        for (int i = gap; i < n; i += 1)
	        {
	            int temp = arr[i];
	            int j;
	            for (j = i; j >= gap && arr[j - gap] > temp; j -= gap)
	                arr[j] = arr[j - gap];
	            arr[j] = temp;
	        }
	    }
	    return 0;
	}
	
	struct ListNode* sortList(struct ListNode* head) {
	    struct ListNode* ptr = head;
	    int count = 0;
	    while(ptr) {
	        count++;
	        ptr = ptr->next;
	    }
	    int* temp = malloc(count*sizeof(int));
	    ptr = head;
	    count = 0;
	    while(ptr) {
	        temp[count] = ptr->val;
	        count++;
	        ptr = ptr->next;
	    }
	    shellSort(temp,count);
	    ptr = head;
	    for (int i = 0; i < count; i++) {
	        ptr->val = temp[i];
	        ptr = ptr->next;
	    }
	    return head;
	}

>3.第三种是速度稍慢的归并排序。使用快慢指针将链表划分为两部分，然后对两部分排序再归并。下面的解法运用了多次递归。
>
	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	void splitHalf(struct ListNode* source, struct ListNode** first, struct ListNode** second) {
	    struct ListNode* slow = source;
	    struct ListNode* fast = source->next;
	    while (fast != NULL) {
	        fast = fast->next;
	        if (fast != NULL) {
	            slow = slow->next;
	            fast = fast->next;
	        }
	    }
	    *first = source;
	    *second = slow->next;
	    slow->next = NULL;
	}
	
	struct ListNode* mergesort(struct ListNode* first, struct ListNode* second) {
	    if (first == NULL) return second;
	    if (second == NULL) return first;
	    if (first->val <= second->val) {
	        first->next = mergesort(first->next, second);
	        return first;
	    } else {
	        second->next = mergesort(first, second->next);
	        return second;
	    }
	}
	
	struct ListNode* sortList(struct ListNode* head) {
	    if (head == NULL || head->next == NULL) {
	        return head;
	    }
	    struct ListNode* first;
	    struct ListNode* second;
	    splitHalf(head, &first, &second);
	    first = sortList(first);
	    second = sortList(second);
	    
	    return mergesort(first, second);
	}


