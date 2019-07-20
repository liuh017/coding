给定一个整数数组 nums，其中恰好有两个元素只出现一次，其余所有元素均出现两次。 找出只出现一次的那两个元素。

来源：力扣（LeetCode）
[链接：](https://leetcode-cn.com/problems/single-number-iii)

示例 :

输入: [1,2,1,3,2,5]
输出: [3,5]
注意：

结果输出的顺序并不重要，对于上面的例子， [5, 3] 也是正确答案。
你的算法应该具有线性时间复杂度。你能否仅使用常数空间复杂度来实现？

**思路**
只出现一次的两个数使不同的。
1. 首先通过报所有数进行异或的到 a异或b的值，通过其找出不同比特位。
2. 通过该比特位将所有的数分为两类，分别进行异或，即可得到a,b.

 ```c++
 class Solution {
public:
    vector<int> singleNumber(vector<int>& nums) {
        int temp=0;
        vector<int> result(2);
        for(int i=0;i<nums.size();i++)
        {
            temp^=nums[i];
        }
        int ibit=1;
        while((ibit & temp)==0)
        {
            ibit<<=1;
        }
        for(int i=0;i<nums.size();i++)
        {
            if((nums[i]&ibit)==0)
            {
                result[0]^=nums[i];
            }
            else
            {
                 result[1]^=nums[i];
            }
        }
        return result;
        
    }
};
```
