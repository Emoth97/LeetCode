Given a 32-bit signed integer, reverse digits of an integer.

Example 1:

Input: 123
Output: 321
Example 2:

Input: -123
Output: -321
Example 3:

Input: 120
Output: 21
Note:
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

#注意点：
>1.考虑使用INT_MAX、INT_MIN进行边界判断，头文件limits.h。

>2.与INT_MAX、INT_MIN比较非常耗时，且只能在反转结束后进行判断。因此考虑在反转的过程中进行判断。只要在反转过程中不满足循环体中的式子就意味着这个传入的参数不合法，超出了int可表示的范围。

	static int myreverse(int x) { 
	    long y = 0;
	    while(x != 0) {
	        y = y * 10 + x % 10;
	        x = x/10;
	    }
	    if(y < INT_MIN || y > INT_MAX) {return 0;}
	    return y;
	}
	static int sec_4_reverse(int x) {
	    int y = 0;//需要返回的数
	    while(x != 0) {
	        int temp = y; // 暂存y的值
	        y = y * 10 + x % 10; // 倒序；把x的最低位依次压入y的最低位
	        // 反向推，若推不出原值则溢出
			if((y - x % 10) / 10 != temp) {
	            return 0;
	        }
	        x /= 10;
	    }
	    return y;
	}
	int reverse(int x) {
	   // return myreverse(x);
	    return sec_4_reverse(x);
	}
