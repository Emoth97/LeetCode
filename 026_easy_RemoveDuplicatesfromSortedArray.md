Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Example 1:
	
	Given nums = [1,1,2],
	
	Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
	
	It doesn't matter what you leave beyond the returned length.

Example 2:

	Given nums = [0,0,1,1,1,2,2,3,3,4],
	
	Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.
	
	It doesn't matter what values are set beyond the returned length.

Clarification:

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by reference, which means modification to the input array will be known to the caller as well.

Internally you can think of this:

	// nums is passed in by reference. (i.e., without making a copy)
	int len = removeDuplicates(nums);
	
	// any modification to nums in your function would be known by the caller.
	// using the length returned by your function, it prints the first len elements.
	for (int i = 0; i < len; i++) {
	    print(nums[i]);
	}


#注意点：
>1.此题要求只能申请O(1)的存储空间，也就是说使用另外一个数组保存该数组是行不通的。 

>2.可以考虑设置两个指针i和j分别指向当前遍历的位置和当前非重复的最后一个元素下标。如果j指向的元素与i指向的元素不同，则说明i指向的是新的元素，j做+1运算并置j运算后指向的数为i指向的数。

>3.返回时注意考虑j为下标，j+1才是长度。

	int removeDuplicates(int* nums, int numsSize) {
	    if(numsSize == 0) { return 0; }
	    else if(numsSize == 1) { return 1; }
	    int i = 1, j = 0;
	    for(; i <numsSize; i++){
	        if(nums[i] != nums[j]) { nums[++j] = nums[i]; }
	    }
	    return ++j;
	}