## 110	Balanced Binary Tree

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

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
private:
	int height(TreeNode *x){
		if(x == NULL) return 0;
		if(x -> left == NULL && x -> right == NULL) return 1;
		return max(height(x -> left), height(x -> right)) + 1;
	}
public:
    bool isBalanced(TreeNode* root) {
        if(root == NULL) return true;
        int l = height(root -> left);
        int r = height(root -> right);
        if(abs(l-r)>1) return false;
        return isBalanced(root -> left) && isBalanced(root -> right);
    }
};
```