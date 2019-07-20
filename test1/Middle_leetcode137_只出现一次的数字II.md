给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现了三次。找出那个只出现了一次的元素。

来源：力扣（LeetCode）
[链接：](https://leetcode-cn.com/problems/single-number-ii)

**说明**：

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

**示例 1**:

输入: [2,2,3,2]

输出: 3

**示例 2**:

输入: [0,1,0,1,0,1,99]

输出: 99

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int ones=0,twos=0;
        for(int i=0;i<nums.size();i++)
        {
            ones=(ones^nums[i])&~twos;
            twos=(twos^nums[i])&~ones;
        }
        return ones;
    }
};
```

**思路**
首先我们会定义两个变量ones和twos，当遍历nums的时候，对于重复元素x，第一次碰到x的时候，我们会将x赋给ones，第二次碰到后再赋给twos，第三次碰到就全部消除。赋值和消除的动作可以通过xor很简单的实现。所以我们就可以写出这样的代码

```c++
 ones = (ones^num)
 twos = (twos^num)
```
 
但是上面写法忽略了，只有当ones是x的时候，我们会将0赋给twos，那要怎么做呢？我们知道如果b=0，那么b^num就变成了x，而x&~x就完成了消除操作.所以代码应该写成：
```c++
 ones = (ones^num)&~(twos)
 twos = (twos^num)&~(ones)
```
第一次出现x记录在ones中，并且此时twos应为0；第二次出现x记录在twos中，同时ones置为0,；第三次出现x，则ones，twos均重置为0

例如：第一个数：10，则ones = 10，twos = 0,第二个数10，则ones = 0, twos = 10, 第三个数10, 则ones= 0,twos=0
```c++
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        ones, twos = 0,0
        for num in nums:
            ones = (ones^num)&~(twos)
            twos = (twos^num)&~(ones)
        
        return ones
```c++
**若题目改成找只出现两次的数，则return twos**


