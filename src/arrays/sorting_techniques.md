# SORTING TECHNIQUES

## Introduction

```cpp
sort(v.begin(), v.end());
```

```cpp
sort(v.begin(), v.end(), greater<int>());
```

```cpp
bool compare(int a, int b)
{
	return a<b;
	//toggle sign to see variation in output
}

//we will pass our own comparator function into user defined sorting function
void bubbleSort(int a[], int n, bool (&cmp)(int a, int b))
{
	for(int i=0;i<n;i++)
	{
		for(int j=0;j<n-i-1;j++)
		{
			if(cmp(a[j],a[j+1]))
				swap(a[j],a[j+1]);
		}
	}
}
```

```cpp
bool customComparator(){}

sort(v.begin(), v.end(), customComparator());
```

## Bubble Sort

```cpp
void bubbleSort(vector<int> &a, int n){
	for(int i=0;i<n-1;i++){
		for(int j=0;j<n-i-1;j++){
			if(a[j]>a[j+1]) swap(a[j], a[j+1]);
		}
	}
}
```

## Selection Sort

```cpp
void selectionSort(vector<int> &v, int n){
	for(int i=0;i<n-1;i++){
		int mini = i;
		for(int j=i+1;j<n;j++){
			if(v[j]<v[mini]) mini = j;
		}
		swap(v[i], v[mini]);
	}
}
```

## Insertion Sort

```cpp
void insertionSort(vector<int> &v, int n){
	for(int i=1;i<n;i++){
		int x = v[i];
		int j=i-1;
		while(j>=0 and v[j]>x){
			v[j+1] = v[j];
			j--;
		}
		v[j+1]=x;
	}
}
```

## Merge Sort

```cpp
void merge(vector<int> &v, int l, int m, int r){
	int x = m-l+1, y = r-m;
	vector<int> a(x), b(y);
	for(int i=0;i<x;i++) a[i] = v[l+i];
	for(int j=0;j<y;j++) b[j] = v[m+j+1];

	int i=0, j=0, k=l;
	while(i<x and j<y){
		if(a[i]<b[j]) v[k++] = a[i++];
		else v[k++] = b[j++];
	}
	while(i<x) v[k++] = a[i++];
	while(j<y) v[k++] = b[j++];
}

void mergeSort(vector<int> &v, int l, int r){
	if(l<r){
		int mid = l + (r-l)/2;
		mergeSort(v, l, mid);
		mergeSort(v, mid+1, r);
		merge(v, l, mid, r);
	}
}
```

## Quick Sort

```cpp
int partition(vector<int> &v, int l, int r){
	int i = l-1;
	int pivot = v[r];

	for(int j=l;j<r;j++){
		if(v[j]<pivot){
			i++;
			swap(v[i], v[j]);
		}
	}
	swap(v[i+1], v[r]);
	return i+1;
}

void quickSort(vector<int> &v, int l, int r){
	if(l<r){
		int p = partition(v, l, r);
		quickSort(v, l, p-1);
		quickSort(v, p+1, r);
	}
}
```
