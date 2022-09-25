# BINARY SEARCH

## Introduction

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

## Standard Problems

- Floor

  ```cpp
  int floor(vector<int> v, int k){
      int n = v.size();
      int s=0, e=n-1;
      int ans = n, res;
      while(s<=e){
          int mid = s+(e-s)/2;
          if(v[mid]==k) return mid;
          else if(v[mid]<k){
              ans = mid;
              s = mid+1;
          } else{
              e = mid-1;
          }
      }
      return ans;
  }
  ```

- Find Element in rotated Sorted Array

  ```cpp
  int solve(vector<int> v, int k){
      int n=v.size();
      int s=0, e=n-1;
      while(s<=e){
          int mid=s+(e-s)/2;
          if(v[mid]==k) return mid;
          if(v[mid]>v[0] and k>=v[0] and k<v[mid]) e = mid-1;
          else s = mid+1;
      }
      return -1;
  }
  ```

- First and last occurence of element

  ```cpp
  void sol_stl(vector<int> v, int k){
      int x = lower_bound(v.begin(), v.end(), k) - v.begin();
      int y = upper_bound(v.begin(), v.end(), k) - v.begin();
      cout<<x<<" "<<y-1<<endl;
  }

  void solve(vector<int> v, int k){
      int s=0, e=v.size()-1;
      int fo=-1;
      while(s<=e){
          int mid = s + (e-s)/2;
          if(v[mid]==k){
              fo = mid;
              e = mid-1;
          }
          else if(v[mid]<k) s = mid+1;
          else e = mid - 1;
      }

      s = 0, e = v.size()-1;
      int lo=-1;
      while(s<=e){
          int mid = s + (e-s)/2;
          if(v[mid]==k){
              lo = mid;
              s = mid+1;
          }
          else if(v[mid]<k) s = mid+1;
          else e = mid - 1;
      }
      cout<<fo<<" "<<lo<<endl;
  }
  ```

- Search element in Bitonic Array

  Bitonic Array => first monotonically increasing then monotonically decreasing  
  Not a rotated sorted array  
  monotonic => arr[i+1]>arr[i] AND NOT arr[i+1]>=arr[i]  
  bitonic array => can never become sorted

  ```cpp
  int search(vector<int> v, int k){
      int n = v.size();
      int s=0, e=n-1;
      int p = peak(v);

      int x = lower_bound(v.begin(), v.begin()+p, k) - v.begin();
      int y = lower_bound(v.begin()+p, v.end(), k, greater<int>()) - v.begin();

      if(x!=p) return (v[x]==k) ? x : -1;
      if(y!=n) return (v[y]==k) ? y : -1;

      return -1;

  }
  ```

- Peak Element

  ```cpp
  int peak(vector<int> v){
      int n = v.size();
      int l=0, h=n-1;
      while(l<=h){
          int mid = l + (h-l)/2;
          if(mid-1>=0 and v[mid-1]>v[mid]) h=mid-1;
          else if(mid+1<n and v[mid+1]>v[mid]) l=mid+1;
          else return mid;
      }
      return -1;
  }
  ```

- Nth root

  ```cpp
  double multiply(double num, int n){
      double ans = 1;
      for(int i=0;i<n;i++) ans*=num;
      return ans;
  }

  double findNthRootOfM(int n, long long m) {
      double l=1, h=m;
      double br = 1e-6;
      while(h-l > br){
          double mid = l + (h-l)/2.0;
          if(multiply(mid, n)<m){
              low=mid;
          } else{
              high=mid;
          }
      }
      return l;
  }
  ```

- Number of rotations

  ```cpp
  // index of min element = no. of rotations
  int solve(vector<int> v){
      int n = v.size();
      int s=0, e=n-1;
      while(s<=e){
          int mid = s + (e-s)/2;
          if(v[mid]<v[(mid+1)%n] and v[mid]<v[(mid-1+n)%n]) return mid;
          else if(v[mid]>v[0]) s = mid+1;
          else e = mid-1;
      }
      return -1;
  }
  ```

