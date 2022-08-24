# Python Interview Important Questions


### 1.  What are lists and tuples? What is the key difference between the two?
**Lists** and **Tuples** are both **sequence data types** that can store a collection of objects in Python. The objects stored in both sequences can have **different data types**. Lists are represented with **square brackets** `['sara', 6, 0.19]`, while tuples are represented with **parantheses** `('ansh', 5, 0.97)`.

But the real difference between the two ? The key difference between the two is that **lists are mutable** and **tuples are immutable**. This means the list can be modified, appended or sliced.
But tuple remains constant and cannot be modified in any manner. 

![[listvstuple.png]]


### 2. Can we use set as a key in dictionary ?
-Currently, Python has two built-in set types - **set** and **frozenset**. **set** type is mutable and supports methods like `add()` and `remove()`. **frozenset** type is immutable and can't be modified after creation.

**set** - Mutable unordered collection of distinct hashable objects.
**frozenset** - Immutable collection of distinct hashable objects.

**Note:** `_set_` _is mutable and thus cannot be used as key for a dictionary. On the other hand,_ `_frozenset_` _is immutable and thus, hashable, and can be used as a dictionary key or as an element of another set.

### 3.  What is pass in Python?

The `pass` keyword represents a null operation in Python. It is generally used for the purpose of filling up empty blocks of code which may execute during runtime but has yet to be written. Without the **pass** statement in the following code, we may run into some errors during code execution.

```python
def myEmptyFunc():
   # do nothing
   pass
myEmptyFunc()    # nothing happens
## Without the pass keyword
# File "<stdin>", line 3
# IndentationError: expected an indented block
```


### 4. What are modules and packages in Python?

Python packages and Python modules are two mechanisms that allow for **modular programming** in Python. Modularizing has several advantages -

-   **Simplicity**: Working on a single module helps you focus on a relatively small portion of the problem at hand. This makes development easier and less error-prone.
-   **Maintainability**: Modules are designed to enforce logical boundaries between different problem domains. If they are written in a manner that reduces interdependency, it is less likely that modifications in a module might impact other parts of the program.
-   **Reusability**: Functions defined in a module can be easily reused by other parts of the application.
-   **Scoping**: Modules typically define a separate namespace, which helps avoid confusion between identifiers from other parts of the program.


### 5. How is memory managed in Python?

-   Memory management in Python is handled by the **Python Memory Manager**. The memory allocated by the manager is in form of a **private heap space** dedicated to Python. All Python objects are stored in this heap and being private, it is inaccessible to the programmer. Though, python does provide some core API functions to work upon the private heap space.
-   Additionally, Python has an in-built garbage collection to recycle the unused memory for the private heap space.

### 6. What is lambda in Python? Why is it used?
Lambda is an anonymous function in Python, that can accept any number of arguments, but can only have a single expression. It is generally used in situations requiring an anonymous function for a short time period.

### 7. Difference between shallow copy() and deepcopy()
https://www.geeksforgeeks.org/copy-python-deep-copy-shallow-copy/

In shallow copy the value  changed is  reflected to the actual object.
But in deep copy the value changed is not reflected to the actual object.

### 8. How Python is interpreted?

-   Python as a language is not interpreted or compiled. Interpreted or compiled is the property of the implementation. Python is a bytecode(set of interpreter readable instructions) interpreted generally.
-   Source code is a file with .py extension.
-   Python compiles the source code to a set of instructions for a virtual machine. The Python interpreter is an implementation of that virtual machine. This intermediate format is called “bytecode”.
-   .py source code is first compiled to give .pyc which is bytecode. This bytecode can be then interpreted by the official CPython or JIT(Just in Time compiler) compiled by PyPy.

### 9.What does * args and ** kwargs mean?

#### Things to Remember:

-   * args and ** kwargs are special keyword which allows function to take variable length argument.
-   * args passes variable number of non-keyworded arguments and on which operation of the tuple can be performed.
-   ** kwargs passes variable number of keyword arguments dictionary to function on which operation of a dictionary can be performed.
-   * args and ** kwargs make the function flexible.

```python
def adder(*num):
    sum = 0
    
    for n in num:
        sum = sum + n

    print("Sum:",sum)

adder(3,5)       #Sum: 8
adder(4,5,6,7)   #Sum: 12
adder(1,2,3,5,6) #Sum: 17
```

```python
def intro(**data):
    print("\nData type of argument:",type(data))

    for key, value in data.items():
        print("{} is {}".format(key,value))

intro(Firstname="Sita", Lastname="Sharma", Age=22, Phone=1234567890)
intro(Firstname="John", Lastname="Wood", Email="johnwood@nomail.com", Country="Wakanda", Age=25, Phone=9876543210)
```

```
Data type of argument: <class 'dict'>
Firstname is Sita
Lastname is Sharma
Age is 22
Phone is 1234567890

Data type of argument: <class 'dict'>
Firstname is John
Lastname is Wood
Email is johnwood@nomail.com
Country is Wakanda
Age is 25
Phone is 9876543210
```

https://www.programiz.com/python-programming/args-and-kwargs


### 10. What is init method in python?

The **init** method works similarly to the constructors in Java. The method is run as soon as an object is instantiated. It is useful for initializing any attributes or default behaviour of the object at the time of instantiation

