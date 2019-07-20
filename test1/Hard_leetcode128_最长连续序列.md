#### [128. 最长连续序列](https://leetcode-cn.com/problems/longest-consecutive-sequence/)

给定一个未排序的整数数组，找出最长连续序列的长度。

要求算法的时间复杂度为 O(n)。

示例:

```
输入: [100, 4, 200, 1, 3, 2]
输出: 4
解释: 最长连续序列是 [1, 2, 3, 4]。它的长度为 4。
```
**思路**:
哈希表

题目有时间复杂度要求，因此不能直接排序，具体做法采用字典类型存子过程，空间换时间，先建立一个哈希表，存储中间元素的最长长度，遍历数组所有元素，每次去hash里面查找大小相邻的元素是否存在，然后将相邻元素的最大长度相加并加上自身的1得到当前元素的最大连续序列长度，之后再将相邻元素的最长长度更新。遍历一次即可得到最长连续序列长度。
```
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
     unordered_map<int, int> hashmap;
        if(nums.empty())
            return 0;
      
        int maxlen=0,templen=1;
        for (int i=0; i<nums.size(); i++) {
            hashmap[nums[i]]++;
        }
        for (int i=0; i<nums.size(); i++) {
            int num=nums[i];
            templen=1;
            while (hashmap[--num]) {
                templen++;
                hashmap.erase(num);
            }
            num=nums[i];
            while (hashmap[++num]) {
                templen++;
                hashmap.erase(num);
            }
            hashmap.erase(nums[i]);
            maxlen=maxlen>templen?maxlen:templen;
        }
        return maxlen;
    }
};
```

