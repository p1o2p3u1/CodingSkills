## 101	Symmetric Tree

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree is symmetric:
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
But the following is not:
```
    1
   / \
  2   2
   \   \
   3    3
```
Bonus points if you could solve it both recursively and iteratively.


## Solution
递归版本，蛋疼版
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
	void lmr(TreeNode *x, queue<TreeNode*> &q){
		q.push(x);
		if(x == NULL) return;
		lmr(x -> left, q);
		lmr(x -> right, q);
	}
	bool rml(TreeNode *x, queue<TreeNode*> &q){
		if(!q.empty()){
			TreeNode *p = q.front(); q.pop();
			if(p == NULL){
				if(x == NULL) return true;
				else return false;
			}
			if(x == NULL) return false;
			if(p -> val == x -> val)
				return rml(x -> right, q) && rml(x -> left, q);
			else
				return false;
		}else
			return x == NULL;
	}
public:
    bool isSymmetric(TreeNode* root) {
        if(root == NULL) return true;
        queue<TreeNode*> q;
        lmr(root -> left, q);
        return rml(root -> right, q);
    }
};

```

递归版本，简单版
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
    bool isSymmetric(TreeNode *root) {
    	if(root == NULL) return true;
    	return isSymmetric(root -> left, root -> right);
    }
    bool isSymmetric(TreeNode *left, TreeNode *right){
    	if(left == NULL && right == NULL) return true;
    	if(left == NULL || right == NULL) return false;
    	return left -> val == right -> val &&
    		isSymmetric(left -> left, right -> right) &&
    		isSymmetric(left -> right, right -> left);
	}
};
```

迭代版本
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
    bool isSymmetric(TreeNode *root) {
		if(root == NULL) return true;
		stack<TreeNode*> s;
		s.push(root -> left);
		s.push(root -> right);
		while(!s.empty()){
			TreeNode *l = s.top(); s.pop();
			TreeNode *r = s.top(); s.pop();
			if(l == NULL && r == NULL) continue;
			if(l == NULL || r == NULL) return false;
			if(l -> val != r -> val) return false;
			s.push(l -> left); s.push(r -> right);
			s.push(l -> right); s.push(r -> left);
		}
		return true;
	}
};
```