# 2D Arrays

```cpp
vector<vector<int>> v(n, vector<int> (m));
```

## Standard Problems

- Different types of prints

  ```cpp
  //WAVE PRINT
  //col is even we go top down
  //col is odd we go bottom up
  for(int i=0;i<c;i++)
  {
      if(i%2 == 0)
      {
          for(int j=0;j<r;j++)
          cout<<a[j][i]<<" ";
      }

      else
      {
          for(int j=r-1;j>=0;j--)
          cout<<a[j][i]<<" ";
      }
  }
  //SNAKE PATTERN
  //it is similar to wave print in horizontal fashion

  //SPIRAL PRINT
  //we have to traverse the array in spiral fashion
  cout<<endl<<endl;
  int startRow = 0;
  int startCol = 0;
  int endRow = r-1;
  int endCol = c-1;

  while(startRow<=endRow and startCol<=endCol)
  {
      //printing startRow
      for(int i=startCol; i<=endCol; i++)
          cout<<a[startRow][i]<<" ";

      startRow++;

      //printing the endCol
      for(int i=startRow; i<=endRow; i++)
          cout<<a[i][endCol]<<" ";

      endCol--;

      //print the endRow
      if(startRow<endRow){
          for(int i=endCol;i>=startCol;i--)
              cout<<a[endRow][i]<<" ";

          endRow--;
      }

      //print the startCol
      if(startCol<endCol){
          for(int i = endRow; i>=startRow; i--)
              cout<<a[i][startCol]<<" ";

          startCol++;
      }
  }
  ```

- Rotate Image

  ```cpp
  void rotate(int a[][100], int n)
  {

      //reverseal of rows
      for(int i=0;i<n;i++)
      {
          // int startCol = 0;
          // int endCol = n-1;
          // while(startCol<endCol)
          // 	swap(a[i][startCol++],a[i][endCol--]);

          //stl reverse
          reverse(a[i],a[i]+n);
      }

      //transposing the revrsed row matrix
      for(int i=0;i<n;i++)
      {
          for(int j=0;j<n;j++)
          {
              if(i<j)
                  swap(a[i][j],a[j][i]);
          }
      }
  }
  ```

- Staircase Search

  ```cpp
  void staircaseSearch(int a[][100], int n, int key)
  {
      int f = 0;
      int i = 0;
      int j = n-1;

      while(i!=n-1 || j!=0)
      {
          if(a[i][j] == key)
          {
              f = 1;
              break;
          }
          if(a[i][j]>key)
              j--;
          else
              i++;
      }
      if(f==0)
          cout<<"Key not found";

      else
          cout<<"Key found at index"<<i<<" "<<j;
  }
  ```

- Matrix Multiplication

  ```cpp
  void multiply(int mat1[][N],
              int mat2[][N],
              int res[][N],int n)
  {
      int i, j, k;
      for (i = 0; i < n; i++)
      {
          for (j = 0; j < n; j++)
          {
              res[i][j] = 0;
              for (k = 0; k < n; k++)
                  res[i][j] += mat1[i][k] *
                              mat2[k][j];
          }
      }
  }
  ```

- Submatrix Sum

  ```cpp
  int main()
  {


      int a[N][N];
      int preSum[N][N];
      int n;
      cin>>n;
      for(int i=0;i<n;i++)
      {
          for(int j=0;j<n;j++)
          {
              cin>>a[i][j];
              preSum[i][j] = a[i][j];
          }
      }

      for(int i=0;i<n;i++)
      {
          for(int j=1;j<n;j++)
              preSum[i][j] += preSum[i][j-1];
      }
      for(int j=0;j<n;j++)
      {
          for(int i=1;i<n;i++){
              preSum[i][j] += preSum[i-1][j];
          }
      }
      int t;
      cin>>t;
      while(t--)
      {
          int tli,tlj,bri,brj;
          cin>>tli>>tlj>>bri>>brj;
          // to find sum of submatrix fo coresponding top left and bottom right
          int s1 = preSum[bri][brj];
          int s2 = (tli==0) ? 0 : preSum[tli-1][brj];
          int s3 = (tlj==0) ? 0 : preSum[bri][tlj-1];
          int s4 = (tli==0 || tlj==0) ? 0 : preSum[tli-1][tlj-1];
          cout<<s1<<" "<<s2<<" "<<s3<<" "<<s4<<endl;
          int res = s1 - s2 - s3 + s4;
          cout<<res<<endl;

      }
      return 0;
  }
  ```

- Max Sum Submatrix

  ```cpp
  int main()
  {

      int a[N][N];
      int suffSum[N][N];
      int n;
      cin>>n;
      for(int i=0;i<n;i++)
      {
          for(int j=0;j<n;j++)
          {
              cin>>a[i][j];
              suffSum[i][j] = a[i][j];
          }
      }

      for(int i=n-1;i>=0;i--)
      {
          for(int j=n-2;j>=0;j--)
              suffSum[i][j] += suffSum[i][j+1];
      }

      for(int j=n-1;j>=0;j--)
      {
          for(int i=n-2;i>=0;i--)
              suffSum[i][j] += suffSum[i+1][j];
      }
      //suffix sum array is created
      int max = INT_MIN;
      int x,y;
      for(int i=0;i<n;i++)
      {
          for(int j=0;j<n;j++)
          {
              if(suffSum[i][j]>max)
              {
                  max = suffSum[i][j];
                  x = i;
                  y = j;
              }
          }
      }

      cout<<"Submatrix is :-"<<endl;
      cout<<"Top Left : "<<x<<" "<<y<<endl;
      cout<<"Bottom Right : "<<n-1<<" "<<n-1<<endl;
      cout<<"Sum : "<<max;
      return 0;
  }
  ```
