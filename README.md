# CodingSkills
Test Cheat Sheet

## 排序
### 选择排序

1. 初始时，`i=0`
2. 从`i+1`到最后里最小的数，跟i交换，然后`i++`。
3. 重复2，直到i到数组的末尾。

```C++
void selectSort(int a[], int n){
    for(int i=0; i<n; i++){
        int min = i;
        for(int j=i+1; j<n; j++){
            if(a[j] < a[min])
                min = j;
        }
        swap(a[i], a[min]);
    }
}
```
或者
```C++
void selectSort(int a[], int n){
    for(int i=0; i<n; i++){
        for(int j=i+1; j<n; j++){
            if(a[i] > a[j])
                swap(a[i], a[j]);
        }
    }
}
```

### 插入排序

1. 初始时`i=0`
2. 确保从0到i是有序的，否则移动数据使其有序，`i++`
3. 重复2，直到i到数组末尾。

```C++
void insertSort(int a[], int n){
	for(int i=0; i<n; i++){
		for(int j=i; j>0; j--){
			if(a[j-1] > a[j]) // 注意比较的是0~i里面的数，使其有序
				swap(a[j-1], a[j]);
			else break;
		}
	}
}
```
### 冒泡排序

1. 初始时`i=0`
2. 从`0~n-i`中不断移动最大的数，使其移动到末尾，`i++`
3. 重复2，直到i到达数组末尾。

```C++
void bubbleSort(int a[], int n){
	for(int i=0; i<n; i++){
		for(int j=0; j<n-i-1; j++){
		    if(a[j] > a[j+1]) // 往上冒泡
		        swap(a[j], a[j+1]);
		}
	}
}
```

### 希尔排序
希尔排序与插入排序类似，区别在于在向前进行比较的时候，不是比较前面第1个，而是比较前面第h个。
```C++
void shellSort(int a[], int n){
	int h = n / 3 + 1; // 定义增长率
	while(h >=1){
	    // 此处与插入排序类似
		for(int i=h; i<n; i++){ 
			for(int j=i; j>=h && a[j] < a[j-1]; j-=h){
				swap(a[j], a[j-1]);
			}
		}
		h /= 3;
	}
}
```

### 归并排序

```C++
/*
    将low~mid和mid+1~high合并起来，使用aux作为临时存储
*/
void merge(int a[], int aux[], int low ,int mid, int high){
	for(int i=low; i<=high; i++) aux[i] = a[i];
	int i=low, j=mid+1;
	for(int k=low; k<=high; k++){
		if(i > mid)                 a[k] = aux[j++];
		else if(j > high)           a[k] = aux[i++];
		else if(aux[i] <= aux[j])   a[k] = aux[i++];
		else                        a[k] = aux[j++];
	}
}
/*
    排序左半部分，排序右半部分，然后合并两部分
*/
void sort(int a[], int aux[], int low, int high){
	if(low >= high) return;
	int mid = low + (high - low ) / 2;
	sort(a, aux, low, mid);
	sort(a, aux, mid+1, high);
	merge(a, aux, low, mid, high);
}
/*
    对外接口，申请临时数组
*/
void mergeSort(int a[], int n){
	int *aux = (int*)malloc(sizeof(int) * n);
	sort(a, aux, 0, n-1);
	free(aux);
}
```

### 快速排序

```C++
int partition1(int array[], int low, int high){
	int key = array[low];
	int i=low, j=high + 1;
	while(true){
		while(i < high && array[++i] < key);
		while(j > low && array[--j] > key);
		if(i >= j) break;
		swap(array[i], array[j]);
	}
	swap(array[low], array[j]);
	return j;
}

int partition2(int array[], int low, int high){
	
}
void qsort(int array[], int low, int high){
	int k = partition(array, low, high);
	qsort(array, low, k-1);
	qsort(array, k+1, high);
}

void quickSort(int array[], int n){
	qsort(array, 0, n-1);
}

```

### 堆排序

```C++


```

