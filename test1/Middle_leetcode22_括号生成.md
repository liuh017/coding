## [22. 括号生成](https://leetcode-cn.com/problems/generate-parentheses/)
### 给出 n 代表生成括号的对数，请你写出一个函数，使其能够生成所有可能的并且有效的括号组合。

例如，给出 n = 3，生成结果为：
```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```
**BFS+剪枝**
```c++
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> res;
        func(res,"",0,0,n);
            return res;
        
    }
    
    void func(vector<string> &res, string str,int l,int r, int n)
    {
        if(l>n||r>n||r>l) return;
        if(l==n && r==n)
        {res.push_back(str);
         return;
        }
        func(res,str+'(',l+1,r,n);
        func(res,str+')',l,r+1,n);
        return;
    }
};
```
