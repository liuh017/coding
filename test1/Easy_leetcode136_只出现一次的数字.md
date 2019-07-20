## 给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。
[链接：](https://leetcode-cn.com/problems/single-number)

说明：你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

示例 1:
输入: [2,2,1]
输出: 1
示例 2:
输入: [4,1,2,1,2]
输出: 4

**解法**：异或
解法：异或
异或运算的特点：两个相同的数字异或，结果为0。

因为数组中除了一个元素只出现一次之外，其它的元素都出现两次，如果把所有的数都异或，相同的数字异或为0，最后只剩下出现一次的数字，它和0异或，结果就是它本身。

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
    int result=0;
        for(int i=0;i<nums.size();i++)
        {
            result^=nums[i];
        }
        return result;
    }
};
```
