## 144	Binary Tree Preorder Traversal
Given a binary tree, return the preorder traversal of its nodes' values.

For example:
Given binary tree `{1,#,2,3}`,
```
   1
    \
     2
    /
   3
```
return `[1,2,3]`.

## Solution

```C++
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
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> ret;
        if(root == NULL) return ret;
        stack<TreeNode*> s;
        s.push(root);
        while(!s.empty()){
        	TreeNode *p = s.top(); s.pop();
        	ret.push_back(p -> val);
        	if(p -> right != NULL) s.push(p -> right);
        	if(p -> left != NULL) s.push(p -> left);
    	}
    	return ret;
    }
};
```