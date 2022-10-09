# Union of Two Sorted Arrays :




### Code :

```cpp
#include<bits/stdc++.h>
using namespace std;

int main()
{
    vector<int> a={1,2,2,3,4,5,5,6};
    vector<int> b={2,2,3,3,5,6,6};
    int minLen=a.size()<b.size()?a.size():b.size();
    int i=0,j=0;
    while(i<a.size() && j<b.size())
    {
        if(i>0 && a[i]==a[i-1])
            i++;
        if(j>0 && b[j]==b[j-1])
            j++;
        else if(a[i]<b[j])
        {
            cout<<a[i]<<" ";
            i++;
        }
        else if(b[j]<a[i])
        {
            cout<<b[j]<<" ";
            j++;
        }
        else if(a[i]==b[j])
        {
            cout<<a[i]<<" ";
            i++;
            j++;
        }
    }
    return 0;
}

```