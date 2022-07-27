# Stable Array Interview Series -59 GFG

![[stable_arr_1.png]]

![[stable_arr_2.png]]


### Approach :

1. We will calculate frequency of elements
2. Then sort them in ascending order
3. Then we will start a for loop
	1. Find number of elements which are greater than equal to x
		1. Find the index of first  frq which is greater than equal to x. 
			*int index=lower_bound(frq.begin(),frq.end(),x)-frq.begin();*
		2. Then find how many elements are there whose frequencies is less than x 
			*int num_of_ele=frq.size()-index;*
	2. Then find how many elements will be deleted  whose frequency is greater than x
		**ans=min(ans,n-(num_of_ele*x));**

```cpp
  int stableArray(vector<int>& a){
      //Code Here
      map<int,int> mp;
      int n=a.size();
      for(int i=0;i<n;i++)
      {
          mp[a[i]]++;
      }
      vector<int> frq;
      for(auto it:mp)
          frq.push_back(it.second);
      sort(frq.begin(),frq.end());
      int ans=n+1;
      for(int x:frq)
      {
          int index=lower_bound(frq.begin(),frq.end(),x)-frq.begin();
          int num_of_ele=frq.size()-index;
          ans=min(ans,n-(num_of_ele*x));
      }
      return ans;
  }
```


### Question :
https://practice.geeksforgeeks.org/contest/interview-series-59/problems/#