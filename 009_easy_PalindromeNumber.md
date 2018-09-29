Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

Example 1:

	Input: 121
	Output: true

Example 2:

	Input: -121
	Output: false
	Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.

Example 3:

	Input: 10
	Output: false
	Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
Follow up:

Could you solve it without converting the integer to a string?

#注意点：
>1.负数的回文数结尾为-，所以一定返回false。0的回文数为0，所以一定返回true。

>2.不使用转换为字符串，可以考虑先逆置该数，然后比较两数，相等则为true，不等则为false。


	bool isPalindrome(int x) {
	    if(x < 0) { return false; }
	    else if(x == 0) { return true; }
	    else{
	        if(getReverse(x) == x){
	            return true;
	        }
	        return false;
	    }
	}
	int getReverse(int x){
	    int y=0;
	    while(x != 0){
	        y = x % 10 + y * 10;
	        x = x / 10;
	    }
	    return y;
	}