- Median of two sorted arrays

  ```cpp
  double findMedianSortedArrays(vector<int>& v1, vector<int>& v2) {
      if(v2.size()<v1.size()) return findMedianSortedArrays(v2, v1);
      int n1 = v1.size();
      int n2 = v2.size();
      int l = 0, h = n1;
      int med = (n1+n2+1)/2
      while(l<=h){
          int c1 = l+(h-l)/2;
          int c2 = med-c1;
          int l1 = c1==0 ? INT_MIN : v1[c1-1];
          int l2 = c2==0 ? INT_MIN : v2[c2-1];
          int r1 = c1>=n1 ? INT_MAX : v1[c1];
          int r2 = c2>=n2 ? INT_MAX : v2[c2];

          if(l1<=r2 and l2<=r1){
              if((n1+n2)&1) return max(l1,l2);
              else return (max(l1,l2) + min(r1,r2))/2.0;
          }
          else if(l1>r2) h=c1-1;
          else l=c1+1;
      }
  return 0.0;
  }
  ```

- Kth largest in two sorted arrays

  ```cpp
  int solve(vector<int> &v1, vector<int> &v2, int m, int n, int k) {
      // Write your code here.,
      if(m>n) return solve(v2, v1, n, m, k);

      int l=max(0,k-n), h=min(k,m);
      while(l<=h){
          int c1 = (l+h)>>1;
          int c2 = k-c1;

          int l1 = c1==0 ? INT_MIN : v1[c1-1];
          int l2 = c2==0 ? INT_MIN : v2[c2-1];
          int r1 = c1>=m ? INT_MAX : v1[c1];
          int r2 = c2>=n ? INT_MAX : v2[c2];

          if(l1<=r2 and l2<=r1) return max(l1, l2);
          else if (l1>r2) h=c1-1;
          else l=c1+1;
      }
      return 0;
  }
  ```

- Aggressive Cows

  ```cpp
  bool canPlace(vector<int> &v, int k, int n){
      // cout<<endl<<k<<"->"<<n<<"cows : ";
      int p = v[0];
      int ans = 1;
      for(int i=1;i<v.size();i++){
          // cout<<v[i]<<" ";
          if(v[i]-p>=k){

              ans++;
              if(ans>=n) return 1;
              p=v[i];
          }
      }
      // cout<<"false";
      return 0;
  }

  void solve(){
      int n, k;
      cin>>n>>k;
      vector<int> stalls(n);
      for(int i=0;i<n;i++) cin>>stalls[i];
      sort(stalls.begin(), stalls.end());

      int l=0, h=stalls[n-1];
      int ans = 0;
      while(l<=h){
          int mid = (l+h)>>1;
          if(!canPlace(stalls, mid, k)) h=mid-1;
          else {
              ans = mid;
              l=mid+1;
          }
      }
      cout<<ans<<endl;
  }
  ```

- Allocate Minimum Pages

  ```cpp
  bool isValid(vector<int> v, int n, int k){
      int i = 0;
      int csum = 0;
      int sn=0;
      while(i<v.size()){
          if(csum+v[i]<=n){
              csum += v[i++];
              continue;
          } else{
              sn++;
              csum=v[i++];
              if(sn==k) return 0;
          }
      }
      return sn==k-1 ? 1 : 0;
  }

  void solve(){
      int n;
      cin>>n;
      vector<int> v(n);
      for(int &x : v) cin>>x;
      int k;
      cin>>k;
      int s = *max_element(v.begin(), v.end());
      int e = accumulate(v.begin(), v.end(), 0);
      int res = -1;
      while(s<=e){
          int mid = s + (e-s)/2;
          if(isValid(v, mid, k)){
              res = mid;
              e=mid-1;
          }
          else s = mid+1;
      }
      cout<<res<<endl;
  }
  ```
