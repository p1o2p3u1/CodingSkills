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
### 已知前序中序，求后续
```C++
string post_order(const string &pre, const string &mid){
	unsigned long len = pre.length();
	if(len <= 1) return pre;
	char root = pre[0];
	unsigned long index = pre.find(root);
	string left_pre = pre.substr(1, index);
	string right_pre = pre.substr(index + 1, len - index - 1);
	string left_mid = mid.substr(0, index);
	string right_mid = mid.substr(index + 1, len - index - 1);
	return post_order(left_pre, left_mid) + post_order(right_pre, right_mid) + root;
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
### Trie
前缀树
```C++
struct Trie{
	char c;
	int cnt; // 到当前Trie节点为前缀的单词的个数
	struct Trie *next[26];
	Trie(char c, int v = 0): c(c), cnt(v) {
		for(int i=0; i<26; i++){
			next[i] = nullptr;
		}
	}
} ;

void insert(Trie *root, string str){
	Trie *p = root;
	for(int i=0; i<str.length(); i++){
		char c = str[i];
		int v = c - 'a';
		if(p -> next[v] == nullptr){
			p -> next[v] = new Trie(c, 1);
		} else {
			p->next[v] -> cnt ++;
		}
		p = p -> next[v];
	}
}
// 返回以str为前缀的单词的个数
int query(Trie *root, string str){
	Trie *p = root;
	int ret = 0;
	for(int i=0; i<str.length(); i++){
		int v = str[i] - 'a';
		if(p -> next[v] == nullptr) return 0;
		else {
			ret = p -> next[v] -> cnt;
			p = p -> next[v];
		}
	}
	return ret;
}

```
### 后缀数组
### 线段树
### 树状数组
### 红黑树

## 子串查找
### KMP
```C++
void get_next(const string sub, int *next) {
    int len=sub.length();
    int i,k;
    next[0]=k=-1;
    for (i=0; i<len;) {
        if (k==-1 || sub[i]==sub[k]) {
            k++; i++;
            if (sub[k]!=sub[i]) next[i]=k;
            else next[i]=next[k];    //避免重复计算优化next数组
        }
        else k=next[k];
    }
}

int KMP(const string str, const string sub, const int *next) {
    //返回子串在主串中的起始位置下标
    int i,j;
    int len1=str.length();
    int len2=sub.length();
    for (i=0, j=0; i<len1 && j<len2;)
        if (j==-1 || str[i]==sub[j])
            i++; j++;
        else 
            j=next[j];
    if (j==len2)
        return i-len2;
    return -1; //如果找不到就返回-1
}
```
### Boyer-Moore
### Rabin-Karp

## 图
### 并查集
### Kruskal
### Prim
### Dijkstra
### SPFA
### 拓扑排序
### 二分图
## 几何
### 多边形面积
## 其他
### BigInteger

```C++
const int BASE_LENGTH = 2;
const int BASE = (int) pow(10, BASE_LENGTH);
const int MAX_LENGTH = 500;

string int_to_string(int i, int width, bool zero) {
    string res = "";
    while (width--) {
        if (!zero && i == 0) return res;
        res = (char)(i%10 + '0') + res;
        i /= 10;
    }
    return res;
}

struct bigint {
    int len, s[MAX_LENGTH];

    bigint() {  
        memset(s, 0, sizeof(s));  
        len = 1;  
    }

    bigint(unsigned long long num) {
        len = 0;
        while (num >= BASE) {
            s[len] = num % BASE;
            num /= BASE;
            len ++;
        }
        s[len++] = num;
    }

    bigint(const char* num) {
        int l = strlen(num);
        len = l/BASE_LENGTH;
        if (l % BASE_LENGTH) len++;
        int index = 0;
        for (int i = l - 1; i >= 0; i -= BASE_LENGTH) {
            int tmp = 0;
            int k = i - BASE_LENGTH + 1;
            if (k < 0) k = 0;
            for (int j = k; j <= i; j++) {
                tmp = tmp*10 + num[j] - '0';
            }
            s[index++] = tmp;
        }
    }

    void clean() {  
        while(len > 1 && !s[len-1]) len--;  
    }

    string str() const {
        string ret = "";
        if (len == 1 && !s[0]) return "0";
        for(int i = 0; i < len; i++) {
            if (i == 0) {
                ret += int_to_string(s[len - i - 1], BASE_LENGTH, false);
            } else {
                ret += int_to_string(s[len - i - 1], BASE_LENGTH, true);
            }
        }
        return ret;
    }

    unsigned long long ll() const {
        unsigned long long ret = 0;
        for(int i = len-1; i >= 0; i--) {
            ret *= BASE;
            ret += s[i];
        }
        return ret;
    }

    bigint operator + (const bigint& b) const {
        bigint c = b;
        while (c.len < len) c.s[c.len++] = 0;
        c.s[c.len++] = 0;
        bool r = 0;
        for (int i = 0; i < len || r; i++) {
            c.s[i] += (i<len)*s[i] + r;
            r = c.s[i] >= BASE;
            if (r) c.s[i] -= BASE;
        }
        c.clean();
        return c;
    }

