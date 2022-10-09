

# Stack Implementation using Array
### Code :
```cpp
void MyStack :: push(int x)
{
    // Your Code
    top++;
    arr[top]=x;
}

//Function to remove an item from top of the stack.
int MyStack :: pop()
{
    // Your Code
    if(top==-1)
        return -1;
    return arr[top--];
}
```


### Question :
https://practice.geeksforgeeks.org/problems/implement-stack-using-array/1


# Stack Implementation using Linkedlist :

### Code :

```cpp
void MyStack ::push(int x) 
{
    // Your Code
    StackNode *tmp=new StackNode(x);
    tmp->next=top;
    top=tmp;
}

//Function to remove an item from top of the stack.
int MyStack ::pop() 
{
    // Your Code
    if(top==NULL)
        return -1;
    int ans=top->data;
    top=top->next;
    return ans;
}
```


## Question :
https://practice.geeksforgeeks.org/problems/implement-stack-using-linked-list/1