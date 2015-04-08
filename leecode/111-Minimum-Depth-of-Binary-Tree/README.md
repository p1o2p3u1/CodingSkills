## Minimum Depth of Binary Tree
Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

## Solution
注意是从根节点到叶结点的最小深度，必须是到叶结点才可以。
递归版本解法
```C++
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int minDepth(TreeNode *root) {
        if(root == NULL) return 0;
        if(root -> left == NULL && root -> right == NULL) return 1;
        if(root -> left == NULL)
            return minDepth(root -> right) + 1;
        else if(root -> right == NULL)
            return minDepth(root -> left) + 1;
        else
            return min(minDepth(root -> left), minDepth(root -> right)) + 1;
    }
};
```
迭代版，使用层序遍历，当在某一层不存在子节点时，直接返回层数。
```C++
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int minDepth(TreeNode *root) {
        if(root == NULL) return 0;
        queue<vector<TreeNode*> > q;
        q.push({root});
        int level = 1;
        while(!q.empty()){
            vector<TreeNode*> v = q.front(); q.pop();
            vector<TreeNode*> next;
            for(int i=0; i<v.size(); i++){
                if(v[i] -> left == NULL && v[i] -> right == NULL) return level;
                if(v[i] -> left != NULL) next.push_back(v[i] -> left);
                if(v[i] -> right != NULL) next.push_back(v[i] -> right);
            }
            level += 1;
            if(next.size() > 0) q.push(next);
        }
        return level;
    }
};
```
