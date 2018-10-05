Given a singly linked list, determine if it is a palindrome.

Example 1:
	
	Input: 1->2
	Output: false

Example 2:
	
	Input: 1->2->2->1
	Output: true

Follow up:
Could you do it in O(n) time and O(1) space?


#注意点：
>1.用快慢指针遍历，快指针每次走两步，慢指针每次走一步。快指针走到尾时慢指针为中间。
>
>2.快慢指针的判断是难点。
>
>3.慢指针在开始把遍历到的内容存到栈中，快指针到头时开始出栈。


	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	bool isPalindrome(struct ListNode* head) {
	    int nums[65536] = {}, i = 0;
	    if(!head || !head->next) { return true;}
	    struct ListNode *fast = head, *slow = head;
	    while(fast->next) {
	        fast = fast->next;
	        nums[++i] = slow->val;
	        if(fast->next) {
	            fast = fast->next;
	            slow = slow->next;
	        }
	    }
	    if(slow->next) { slow = slow->next; }
	    while(slow){
	        if(nums[i] != slow->val) { return false; }
	        i--;
	        slow = slow->next;
	    }
	    return !i;
	}

