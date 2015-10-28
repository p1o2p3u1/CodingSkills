## 107-Binary-Tree-Level-Order-Traversal-II

Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree `{3,9,20,#,#,15,7}`,
```
    3
   / \
  9  20
    /  \
   15   7
```
return its bottom-up level order traversal as:
```
[
  [15,7],
  [9,20],
  [3]
]
```

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
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        vector<vector<int>> ret;
        if(root == NULL) return ret;
        queue<vector<TreeNode*>> q;
        q.push({root});
        while(!q.empty()){
        	vector<TreeNode*> v = q.front(); q.pop();
        	vector<TreeNode*> next;
        	vector<int> data;
        	for(int i=0; i<v.size(); i++){
        		if(v[i] -> left != NULL) next.push_back(v[i] -> left);
        		if(v[i] -> right != NULL) next.push_back(v[i] -> right);
        		data.push_back(v[i] -> val);
        	}
        	if(next.size() > 0) q.push(next);
        	ret.insert(ret.begin(), data);
    	}
    	return ret;
    }
};
```