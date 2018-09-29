Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:  
Open brackets must be closed by the same type of brackets.  
Open brackets must be closed in the correct order.  
Note that an empty string is also considered valid.  

Example 1:
	
	Input: "()"
	Output: true

Example 2:
	
	Input: "()[]{}"
	Output: true

Example 3:
	
	Input: "(]"
	Output: false

Example 4:
	
	Input: "([)]"
	Output: false

Example 5:
	
	Input: "{[]}"
	Output: true

#注意点：
>1.本题很明显是使用栈进行运算。

>2.空字符串也认为是有效的。


	bool isValid(char* s) {
	    int len = strlen(s);
	    if(len == 0) { return true; }
	    char* stack = (char *)malloc(len * sizeof(char));
	    int j = -1;
	    for(int i = 0; i < len; i++){
	        switch(s[i]){
	            case '{':
	            case '[':
	            case '(':
	                stack[++j] = s[i];
	                break;
	            case '}':
	                if(stack[j] != '{') { return false; }
	                j--;    break;
	            case ']':
	                if(stack[j] != '[') { return false; }
	                j--;    break;
	            case ')':
	                if(stack[j] != '(') { return false; }
	                j--;    break;
	            default:    break;
	        }
	    }
	    return j == -1;
	}