    # C++ TIPS

## To intialize the array in C++

```cpp
int num[5] = {1, 1, 1, 1, 1};
```

---

## Use unordered set when you need to find the exist element

You can take help from **CSES TWO_SET PROBLEM**

- To find element in unordered set

```cpp
unordered_set<int> arr1;
if (arr1.find(i) != arr1.end())
	cout<<"FOUND"<<endl;
else
{
	cout<<"NOT FOUND"<<endl;
}
```

- To print the unordered SET

```cpp
unordered_set<int>::iterator itr;
for (itr = arr1.begin(); itr != arr1.end(); itr++)
	cout << (*itr) << " ";
```

OR YOU CAN USE AUTO IN FOR LOOP

```cpp
for(auto element : v)
{
cout << element; //prints the values in the vector
}
```

---

## To divide the number n in two set of equal sum

Find the sum of n natural number and divide it by 2
Check two_set problem in CSES

```
sum=(n*(n+1))/4
```

## To find sum of n natural numbers:

```
sum=(n*(n+1))/2
```

## To convert char to string

```cpp
string s(1, x);
```

where 1 means number of char and x is char

## To get each charachter of string

```cpp
string  s="Hello";
for(char d : s)
{
	cout<<d<<endl;
}
```

---

## To print string vector

To print string vector there is one method

```cpp
vector<string> ans;
for(string a : ans)
	cout<<a<<endl;
```

## To print permutation

[link](https://www.geeksforgeeks.org/permutations-of-a-given-string-using-stl/)

We can use STL for printing permutation.

```cpp
string s="aabac";
sort(s.begin(),s.end());
do
{
cout << s << endl;
} while (next_permutation(s.begin(),s.end()));
```

You can take help from **CSES CREATING_STRINGS_PROBLEM**

---

## INT_MAX and INT_MIN

If we want to find minimum value then we should intialize the variable with
**INT_MAX** and if wr have to find maximum value then intialize with **INT_MIN**
GFG:-
We usually assign a high value to MIN to compute minimum value in an array. But if an array has large elements, we must assign the highest possible value to the array.

```cpp
int a=INT_MAX;
int b=INT_MIN;
```

---

## To find $2^n$ :

We can use 1<<n to find $2^n$

```cpp
  int n=3;
  for(int j=0;j<(1<<n);j++)
  {
    cout<<j<<endl;
  }
```

---

## Find binary of decimal

```c++
std::string binary = std::bitset<n>(i).to_string();
```

where n is no bit like
if n=8
then binary of 2 will be 00000010
if n=3
then binary of 2 will be 010

---

## Find subsequence or subset of array or n numbers

We can use # BITMASK to find subset

Like we have 3 numbers a,b,c
So their subset will be

> a
> b
> c
> ab
> ac
> bc
> abc

We have total_combination=($2^n$ -1)

i.e n=3
total_combination =8-1 => 7

---

## To find sum of array

For this we can use stl function accumulate(arr,arr+n,sum)

```cpp
n=3;
int arr[n]={2,4,6};
ll int total_sum=0;
total_sum=accumulate(arr,arr+n,total_sum);
```

---

## USE VECTOR INSTEAD OF STRING

If you are getting time exceed using string use vector instead of that.

See last two palindrome_reorder submission in cses

---

## To print reverse Vector

```cpp
for(int p=v.size()-1;p>=0;p--)
cout<<v[p];
```

---

## TO SORT ARRAY

```cpp
sort(arr, arr + N) // where N is size of array
```

---

## TO SORT ARRAY IN DESCENDING ORDER

```cpp
sort(arr, arr + N,greater<int>());
```

---

## Use else if instead more than if

Don't use if like this

```cpp
if(cond.)
	statement1;
if(cond.)
	statement2;
if(cond.)
	statement3;
```

Use else if

```cpp
if(cond.)
	statement1;
else if(cond.)
	statement2;
else if(cond.)
	statement3;
```

---

## Use one for loop instead of two

If you want to find the maximum and minimum element in subarray of 4.
Example : A[]={3, 4, 1, 9, 56, 7, 9, 12}
Output:- (1,7),(9,56)

Then we will make subarray of size of 4 like this

{1,3,4,7} and {9,9,12,56}
Minimum and Maximum in subarray 1 =(1,7)
Minimum and Maximum in subarray 2=(9,56)

If we do this in two for loop then code will be

```cpp
for(int i=0;i<n;i++)
{
	int max=A[i];
	int min=A[i];
	for(int j=i;j+4<n;j++)
	{
		if(A[j]<min)
		min=A[j];
		if(A[j]>max)
		max=A[j];
	}
cout<<"("<<min<<","<<max<<")"<<endl;
}
```

So we can do this in one for loop like this:
But we have to sort the array before this for loop.

```cpp
m=4;
for(int i=0;i+m-1<n;i++)
{
	min=A[i];
	max=A[i+m-1];
	cout<<"("<<min<<","<<")"<<endl;
}
```

So we can reduce two for loop into one.

---

## TERNARY OPERATOR

**Syntax: **

> variable = (condition) ? expressionTrue: expressionFalse;

**Example :**

```cpp
int time = 20;
if (time < 18) {
 cout << "Good day.";
} else {
 cout << "Good evening.";
}
```

You can simply write this to ternary operator.

```cpp
int time = 20;
string result = (time < 18) ? "Good day." : "Good evening.";
cout << result;
```

---

## To delete specific character from string

```cpp
string tmp="mkd";
tmp.erase(remove(tmp.begin(), tmp.end(), 'd'), tmp.end());
cout<<tmp<<endl; //output --> mk
```

---

## To input string with spaces

```cpp
string s;
getline(cin,s);
```

## To remove all the spaces in string

```cpp
string s;
getline(cin,s);
s.erase(remove(s.begin(), s.end(), ' '), s.end());
```

## To find prime numbers optimally and faster

Use [Seive of Eratosthenes algorithm](https://www.youtube.com/watch?v=nDPo9hsDNvU)

## How to sort map by values

We will use vector pair to sort map

```cpp
bool comp(pair<string,int>& a,pair<string,int>& b)
{
 return a.second>b.second;
}
int main()
{
unordered_map<string, int> m;
 vector<pair<string, int>> A;
 for (int i = 0; i < n; i++)
 {
 m[arr[i]]++;
 }
 for (auto &i : m)
 	A.push_back(i);
 sort(A.begin(), A.end(), comp);
}
```
