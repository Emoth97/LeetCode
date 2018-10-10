Given a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

Note: Do not modify the linked list.

Follow up:
Can you solve it without using extra space?


#注意点：
>1.好题！
>
>2.首先还是使用快慢指针来判断是否有环
>
>3.假如有环，不妨设环的开始结点为第k个结点，相遇的位置为环上的第x个结点，n为环的长度。  
>&nbsp;&nbsp;&nbsp;相遇时慢指针移动了m = k + x + q * n步，快指针多移动了m = 2m - m = p * n步。  
>&nbsp;&nbsp;&nbsp;所以k + x = (p - q)n。所以环上的指针继续移动k个结点后，他们将在环的开始结点相遇。

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode *detectCycle(struct ListNode *head) {
	        struct ListNode *slow = head, *fast = head;
	        while (fast && fast->next) {
	            slow = slow->next;
	            fast = fast->next->next;
	            if (slow == fast) break;
	        }
	        if (!fast || !fast->next) return NULL;
	        slow = head;
	        while (slow != fast) {
	            slow = slow->next;
	            fast = fast->next;
	        }
	        return fast;
	}