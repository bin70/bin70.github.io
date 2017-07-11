---
title: quickSort
date: 2017-07-11 19:17:23
tags: algorithm, c++
---

快排的核心在partition，它先选取一个枢轴(pivot)，然后想办法把它放到一个位置，使得它左边的数都比它小，右边的都比它大。

qsort函数递归调用自己，因此外封装一个quickSort函数。代码中注释部分为第一次写快排犯下的错误，今后需要多多注意。

代码如下：

```c++
#include<iostream>
#include<fstream>

using namespace std;

struct List{
	int size;
	int arr[100];
};

void swap(List* L, int low, int high){
	int temp;
	temp = L->arr[low];
	L->arr[low] = L->arr[high];
	L->arr[high] = temp;
}

int partition(List* L, int low, int high){
	int pivotkey = L->arr[low];  // select first element as pivot
	while(low<high)   // missing this cannot sort same elements 
	{
		while(low<high && L->arr[high] >= pivotkey) // >= not >
			high--;
		swap(L, low, high);
		while(low<high && L->arr[low] <= pivotkey)
			low++;
		swap(L, low, high);
	}
	return low;
}

void qsort(List* L, int low, int high){
	int pivot;
	if(low<high){   // missing this will segment fault
		pivot = partition(L, low, high);
		qsort(L, low, pivot-1);
		qsort(L, pivot+1, high);
	}
}

void quickSort(List* L){
	qsort(L, 0, L->size-1);
}

int main(){
	fstream input("input.txt");
	if(!input.is_open()){
		cout << "cannot open." << endl;
	}
	List L;
	int i=0;
	while(input >> L.arr[i++]){
		L.size = i;
	}
	quickSort(&L);
	for(int j=0; j<L.size; j++){
		cout << L.arr[j] << " ";
	}
	cout << endl;
}
```

