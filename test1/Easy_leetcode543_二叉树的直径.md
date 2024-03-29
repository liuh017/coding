#### [543. 二叉树的直径](https://leetcode-cn.com/problems/diameter-of-binary-tree/)

#### 给定一棵二叉树，你需要计算它的直径长度。一棵二叉树的直径长度是任意两个结点路径长度中的最大值。这条路径可能穿过根结点。

示例 :
给定二叉树

```
      1
     / \
    2   3
   / \     
  4   5    
```

返回 3, 它的长度是路径 [4,2,1,3] 或者 [5,2,1,3]。

注意：两结点之间的路径长度是以它们之间边的数目表示。

**思路**:
分三种情况：len_l+len_r、max(l)、max(r)
```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int maxLength=0;
    int maxDepth(TreeNode* root)
    {
        if(!root)
            return 0;
        int l=maxDepth(root->left);
        int r=maxDepth(root->right);
        if((l+r)>maxLength)
            maxLength=(l+r);
        return 1+max(l,r);
    }
        
    int diameterOfBinaryTree(TreeNode* root) 
    {
        if(!root)
            return 0;
        maxDepth(root);
        return maxLength;
    }
};
```

