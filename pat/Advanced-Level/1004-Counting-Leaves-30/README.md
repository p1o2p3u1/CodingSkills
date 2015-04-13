## 1004. Counting Leaves (30)

A family hierarchy is usually presented by a pedigree tree. Your job is to count those family members who have no child.
Input

Each input file contains one test case. Each case starts with a line containing 0 < N < 100, the number of nodes in a tree, and M (< N), the number of non-leaf nodes. Then M lines follow, each in the format:

ID K ID[1] ID[2] ... ID[K]
where ID is a two-digit number representing a given non-leaf node, K is the number of its children, followed by a sequence of two-digit ID's of its children. For the sake of simplicity, let us fix the root ID to be 01.
Output

For each test case, you are supposed to count those family members who have no child for every seniority level starting from the root. The numbers must be printed in a line, separated by a space, and there must be no extra space at the end of each line.

The sample case represents a tree with only 2 nodes, where 01 is the root and 02 is its only child. Hence on the root 01 level, there is 0 leaf node; and on the next level, there is 1 leaf node. Then we should output "0 1" in a line.

Sample Input
```
2 1
01 1 02
```
Sample Output
```
0 1
```

## Solution
层序遍历
```C++
#include<cstdio>
#include<string>
#include<iostream>
#include<vector>
#include<map>
#include<queue>
using namespace std;
struct node{
	int k;
	vector<string> childs;
	node(){
		k = 0;
	}
};

int main(){
	int n,m;
	// n nodes and m parents
	cin>>n>>m;
	if(n == 1) {
		cout<<"0"<<endl;
		return 0;
	}
	map<string, node> family;
	string id;
	while(m--){
		node p;
		cin>>id>>p.k;
		for(int j=0; j<p.k; j++){
			string child;
			cin>>child;
			p.childs.push_back(child);
		}
		family[id] = p;
	}
	queue<vector<node> > q;
	vector<node> tmp; tmp.push_back(family["01"]);
	q.push(tmp);
	bool first = true;
	while(!q.empty()){
		int cnt = 0;
		vector<node> t = q.front(); q.pop();
		vector<node> next;
		for(int i=0; i<t.size(); i++){
			node n1 = t[i];
			if(n1.k == 0)  cnt++;
			else{
				for(int j=0; j<n1.k; j++){
					if(family.find(n1.childs[j]) == family.end()){
						node n2;
						next.push_back(n2);
					}
					else
						next.push_back(family[n1.childs[j]]);
				}
			}
		}
		if(next.size() > 0) q.push(next);
		if(first) {cout<<cnt; first = false;}
		else cout<<" "<<cnt;
	}
	cout<<endl;
}
```
