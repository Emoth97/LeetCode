Suppose Andy and Doris want to choose a restaurant for dinner, and they both have a list of favorite restaurants represented by strings.

You need to help them find out their common interest with the least list index sum. If there is a choice tie between answers, output all of them with no order requirement. You could assume there always exists an answer.

Example 1:

	Input:
	["Shogun", "Tapioca Express", "Burger King", "KFC"]
	["Piatti", "The Grill at Torrey Pines", "Hungry Hunter Steakhouse", "Shogun"]
	Output: ["Shogun"]
	Explanation: The only restaurant they both like is "Shogun".

Example 2:
	Input:
	["Shogun", "Tapioca Express", "Burger King", "KFC"]
	["KFC", "Shogun", "Burger King"]
	Output: ["Shogun"]
	Explanation: The restaurant they both like and have the least index sum is "Shogun" with index sum 1 (0+1).

Note:
>1.The length of both lists will be in the range of [1, 1000].  
>2.The length of strings in both lists will be in the range of [1, 30].  
>3.The index is starting from 0 to the list length minus 1.  
>4.No duplicates in both lists.

#注意点：
>1.这道题是简单的字符串比对题，需要注意的是类似于KMP的思路：假设当list1[i1]与list2[i2]相等时，len = i1 + i2。此时对于下一个i1，不需要再比较i2 > len - i1之后的字符串。（因为即使字符串相同，索引之和也不为最小值）  
>2.为了获得最大效率，需要重写字符串对比函数和字符串拷贝函数。（不需要考虑太多边界值，因为本题的输入很人性化，避免了大量的边界检测）  
>3.其余的beat 100%的解答都进行了自定义哈希表的算法，个人感觉在这种小题中没有必要使用，在笔试或机试时没有那么多时间或空间用来编写哈希表。

	/**
	 * Return an array of size *returnSize.
	 * Note: The returned array must be malloced, assume caller calls free().
	 */
	static bool emothstrcmp(const char *s1, char *s2) {
	    int i = 0;
	    for(; s1[i] != '\0'; i++){
	        if(s1[i] != s2[i]) {
	            return false;
	        }
	    }
	    return s2[i] == '\0';
	}
	
	static void emothstrcpy(char *s1, const char *s2) {
	    int i = 0;
	    for(; s2[i] != '\0'; i++){
	        s1[i] = s2[i];
	    }
	    s1[i] = '\0';
	}
	
	char** findRestaurant(char** list1, int list1Size, char** list2, int list2Size, int* returnSize) {
	    int i1, i2, len = list1Size + list2Size - 2, ip = 0;
	    char **p = (char **)malloc(sizeof(char *) * list1Size);
	    for(i1 = 0; i1 <= len && i1 < list1Size; i1++) {
	        for(i2 = 0; i1 + i2 <= len && i2 < list2Size; i2++) {
	            if(emothstrcmp(list1[i1], list2[i2])) {
	                if(i1 + i2 == len) {
	                    p[ip] = (char *)malloc(sizeof(char *) * 30);
	                    emothstrcpy(p[ip], list1[i1]);
	                    ip++;
	                } else if(i1 + i2 < len) { 
	                    p[ip] = (char *)malloc(sizeof(char *) * 30);
	                    len = i1 + i2;
	                    emothstrcpy(p[0], list1[i1]);
	                    ip = 1;
	                }
	            }
	        }
	    }
	    *returnSize = ip;
	    return p;
	}