Write a program to find the node at which the intersection of two singly linked lists begins.


For example, the following two linked lists:

	A:          a1 → a2
	                   ↘
	                     c1 → c2 → c3
	                   ↗            
	B:     b1 → b2 → b3

begin to intersect at node c1.


Notes:

>If the two linked lists have no intersection at all, return `null``.
>
>The linked lists must retain their original structure after the function returns.
>
>You may assume there are no cycles anywhere in the entire linked structure.
>
>Your code should preferably run in O(n) time and use only O(1) memory.

#注意点：
>1.本题一开始想的是建立类似于哈希表的存储结构，大小为65536。存在的问题一是空间复杂度虽然为O(1)，但太大而且不能确定这个大小是否足够，二是时间复杂度仍然未能达到最优。
>
>2.如果两个链长度相同的话，那么对应一个个比下去就能找到，所以只需要把长链表变短即可。
>
>具体算法为：分别遍历两个链表，得到分别对应的长度。然后求长度的差值，把较长的那个链表向后移动这个差值的个数，然后一一比较即可。
>
>3.这道题还有一种特别巧妙的方法，虽然题目中强调了链表中不存在环，但是我们可以用环的思想来做，我们让两条链表分别从各自的开头开始往后遍历，当其中一条遍历到末尾时，我们跳到另一个条链表的开头继续遍历。两个指针最终会相等，而且只有两种情况，一种情况是在交点处相遇，另一种情况是在各自的末尾的空节点处相等。为什么一定会相等呢，因为两个指针走过的路程相同，是两个链表的长度之和，所以一定会相等。这个思路真的很巧妙，而且更重要的是代码写起来特别的简洁。
>
>图解：

	A:          a1 → a2
	                   ↘
	                     c1 → c2 → c3
	                   ↗            
	B:     b1 → b2 → b3

	对于 *a 路线为 a1->a2->c1->c2->c3->b1->b2->b3-> c1 ->c2->c3->NULL
	对于 *b 路线为 b1->b2->b3->c1->c2->c3->a1->a2-> c1 ->c2->c3->NULL

#代码

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode *getIntersectionNode(struct ListNode *headA, struct ListNode *headB) {
	    if(!headA || !headB) { return NULL; }
	    struct ListNode *a = headA, *b = headB;
	    while(a != b){
	        a = a ? a->next : headB;
	        b = b ? b->next : headA;
	    }
	    return a;
	}