## 树
```C++
struct TreeNode {
	int val;
	TreeNode *left;
	TreeNode *right;
	TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
```
### 先序遍历非递归
```C++
vector<int> preorderTraversal(TreeNode *root){
	vector<int> ret;
	if(root == NULL) return ret;
	stack<TreeNode*> s;
	s.push(root);
	while(!s.empty()){
		TreeNode *t = s.top(); s.pop();
		ret.push_back(t -> val);
		if(t -> right)// 注意是先右边入栈
			s.push(t -> right);
		if(t -> left)
			s.push(t -> left);
	}
	return ret;
}

```
### 中序遍历非递归
```C++
vector<int> inorderTraversal(TreeNode *root){
	vector<int> ret;
	if(root == NULL) return ret;
	stack<TreeNode*> s;
	TreeNode *t = root;
	while(!s.empty() || t != NULL){
		if(t != NULL){
			s.push(t);
			t = t -> left;
		}else{
			t = s.top(); s.pop();
			ret.push_back(t -> val);
			t = t -> right;
		}
	}
	return ret;
}
```
### 后序遍历非递归
```C++
vector<int> postorderTraversal(TreeNode *root){
	vector<int> ret;
	if(root == NULL) return ret;
	stack<TreeNode*> s;
	TreeNode *p = root, *visit;
	while(!e.empty() || p != NULL){
		if(p != NULL){
			s.push(p);
			p = p -> left;
		}else{
			p = s.top();
			if(p -> right && p -> right != visit){
				p = p -> right;
				s.push(p);
				p = p -> left;
			}else{
				visit = p;
				ret.push_back(p -> val);
				s.pop();
				p = NULL;
			}
		}
	}
	return ret;
}
```
### 层序遍历
```C++
vector<vector<int> > levelOrder(TreeNode *root){
	vector<vector<int> > ret;
	if(root == NULL) return ret;
	queue<vector<TreeNode*> > q;
	q.push({root});
	while(!q.empty()){
		vector<TreeNode*> x = q.front(); q.pop();
		vector<int> tmp; // 存放该层遍历的结果
		vector<TreeNode*> next; // 存放下一层要遍历的节点
		for(int i=0; i<x.size(); i++){
			tmp.push_back(x[i] -> val);
			if(x[i] -> left != NULL) next.push_back(x[i] -> left);
			if(x[i] -> right != NULL) next.push_back(x[i] -> right); 
		}
		if(next.size() > 0) q.push(next);
		ret.push_back(tmp);
	}
	return ret;
}

```
### Binary Search
```C++
int binarySearch(int array[], int n, int key){
	assertSorted(array);
	int low = 0, high = n-1;
	while(low <= high){
		int mid = low + (high - low) / 2;
		if(array[mid] == key) 		return mid;
		else if(array[mid] > key) 	high = mid - 1;
		else						low = mid + 1;
	}
	return -1;
}
```
### Tries
### Red Black

## 子串查找
### KMP
### Boyer-Moore
### Rabin-Karp

## 图
### Kruskal
### Prim
### Dijkstra
### SPFA

## 其他
### atoi
### strlen
```C++
int strlen(const char *str){
    const char *s = str;
    while(*s) ++s; // 注意此处是*s
    return (s - str);
}
```
### auto_ptr
### vector
### string
### hashtable
### 链表
### 栈
### 队列
### malloc
### LRU
```C++
// 使用list+map
class LRUCache{
private:
    int capacity;
    list<pair<int, int> > items;
    unordered_map<int, list<pair<int, int> >::iterator> cache;
public:
	LRUCache(int capacity): capacity(capacity) {}
	int get(int key){
		if(cache.find(key) == cache.end())
			return -1;
		// 将找到的节点放到链表头
		items.splice(items.begin(), items, cache[key]);
		return cache[key] -> second;
	}
	void set(int key, int value){
		if(cache.find(key) == cache.end()){
			if(item.size() == capacity){
				// 移除对应的cache和链表底
				cache.erase(items.back().first);
				items.pop_back();
			}
			// 此时确保有足够的空间
			items.push_front(make_pair(key, value));
			cache[key] = items.begin();
		}else{
			// 将找到的节点放到链表头，更新value
			items.splice(items.begin(), items, cache[key]);
			cache[key] -> second = value;
		}
	}
};
```
### 经典DP

