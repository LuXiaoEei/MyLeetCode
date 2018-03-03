# Longest-Palindromic-Substring

给定字符串，寻找最长的回文串（从前往后和从后往前是一样的）

```
Example:

Input: "babad"

Output: "bab"

Note: "aba" is also a valid answer.

```

发现回文最中间只有两种模式:a*a,或者aa，所以首先寻找满足a*a或者aa的字符串，然后分别向左右扩张，如果左右一个字符相同，则回文数可以边长，然后继续扩张
直达左右不等，将最左边和最右边字符的位置，字符串的长度保存，最后从保存的list中寻找出最长的,由于这个算法本质上寻找出了所有的回文字符，所以速度慢

```py
class Solution:
    
    def ifcrease(self,s,left,right):
        if left<1 or right>len(s)-2:
            return [left,right,right-left+1]
        elif s[left-1]==s[right+1]:
            return self.ifcrease(s,left-1,right+1)
        else:
            return [left,right,right-left+1]
       
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """

        Res=[]       
        for index in range(len(s)-1):
            if s[index]==s[index+1]:
                left,right=index,index+1
                Res.append(self.ifcrease(s,left,right))

        for index in range(len(s)-2):
            if s[index]==s[index+2]:
                left,right=index,index+2
                Res.append(self.ifcrease(s,left,right))

        if len(Res)!=0:
            Len=[x[2] for x in Res]
            left,right,length=Res[Len.index(max(Len))]
            return s[left:(right+1)]
        else:
            return s[0]
```

看了讨论区，有一个算法是，当找出长度为n的回文字符串之后，接下来只需要寻找是否存在长度为n+1的字符串

```py
class Solution:
    # @return a string
    def longestPalindrome(self, s):
        if len(s)==0:
        	return 0
        maxLen=1
        start=0
        for i in range(len(s)):
        	if i-maxLen >=1 and s[i-maxLen-1:i+1]==s[i-maxLen-1:i+1][::-1]:
        		start=i-maxLen-1
        		maxLen+=2
        		continue

        	if i-maxLen >=0 and s[i-maxLen:i+1]==s[i-maxLen:i+1][::-1]:
        		start=i-maxLen
        		maxLen+=1
        return s[start:start+maxLen]
                
```
