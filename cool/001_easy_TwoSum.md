Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

	Given nums = [2, 7, 11, 15], target = 9,
	
	Because nums[0] + nums[1] = 2 + 7 = 9,
	return [0, 1].

#注意点：
>1.新写函数设置为静态，使用时当前函数内只进行边界判断、调用该函数。 

>2.函数的参数若为指针，设置为const可以避免函数内部通过该指针修改该指针指向的内容。（但若将其保存的地址赋给另一个不为const的指针，仍然可以修改指针） 

>3.<stdlib.h>中qsort快速排序，参数分别为：
>>void* 待排序数组首地址  
>>size\_t  数组中待排序元素数量  
>>size_t  数组中各元素占用空间大小  
>>int(*)(const void*, const void*)  指向函数的指针，用于确定排序的顺序 

>4.两边分设指针，同时开始查找

	/**
	 * Note: The returned array must be malloced, assume caller calls free().
	 */
	#include <stdlib.h>
	
	static int cmpnumidx(const void *a, const void *b)
	{
	    int ia = *(int*)a;
	    int ib = *(int*)b;
	    return ia - ib;
	}
	
	static int *__myTwoSum(const int* nums, int numsSize, int target);
	
	int* twoSum(int* nums, int numsSize, int target)
	{
	    if (numsSize < 2) {
	        return NULL;
	    }
	    return __myTwoSum(nums, numsSize, target);
	}
	
	static int* __myTwoSum(const int* a, int n, int t)
	{
	    int *ret;
	    int *numidx;
	    int i;
	    int j;
	    int r1;
	    int r2;
	    numidx = (int *)malloc(sizeof(int) * 2 * n);
	    for (i = 0; i < n; ++ i) {
	        numidx[i * 2] = a[i];
	        numidx[i * 2 + 1] = i;
	    }
	    qsort(numidx, n, sizeof(int) * 2, cmpnumidx);
	    i = 0;
	    j = n - 1;
	    while (i < j) {
	        int p = numidx[i * 2];
	        int q = numidx[j * 2];
	        int s = p + q;
	        if (s == t) {
	            break;
	        } else if (s > t) {
	            j --;
	        } else {
	            i ++;
	        }
	    }
	    r1 = numidx[i * 2 + 1];
	    r2 = numidx[j * 2 + 1];
	    free(numidx);
	    ret = malloc(sizeof(int) * 2);
	    if (r1 > r2) {
	        int tr = r1;
	        r1 = r2;
	        r2 = tr;
	    }
	    ret[0] = r1;
	    ret[1] = r2;
	    return ret;
	}
