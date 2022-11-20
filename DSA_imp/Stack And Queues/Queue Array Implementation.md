# Array Implementation of Queue :


### Simple Approach :

```cpp
#include <iostream>
using namespace std;

int arr[100];
int size=100;
int front=-1,rear=-1;
void push(int x)
{
    if(front==size-1)
        std::cout << "Queue OverFlow" << std::endl;
    front++;
    arr[front]=x;
}
void pop()
{
    int ans;
    if(front==-1)
    {
        cout<<"Queue Empty"<<endl;
        ans=-1;
    }
    else
    {
        ans=arr[0];
        for(int i=0;i<front;i++)
            arr[i]=arr[i+1];
    }
    cout<<ans<<endl;
}
int main()
{
    pop();
    push(10);
    push(20);
    push(30);
    pop();
    push(50);
    pop();
    pop();
    
    return 0;
}
```

>**Time Complexity :** O(1) for PUSH and O(N) for POP


### Optimize Approach (Using Circular Array):
1. *front is for POP*
2. *rear is for PUSH*

```cpp
#include <iostream>

using namespace std;
int arr[100];
int cap=100;
int front=0;
int size=0; // size will tell the current size of queue
int getRear()
{
    if(size==0)
        return -1;
    else
        return (front+size-1)%cap;
}
void push(int x)
{
    if(size==cap)
        std::cout << "Queue OverFlow" << std::endl;
    int rear=getRear();
    rear=(rear+1)%cap;
    arr[rear]=x;
    size++;
}
void pop()
{
    int ans;
    if(size==0)
    {
        cout<<"Queue Empty"<<endl;
    }
    else
    {
        front=(front+1)%cap;
        size--;
    }
}
int main()
{
    pop();
    push(10);
    push(20);
    push(30);
    pop();
    push(50);
    pop();
    pop();
    
    return 0;
}

```

>**Time Complexity :** O(1) for PUSH and O(1) for POP


### Queue Implementation Using Linkedlist :

```cpp
//{ Driver Code Starts
#include<bits/stdc++.h>
using namespace std;

struct QueueNode
{
    int data;
    QueueNode *next;
    QueueNode(int a)
    {
        data = a;
        next = NULL;
    }
};

struct MyQueue {
    QueueNode *front;
    QueueNode *rear;
    void push(int);
    int pop();
    MyQueue() {front = rear = NULL;}
};

//Function to push an element into the queue.
void MyQueue:: push(int x)
{
        // Your Code
        QueueNode* temp=new QueueNode(x);
        if(front==NULL)
        {
            front=temp;
            rear=temp;
            return;
        }
        rear->next=temp;
        rear=temp;
}

//Function to pop front element from the queue.
int MyQueue :: pop()
{
        // Your Code
        if(front==NULL)
            return -1;
        QueueNode* temp=front;
        front=front->next;
        if(front==NULL)
            rear=NULL;
        
        int ans=temp->data;
        delete(temp);
        return ans;
}
```

