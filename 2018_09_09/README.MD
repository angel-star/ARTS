# Algorithm

[894. All Possible Full Binary Trees](https://leetcode.com/contest/weekly-contest-99/problems/all-possible-full-binary-trees/)

题目描述：

**英文：**
A full binary tree is a binary tree where each node has exactly 0 or 2 children.

Return a list of all possible full binary trees with `N  ` nodes.  Each element of the answer is the root `node` of one possible tree.

Each node of each tree in the answer must have `node.val = 0.`

You may return the final list of trees in any order.


**中文：**
你将得到一个字符串数组 A。

如果经过任意次数的移动，S == T，那么两个字符串 S 和 T 是特殊等价的。

 

一次移动包括选择两个索引 i 和 j，且 i％2 == j％2，并且交换 S[j] 和 S [i]。

现在规定，A 中的特殊等价字符串组是 A 的非空子集 S，这样不在 S 中的任何字符串与 S 中的任何字符串都不是特殊等价的。

 

返回 A 中特殊等价字符串组的数量。

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
