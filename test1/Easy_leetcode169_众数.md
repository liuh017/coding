给定一个大小为 n 的数组，找到其中的众数。众数是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在众数。

来源：力扣（LeetCode）
[链接：](https://leetcode-cn.com/problems/majority-element)

示例 1:

输入: [3,2,3]
输出: 3
示例 2:

输入: [2,2,1,1,1,2,2]
输出: 2

**思路**：这道题用摩尔投票法，这种方法是因为题目中说众数是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。所以设置一个计数器，选定第一个值作为起始值，然后后面的值如果是这个值那么计数加一，如果不等，那么计数减一，当计数器的值为零时，选取当前值作为新值继续计数。因为众数肯定大于1/2所以最后计数器不为零的数肯定是众数。

```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
       int num=nums[0];
        int count=0;
        for(int i=0;i<nums.size();i++)
        {
            if(count==0)
            {
                num=nums[i];
                count=1;
            }
            else if(num==nums[i])
                count++;
            else
            {
                count--;
            }
        }
        return num;
    }
};
```
