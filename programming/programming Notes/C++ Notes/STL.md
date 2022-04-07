	


# Vectors

Vector are dynamic arrays in C++ and part of STL.

In vector  we can also add and delete elements at the end in O(1) time.

### TO INTIALIZE VECTOR
```C++
vector<int> v;
```

**OR**

```C++
vector<int> v{10,20,30,40,50,80};
```

### TO INTIALIZE VECTOR WITH INTIAL SIZE

```C++
vector<int> v(30);
```

### TO ADD ELEMENTS FROM THE END

**vector_name.push_back(value);**

```C++
vector<int> v; 
v.push_back(2); // [2] 
v.push_back(3); // [2, 3] 
v.push_back(7); // [2, 3, 7] 
v.push_back(5); // [2, 3, 7, 5]
v[1] = 4; // sets element at index 1 to 4 -> [2, 4, 7, 5]
```


### TO PRINT ELEMENT WHICH IS AT THE LAST
**vector_name.back();**
```C++
// CPP program to illustrate
// Implementation of back() function
#include <iostream>
#include <vector>
using namespace std;

int main()
{
	vector<int> myvector;
	myvector.push_back(3);
	myvector.push_back(4);
	myvector.push_back(1);
	myvector.push_back(7);
	myvector.push_back(2);
	// Vector becomes 3, 4, 1, 7, 2

	cout << myvector.back();
	return 0;
}
```
>**OUTPUT**
>2

### TO PUSH ELEMENT FROM THE FRONT

**vector_name.push_front(value);**

```C++
v.push_front(5);
```

### TO GET THE FIRST ELEMENT OF THE VECTOR
**vector_name.front();**
```C++
// CPP program to illustrate
// Implementation of back() function
#include <iostream>
#include <vector>
using namespace std;

int main()
{
	vector<int> myvector;
	myvector.push_back(3);
	myvector.push_back(4);
	myvector.push_back(1);
	myvector.push_back(7);
	myvector.push_back(2);
	// Vector becomes 3, 4, 1, 7, 2

	cout << myvector.front();
	return 0;
}
```

>**OUTPUT**
>3

### TO DELETE ELEMENT FROM VECTOR

1. vectorname.erase(position)
2. vectorname.erase(startingposition,endingposition)
**vector_name.erase(index);**

```C++
v.erase(v.begin()+1);  // removes element at index 1 -> [2, 7, 5]
v.erase(v.begin(), v.begin()+3); // this erases the first three elements; O(n)
```


### TO PRINT VECTOR USING FOR LOOP

```C++
for(int i = 0; i < v.size(); i++)
{ 
cout << v[i] << " "; 
}
```

### TO SORT THE VECTOR
**sort(vector_name.begin(),vector_name.end());**

```C++
sort(v.begin(), v.end());
```


## IF YOU WANT TO INSERT(INPUT) DATA IN VECTOR OF N SIZE 

You don't need to write for loop like this
```C++
vector<int> v1(n);
int t;
for(int i=0;i<n;i++)
{
	cin>>t;
	v1.push_back(t);	//or v1.insert(t,i);
}
```
	
You can short this code like this

```C++
vector<int> v(n);
for(int &i:v)
	cin>>i;
```