    bigint operator - (const bigint& b) const {
        if (operator < (b)) throw "cannot do subtract";
        bigint c = *this;
        bool r = 0;
        for (int i = 0; i < b.len || r; i++) {
            c.s[i] -= b.s[i];
            r = c.s[i] < 0;
            if (r) c.s[i] += BASE;
        }
        c.clean();
        return c;
    }

    bigint operator * (const bigint& b) const {  
        bigint c;
        c.len = len + b.len;  
        for(int i = 0; i < len; i++)  
            for(int j = 0; j < b.len; j++)  
                c.s[i+j] += s[i] * b.s[j];  
        for(int i = 0; i < c.len-1; i++){  
            c.s[i+1] += c.s[i] / BASE;  
            c.s[i] %= BASE;  
        }  
        c.clean();  
        return c;  
    }

    bigint operator / (const int b) const {
        bigint ret;
        int down = 0;
        for (int i = len - 1; i >= 0; i--) {
            ret.s[i] = (s[i] + down * BASE) / b;
            down = s[i] + down * BASE - ret.s[i] * b;
        }
        ret.len = len;
        ret.clean();
        return ret;
    }

    bool operator < (const bigint& b) const {
        if (len < b.len) return true;
        else if (len > b.len) return false;
        for (int i = 0; i < len; i++)
            if (s[i] < b.s[i]) return true;
            else if (s[i] > b.s[i]) return false;
        return false;
    }

    bool operator == (const bigint& b) const {
        return !(*this<b) && !(b<(*this));
    }

    bool operator > (const bigint& b) const {
        return b < *this;
    }
};
```
### atoi
```C
int atoi(const char *str) {
	int num = 0;
	int sign = 1;
	const int n = strlen(str);
	int i = 0;
	while (str[i] == ' ' && i < n) i++;
	if (str[i] == '+') {
		i++;
	} else if (str[i] == '-') {
		sign = -1;
		i++;
	}
	for (; i < n; i++) {
		if (str[i] < '0' || str[i] > '9')
			break;
		// -2147483648 or +2147483647 ?
		if (num > INT_MAX / 10 ||
				(num == INT_MAX / 10 &&
					(str[i] - '0') > INT_MAX % 10)) {
						return sign == -1 ? INT_MIN : INT_MAX;
					}
		num = num * 10 + str[i] - '0';
	}
	return num * sign;
}
```
### strlen
```C++
int strlen(const char *str){
    const char *s = str;
    while(*s) ++s; // 注意此处是*s
    return (s - str);
}
```
### strcpy
```C++
char *strcpy(char *dst, const char*str){
    if(str == NULL) return NULL;
    if(dst == NULL) return NULL;
    char *ret = dst;
    while( (*dst++ = *src++) != '\0');
    return ret;
}

```
### auto_ptr
```C++
// auto_ptr<T*> ptr(t);
template<typename T>
class auto_ptr<T>{
private:
	T *p;
public:
	// 构造函数禁止隐式类型转换
	explicit auto_ptr(T* t = 0): p(t){};
	// 拷贝构造函数
	template<typename U>
	auto_ptr(auto_ptr<U> &u): p(u.release()){}
	// copy assignment
	template<typename U>
	auto_ptr<T>& operator=(auto_ptr<U> &u){
		if(this != &u) reset(u.release()); // 右操作数自动释放，变为NULL
		return *this;
	}
	//析构函数
	~auto_ptr(){delete p;}
	// 功能函数
	T& operator*() {return *p;}
	T* operator->() {return p;}
	T* get() {return p;}
	T* release(){
		T* tmp = p;
		p = NULL;
		return tmp;
	}
	void reset(T* t = 0){
		if(p != t){
			delete p;
			p = t;
		}
	}
};
```
### gcd
```C++
int gcd(int x, int y){
	if(x < y) return gcd(y, x);
	if(y == 0) return x;
	return (y, x % y);
}

int gcd(int a, int b)
{
	while (a = a % b)
	{
		a ^= b;
		b ^= a;
		a ^= b;
	}
	return b;
}
```
### Prime
```C++
bool isPrime(int n){
    if (n == 1 || n % 2 == 0)
        return false;  
    int t = sqrt(n);
    for (int i = 3; i <= t; i += 2)
        if (n % i == 0)
            return false;
    return true;
}
// 打表法
int is_prime[UP_LIMIT + 1];
for (int i = 1; i <= UP_LIMIT; i++) // init to 1
    is_prime[i] = 1;
for (int i = 4; i <= UP_LIMIT; i += 2) // even number is not
    is_prime[i] = 0;
for (int k = 3; k*k <= UP_LIMIT; k++) // start from 9, end at sqrt
    if (is_prime[k])
        for(int i = k*k; i <= UP_LIMIT; i += 2*k) // every two is not 
            is_prime[i] = 0;
```
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


### 进程同步（基于PV操作）

#### 生产者消费者问题

一组生产者和一组消费者共享大小为N的缓冲区，只要缓冲区未满就能放产品，只要缓冲区未空就能取产品，但一次只能有一个生产者放产品，或者只能有一个消费者取产品。

```C++
// P可以理解为检测，V可以理解为提醒， 这是个1 vs 1的问题。
semaphore mutex = 1; // 对缓冲区是互斥的访问
semaphore item = 0, buffer = n;

