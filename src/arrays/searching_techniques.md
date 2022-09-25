# Searching Techniques

## Linear Search

```cpp
int linearSearch(vector<int> a, int key)
{
	for(int i=0;i<a.size();i++)
	{
		if(a[i] == key)
			return i;
	}
	return -1;
}
```

## Binary Search

```cpp
int binary_search(vector<int> v, int key){
	int s=0, e=v.size()-1;
	while(s<=e){
		int mid = s + (e-s)/2;
		if(v[mid]==key) return mid;
		else if(v[mid]<key) s = mid+1;
		else e = mid-1;
	}
	return -1;
}
```
