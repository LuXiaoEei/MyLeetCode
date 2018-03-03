# Two Sum

这道题我在leetcode做的第一题,给定一组数字，和一个目标，从那组数字中寻找出和是目标值得一对数字


比如：

```
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

我的思路主要是遍历，首先给定一个数字，然后在num中去掉这个数字，之后用差算出另一个数字，然后判断在剩下的数字中是否存在这个数字

```python
class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        for Index in range(len(nums)):
            p=nums.copy()
            p.pop(Index)
            cand=target-nums[Index]
            if cand in p:
                if p.index(cand)<Index:
                    return [Index,p.index(cand)]
                else:
                    return [Index,p.index(cand)+1]
        return 'no solve'
```