procedure Producer() {
	
	while(1){
		// 生产商品
		P(buffer);  // 检查buffer
		P(mutex);
		// 将商品放入缓冲区
		V(mutex);
		V(item); 	// 提醒放入一个商品
	}	
}

procedure Customer() {
	
	while(1){
		P(item);	// 检查是否有商品
		P(mutex);
		// 取出商品
		V(mutex);
		V(buffer);	// 提醒消费一件商品

	}

}

#### 读者写者问题

1. 允许多个读者同时读
2. 只允许一个写者写，写是排他性的。
3. 写者要等所有读者都退出后才能写。

```C++
// 这是一个1 vs n的问题，需要一个计数器纪录读者的数目，满足条件3时才能写

int readerNum = 0;
semophore ReaderMutex = 1, WriterMutex = 1;

procedure Writer(){

	while(1){
		P(WriteMutex)
		write;
		V(WriteMutex);
	}

}
// 写是互斥的，而读者是可以并发的。如果在生产者消费者案例中，允许消费者并发消费，就变成读者写者问题。
procedure Reader(){

	while(1){
		P(ReaderMutex);
		if(readerNum == 0){
			P(WriterMutex); // 只需要第一个进入的读者阻塞写者，否则就变成每次只有一个读者在读。
		}
		readerNum ++;  // 对readerNum的修改是互斥的。
		V(ReaderMutex);
		read;
		P(ReaderMutex);
		readerNum--;
		if(readerNum == 0){
			V(WriterMutex); // 最后一个读者退出时，可以发信号量给写者
		}
		V(ReaderMutex);
	}
}

```

新增一个需求：写者优先。

即当有写者要写时，需要先阻塞其余写者的进入。因此要增加一个互斥信号量。
```C++
int readerNum = 0;
semophore ReaderMutex = 1, WriterMutex = 1, AllReaderStop = 1;

procedure Writer(){
	
	while(1){
		P(AllReaderStop);
		P(WriterMutex);
		write;
		V(WriterMutex);
		V(AllReaderStop);
	}
}

procedure Reader(){

	while(1){
		P(AllReaderStop); // 检查是否有读者阻塞
		P(ReaderMutex);
		if(readerNum == 0){
			P(WriterMutex);
		}
		readerNum++;
		V(ReaderMutex);
		V(AllReaderStop); // 此时释放
		read;
		P(ReaderMutex);
		readerNum--;
		if(readerNum == 0){
			V(WriterMutex);
		}
		V(ReaderMutex);
	}	
}
```

#### 哲学家进餐问题

1. 5个哲学家，5根筷子
2. 哲学家进餐时一次只能拿一根筷子，只有拿了两根筷子才能进餐。吃完后放下筷子。

```C++
// 这是一个m vs n的问题，注意这类问题的解题方法。
// 5个哲学家是5个进程，5根筷子是5个信号量。
// 注意下面这个方法会产生死锁
semophore chopsticks[5] = {1, 1, 1, 1, 1};

procedure Philosopher_i(){

	while(1){
		P(chopsticks[i]);
		P(chopsticks[(i+1)%5]);
		eat;
		V(chopsticks[(i+1)%5]);
		V(chopsticks[i]);
		think;
	}

}
// 此时，当有5个哲学家同时执行P(chopsticks[i])时，就会产生死锁。
// 因此，需要对抓筷子添加互斥，最多同时允许4个哲学家进餐

semophore chopsticks[5] = {1, 1, 1, 1, 1};
semophore mutex = 1;

procedure Philosopher_i(){
	
	while(1){
		P(mutex);
		P(chopsticks[i]);
		P(chopsticks[(i+1)%5]);
		V(mutex); // V(mutex)要在eat之前，否则变成每次只有一个哲学家在进餐了。
		eat; 
		V(chopsticks[(i+1)%5]);
		V(chopsticks[i]);
		think;
	}
}
```

#### 吸烟者问题
三个抽烟进程，一个供应进程。抽烟需要三种材料：烟草，纸和胶水。第一个抽烟者进程只有烟草，第二个抽烟者进程只有纸，第三个抽烟者进程只有胶水。供应进程每次随机产生两种材料放倒桌子上，抽烟者进程拿到对应的材料后抽烟，并发送信号给供应者进程继续供应。

抽烟者：检查材料 －> 抽烟 -> 发送信号
供应者：供应材料 -> 等待信号

```C++
semophore offer1 = offer2 = offer3 = 0; // 每一个offer都对应两种材料，简化逻辑
semophore finish = 0; // 抽完的信号

procedure Smoker_i(){
	
	while(1){
		P(offer_i);
		smoke;
		V(finish); // 发送信号
	}
}

procedure Producer(){
	
	while(1){
		random = ramdom() % 3;
		if(random == 0)			V(offer1);
		else if(random == 1)	V(offer2);
		else 					V(offer3);
		// 将材料放到桌子上
		P(finish);  // 等待信号
	}
}

```
