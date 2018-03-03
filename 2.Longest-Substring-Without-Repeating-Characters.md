# 2. Longest-Substring-Without-Repeating-Characters

给定一个字符串，返回其中最长的没有字符重复的子字符串的长度

```
Examples:

Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. 
```

我一开始的思路是首先定一个函数可以输入时字符串和长度，返回是否存在这个长度的不重复的字符创，然后依次改变增加长度的值，知道不存在,但是在提交之后，发现超时，
于是改用二分法寻找，依旧超时。

```py
class Solution:
    def ifrepeat(self,s,num):
        for index in range(len(s)-num+1):
            res=s[index:index+num]
            if len(set(res))==len(res):
                return True
        return False
    
    def narrow(self,s,left,right):
        if self.ifrepeat(s,int(left/2+right/2)):
            return int(left/2+right/2),right
        else:
            return left,int(left/2+right/2)        
    
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        left=1
        right=len(s)
        while right-left>1:
            left,right=self.narrow(s,left,right)
            
        if self.ifrepeat(s,right):
            return right
        else:
            return left
  ```
  
  然后借鉴了讨论区里一位大神的代码，主要是滑动窗口的思想，逐个字符进行操作，并且记录通过字典记录字符和所在的最新位置，如果遇到重复的字符，则更新最长距离
  数值，并且更新新的起点（因为前面是不可能存在更长的不重复的字符串了），大神就是大神. 
  
  ```py
  class Solution(object):
    def lengthOfLongestSubstring(self, s):
        dic, res, start, = {}, 0, 0
        for i, ch in enumerate(s):
            if ch in dic:
                res = max(res, i-start)
                start = max(start, dic[ch]+1)
            dic[ch] = i
        return max(res, len(s)-start)  
  ```