## Make vector pair like map
[example_of_pair_vector](https://usaco.guide/problems/cses-1640-sum-of-two-values/solution)

To intialize the vector
```vector<pair<int,int>>m;```

#### To input values in vector

```C++
for(int i=0;i<n;i++)
{
ll int tmp;
cin>>tmp;
m.push_back({tmp,i+1});
}
/*
n=4
2 7 5 1

2 1
7 2
5 3
1 4
*/
```


#### To print values in vector
```C++
int i=0;
while(i<n)
{
cout<<"First = "<<m[i].first<<"second = "<<m[i].second<<endl;
i++;
}

/*
4 
2 7 5 1
First = 2second = 1
First = 7second = 2
First = 5second = 3
First = 1second = 4
*/
```

# Map

A **map** is a set of ordered pairs, each containing a **key** and a **value**. In a map, all keys are required to be unique, but values can be repeated. Maps have three primary methods:

-   one to add a specified key-value pairing
    
-   one to retrieve the value for a given key
    
-   one to remove a key-value pairing from the map

Insertions,deletion and searches are all O(logN)

In C++ map m:
-   he `m[key] = value` operator assigns a value to a key and places the key and value pair into the map. The operator `m[key]` returns the value associated with the key. If the key is not present in the map, then `m[key]` is set to 0.
    
-   The `count(key)` method returns the number of times the key is in the map (which is either one or zero), and therefore checks whether a key exists in the map.
    
-   Lastly, `erase(key)` removes the map entry associated with the specified key.

```C++
map<int, int> m;

m[1] = 5; // [(1, 5)]

m[3] = 14; // [(1, 5); (3, 14)]

m[2] = 7; // [(1, 5); (2, 7); (3, 14)]

m[0] = -1; // [(0, -1); (1, 5); (2, 7); (3, 14)]

m.erase(2); // [(0, -1); (1, 5); (3, 14)]

cout << m[1] << '\n'; // 5

cout << m.count(7) << '\n' ; // 0

cout << m.count(1) << '\n' ; // 1
```

## Iterating over maps

```C++
for (pair<int,int> x : m) 
{
 cout << x.first << " " << x.second << '\n';
}

for (auto x : m) 
{
 cout << x.first << " " << x.second << '\n';
}

/* both output the following:

0 -1

1 5

3 14

*/
```

## Inserting  and deleting in maps

```C++
void iterate_insert() {

 map<int,int> m; m[0] = 0; //starts with a single key

 for (auto& p: m) { //adds keys in the loop until the key 10

 if (p.first == 10) break;

 p.second = 5;

 m[p.first+1] = 0;

 }

 cout << "ENTRIES:\n";

 for (pair<int,int> p: m)

 cout << p.first << " " << p.second << "\n";

}

/*

ENTRIES:

0 5

1 5

2 5

3 5

4 5

5 5

6 5

7 5

8 5

9 5

10 0

*/
```

	
	
	
# Stack

Stacks are a type of container adaptors with *LIFO(Last In First Out)* type of working

The functions associated with stack are:  
[empty()](https://www.geeksforgeeks.org/stack-empty-and-stack-size-in-c-stl/) – Returns *true* if  the stack is empty – **Time Complexity : O(1)**
[size()](https://www.geeksforgeeks.org/stack-empty-and-stack-size-in-c-stl/) – Returns the size of the stack – **Time Complexity : O(1)**
[top()](https://www.geeksforgeeks.org/stack-top-c-stl/) – Returns a reference to the top most element of the stack – **Time Complexity : O(1)**
[push(g)](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/) – Adds the element ‘g’ at the top of the stack – **Time Complexity : O(1)**   
[pop()](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/) – Deletes the top most element of the stack – **Time Complexity : O(1)**


## Code
```C++
#include <iostream>
#include <stack>
using namespace std;
int main() {
	stack<int> stack;
	stack.push(21);
	stack.push(22);
	stack.push(24);
	stack.push(25);
	
		stack.pop();
	stack.pop();

	while (!stack.empty()) {
		cout << ' ' << stack.top();
		stack.pop();
	}
}
```

>**OUTPUT**
>22 21


## To insert element in pair in stack

We can intialize the stack like vector .
```C++
stack<pair<int,int>> s;
```

Now you have to insert element like this:
```C++
s.push({2,3});
```

More you can see LOVE_BABBAR_DSA Question [**Merge Overlapping intervals**](https://leetcode.com/problems/merge-intervals/)

And its solution in DSA folder


## To get the top element in stack

We can get the top element in stack using **top()**

```C++
stack<int> a;
a.push(10);
a.push(25);
a.push(15);
a.push(20);
int t=a.top(); // it will give us the top element t.e 20
```

