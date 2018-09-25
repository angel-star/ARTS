# Algorithm

[894. All Possible Full Binary Trees](https://leetcode.com/contest/weekly-contest-99/problems/all-possible-full-binary-trees/)

题目描述：

**英文：**
A full binary tree is a binary tree where each node has exactly 0 or 2 children.

Return a list of all possible full binary trees with `N  ` nodes.  Each element of the answer is the root `node` of one possible tree.

Each node of each tree in the answer must have `node.val = 0.`

You may return the final list of trees in any order.


**中文：**

完整二叉树是一类二叉树，其中每个结点恰好有 0 或 2 个子结点。

返回包含 N 个结点的所有可能完整二叉树的列表。 答案的每个元素都是一个可能树的根结点。

答案中每个树的每个结点都必须有 node.val=0。

你可以按任何顺序返回树的最终列表。

**Example 1:**

>Input: 7


>Output: [[0,0,0,null,null,0,0,null,null,0,0],[0,0,0,null,null,0,0,0,0],[0,0,0,0,0,0,0],[0,0,0,0,0,null,null,null,null,0,0],[0,0,0,0,0,null,null,0,0]]



```c++


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
    vector<TreeNode*> allPossibleFBT(int N) {
        vector<TreeNode*> res;
        if(N % 2 == 0) return res;
        if(N == 1) {
            res.push_back(new TreeNode(0));
            return res;
        }
        
        for(int i=1;i<N;i+=2) {
            if(N-i-1 < 1) continue;
            auto left = allPossibleFBT(i);
            auto right = allPossibleFBT(N-i-1);
            for(auto &l : left){
                for(auto &r : right) {
                    auto temp = new TreeNode(0);
                    temp->left = l;
                    temp->right = r;
                    res.push_back(temp);
                }
            }
        }
        
        return res;
    }
};
```
