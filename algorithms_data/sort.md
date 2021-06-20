# 排序算法
## 八大排序算法

==对于排序算法两个点 代码要撸的熟练 时空间复杂度分析==
快排或者归并等不同的写法需要掌握

### 1. BubbleSort
冒泡排序
```cpp
void BubbleSort(int* a, int n){//降序
	for(int j = n - 1; j > 0; j--){
		for(int i = 1; i <= j; i++){
			if(a[i-1] > a[i]){
				swap(a[i-1], a[i]);
			}
		}
	}
}
```
```cpp
//优化做法 加上标志位
void sort(int* a, int n) {
    for (int i = n - 1; i > 0; i--) {
        int flag = 0;
        for (int j = 1; j < i; j++) {
            if (a[i-1] > a[i]) {
                flag = 1;
                swap(s[i-1], a[i]);                
            }
        }
        if (flag = 1) {
            break;
        }
    }
}
```
### 选择排序
选出最大或者最小的交换到排序区间的末尾
```cpp
void SelectSort(int* a, int n) {//降序
	for(int i = 0; i < n-1; i++){
		int min = i;
		for (int j = i+1; j < n; j++){
			if(a[j] < [min]){
				min = j;
			}
		}
		if(min != i){
			swap(a[min], a[i]);
		}
	}
}

```

### 插入排序 -》直接插入和希尔排序
将区间分为两部分 排序和未排序 每次将元素插入到合适位置

```cpp
void InsertSort(int* a, int n ) {
	for (int i = 0; i < n-1; i++) {
		int end = i;
		int tmp = a[end + 1];
		while (end >= 0) {
			if (a[end] > tmp) {
				a[end + 1] = a[end];
				--end;
			}
			else {
				break;
			}
		}	
		a[end+1] = tmp;
	}
}
```

==希尔排序== 缩小增量法
```cpp
void ShellSort(int* a, int n) {
	int gap = n;
	while (gap > 1) {
		gap = gap / 3 + 1;
		for (int i = 0; i < n - gap; i++) {
			int end = i;
			int tmp = a[end + gap];
			while (end >= 0) {
				if (a[end] > tmp) {
					a[end + gap] = a[end];
					end -= gap;
				}
				else {
					break;
				}
			}
			a[end + gap] = tmp;
		}
	}
}

```

### 桶排序
```cpp
#include <stdio.h>
int main()
{
    int a[11],i,j,t;
    for(i=0;i<=10;i++)
        a[i]=0;  
                 
    for(i=1;i<=5;i++)  //循环读入
    {
        scanf("%d",&t);  
        a[t]++; 
    }
    for(i=0;i<=10;i++)  
        for(j=1;j<=a[i];j++)  //循环 打印
            printf("%d ",i);
   system("pause");
    return 0;
}

```
 ### 堆排序 
 对于堆排序 堆的向上和向下调整算法
 堆的插入和删除算法
 堆逻辑上是一个完全二叉树 物理是上是一个数组
 堆从两个方面进行梳理 -》向下 向上调整算法
 向下调整 左右子树分别为大根或者小根堆 (满足堆顶元素最大或者最小即为大根或者小根堆)
 向上调整 当前位置不满足堆的性质
 
 建堆建立在向下调整 (n-2)/2 就是堆顶的位置
 n*2+1 左孩子
 n*2+2 右孩子
 (child-1)/2 左右孩子双亲的位置
 
 ```cpp
 void AdjustDown(int* a, int root, int n) {//建立小堆
	int parent = root;
	int child = parent*2+1;

	while (child < n){
		//调整逻辑
		//首先选出 左右孩子中最大或者最小的  比如建立小堆就要选出更小的那个孩子和parent交换 
		//交换完毕之后 parent和child下标向下更改 一旦正常 break

		if (child + 1 < n && a[child] > a[child+1]) {
			child++;
		}

		if (a[parent] > a[child]) {
			swap(a[parent], a[child]);
			parent = child;
			child = parent*2+1;
		}else {
			break;
		}

	}
}

 ```

 建堆  其实是以n为孩子 进行从低到上的梳理
 ```cpp
 void CreateHeap(int* a, int n) {
	int parent = (n-2)/2;//这个是最小的parent
	while (parent >= 0) {
		AdjustDown(a, parent, n);
		parent--;
	}
}
```

堆排序 
建堆 交换堆顶和堆低元素向下调整
```cpp
void HeapSort(int* a, int n) {
	CreateHeap(a, n);
	while(n > 0) {
		swap(a[0], a[n-1]);
		n--;
		AdjustDown(a, 0, n);
	}
}
```