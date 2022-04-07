In this File you will get example code which I was not getitng in a code snippet



## In apple_division CSES if(i&(1<<j)) explain

In the below code you will see how this if condition works and find all possible permution
https://usaco.guide/CPH.pdf#page=57

> Thus i & (1<<j) will return a positive value only if the j'th bit is turned on in mask. 

```C++
#include<bits/stdc++.h>
using namespace std;s
int main()
{
  int n=5;
  int arr[5]={3,2,7,4,1};
  set<int> g1;
  set<int> g2;
  cout<<"Array has:  3 2 7 4 1"<<endl;
  for(int i=0;i<(1<<n);i++)
  {
    for(int j=0;j<n;j++)
    {
      if(i&(1<<j))
      {
        cout<<"inserting "<<arr[j]<<" in the g1"<<endl;
        cout<<"i = "<<i<<" j = "<<j<<endl;
        g1.insert(arr[j]);
      }
      else
        g2.insert(arr[j]);
    }
    cout<<"Group 1:"<<endl;
    set<int>::iterator itr1;
    for(itr1=g1.begin();itr1!=g1.end();itr1++)
      cout<<*itr1<<" ";
    cout<<endl;
    cout<<"Group 2:"<<endl;
    for(itr1=g2.begin();itr1!=g2.end();itr1++)
      cout<<*itr1<<" ";
    cout<<endl;
    set<int>::iterator e1;
    set<int>::iterator e2;
    e1=g1.begin();
    e2=g1.end();
    g1.erase(e1,e2);
    e1=g2.begin();
    e2=g2.end();
    g2.erase(e1,e2);
    cout<<"----------------------------------------------------------------------------------------"<<endl;
  }
}
```



--------------------------------------------------------------------