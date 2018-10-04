Design your implementation of the linked list. You can choose to use the singly linked list or the doubly linked list. A node in a singly linked list should have two attributes: `val` and `next`. `val` is the value of the current node, and `next` is a pointer/reference to the next node. If you want to use the doubly linked list, you will need one more attribute `prev` to indicate the previous node in the linked list. Assume all nodes in the linked list are 0-indexed.

Implement these functions in your linked list class:

>get(index) : Get the value of the `index`-th node in the linked list. If the index is invalid, return `-1`.
>
>addAtHead(val) : Add a node of value `val` before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
>
>addAtTail(val) : Append a node of value `val` to the last element of the linked list.
>
>addAtIndex(index, val) : Add a node of value `val` before the `index`-th node in the linked list. If `index` equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted.
>
>deleteAtIndex(index) : Delete the `index`-th node in the linked list, if the index is valid.

Example:

	MyLinkedList linkedList = new MyLinkedList();
	linkedList.addAtHead(1);
	linkedList.addAtTail(3);
	linkedList.addAtIndex(1, 2);  // linked list becomes 1->2->3
	linkedList.get(1);            // returns 2
	linkedList.deleteAtIndex(1);  // now the linked list is 1->3
	linkedList.get(1);            // returns 3

Note:

>All values will be in the range of `[1, 1000]`.
>
>The number of operations will be in the range of `[1, 1000]`.
>
>Please do not use the built-in LinkedList library.

#注意点：
>1.设计链表，使用带头结点的链表比不带头结点的单链表更简单。
>
>2.运行速度最快的方法是另设一个struct保存头结点指针和尾结点指针。个人感觉没有必要。
>
>3.记得要判断所有指针为空的情况，不然会报错。

	
	typedef struct MyLinkedList{
	    int val;
	    struct MyLinkedList *next;
	} MyLinkedList;
	
	/** Initialize your data structure here. */
	MyLinkedList* myLinkedListCreate() {
	    struct MyLinkedList *head = (struct MyLinkedList *)malloc(sizeof(MyLinkedList));
	    head->next = NULL;
	    return head;
	}
	
	/** Get the value of the index-th node in the linked list. If the index is invalid, return -1. */
	int myLinkedListGet(MyLinkedList* obj, int index) {
	    for(; index >= 0; index--){
	        if(obj->next){
	            obj = obj->next;
	        } else {
	            return -1;
	        }
	    }
	    return obj->val;
	}
	
	/** Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list. */
	void myLinkedListAddAtHead(MyLinkedList* obj, int val) {
	    struct MyLinkedList *p = (struct MyLinkedList *)malloc(sizeof(MyLinkedList));
	    p->next = obj->next;
	    p->val = val;
	    obj->next = p;
	}
	
	/** Append a node of value val to the last element of the linked list. */
	void myLinkedListAddAtTail(MyLinkedList* obj, int val) {
	    while(obj->next) { obj = obj->next; }
	    struct MyLinkedList *p = (struct MyLinkedList *)malloc(sizeof(MyLinkedList));
	    p->next = NULL;
	    p->val = val;
	    obj->next = p;
	}
	
	/** Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted. */
	void myLinkedListAddAtIndex(MyLinkedList* obj, int index, int val) {
	    for(; index > 0; index--){
	        if(obj->next){
	            obj = obj->next;
	        } else {
	            return;
	        }
	    }   
	    struct MyLinkedList *p = (struct MyLinkedList *)malloc(sizeof(MyLinkedList));
	    p->val = val;
	    p->next = obj->next;
	    obj->next = p;    
	}
	
	/** Delete the index-th node in the linked list, if the index is valid. */
	void myLinkedListDeleteAtIndex(MyLinkedList* obj, int index) {
	    for(; index > 0; index--){
	        if(obj->next){
	            obj = obj->next;
	        } else {
	            return;
	        }
	    }
	    if(obj->next) {
	        struct MyLinkedList *p = obj->next;
	        obj->next = p->next;
	        free(p);
	    }
	}
	
	void myLinkedListFree(MyLinkedList* obj) {
	    while(obj->next){
	        struct myLinkedList *p = obj;
	        obj = obj->next;
	        free(p);
	    }
	    free(obj);
	}
	
	/**
	 * Your MyLinkedList struct will be instantiated and called as such:
	 * struct MyLinkedList* obj = myLinkedListCreate();
	 * int param_1 = myLinkedListGet(obj, index);
	 * myLinkedListAddAtHead(obj, val);
	 * myLinkedListAddAtTail(obj, val);
	 * myLinkedListAddAtIndex(obj, index, val);
	 * myLinkedListDeleteAtIndex(obj, index);
	 * myLinkedListFree(obj);
	 */