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

```

### 堆排序

```C++

```

## 树

### 先序遍历
### 中序遍历
### 后序遍历
### 层序遍历
### Binary Search
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
### 经典DP

