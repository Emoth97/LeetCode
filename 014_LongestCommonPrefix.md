Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

Example 1:

	Input: ["flower","flow","flight"]
	Output: "fl"

Example 2:
	
	Input: ["dog","racecar","car"]
	Output: ""
	Explanation: There is no common prefix among the input strings.

Note:

All given inputs are in lowercase letters `a`-`z`.

#注意点：
>1.返回时注意返回已经申请内存的char*或静态char数组，若返回普通char数组会在函数结束的时候释放导致返回空值。

>2.尽量使用malloc动态申请空间，而不是申请一大块静态空间。本题为了简单起见可以考虑直接申请长度为strs[0]长度的char型变量空间；还可以设置尾指针j指向最后一个相同的元素的相对位置，对比完成后直接申请长度为j的char型变量空间。

>3.记得最后一位赋值为尾零。

	char* longestCommonPrefix(char** strs, int strsSize) {
	    char *mytmpstring = (char *)malloc(strlen(strs[0]) * sizeof(char));
	    int i;
	    for(i = 0; strs[0][i]!='\0'; i++){
	        char p = strs[0][i];
	        for(int j = 1; j < strsSize; j++){
	            if(strs[j][i]!=p){
	                mytmpstring[i] = '\0';
	                return mytmpstring;
	            }
	        }
	        mytmpstring[i] = p;
	    }
	    mytmpstring[i] = '\0';
	    return mytmpstring;
	}