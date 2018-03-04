# Palindrome Number

判断一个数字是否是回文数

注意：

负数不是回文数

如果先把数字转换为字符串，那么会需要额外的空间

直接反转数字，可能会面临溢出的问题


我考虑的是,首先判断数字的数量级，然后依次判断最后一位和第一位数字是否相等，相等的话，去掉这两位数字之后，再进行比较

```py
class Solution:
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        if x<0:
            return False
        
        r=1
        while x/r>10:
            r*=10
        
        while r>=1:        
            left=x//r
            right=x%10
            if left!=right:
                return False
            x=(x-r*left)//10
            r=r/100
        return True

```
