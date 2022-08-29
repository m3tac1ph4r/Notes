# Pillars of OOPS Concept - Inheritance, Polymorphism, Encapsulation and Abstraction

## Encapsulation :
Wrapping up of data members and functions into an single entity. Another way to think about encapsulation is, that it is a protective shield that prevents the data from being accessed by the code outside this shield. 

* What is fully Encapsulated Class ?
	1. All data members are private in this class.

>**Why Encapsulation ? / Advantages** 
>1. We can hide data using encapsulation. 
>2. If we want we can make class read only using getter. We will not create setter in the class.
>3. Code Reusability

> **Difference between Encalpsulation and Abstraction ?**
https://stackoverflow.com/questions/742341/difference-between-abstraction-and-encapsulation

## Inheritance :
Inheritance is the process of inheriting the properties and behavior of an existing class into a new class. When we inherit the class, we can reuse the existing class’s methods and fields into a new class. Inheritance can also be defined as the Is-A relationship, which is also known as the parent-child relationship.

Important terminology of inheritance 
- **Sub Class:** The class that inherits properties from another class is called Subclass or Derived Class.  
- **Super Class:** The class whose properties are inherited by subclass is called Base Class or Superclass.

#### Mode of Inheritance :
When you write **class derive:mode base** instead of mode you have to use publc,protected,private
Syntax :
*class child_class: access_modifier parent_class*

1. **Public mode :** If we derive a subclass from a public base class. Then, the base class’s public members will become public in the derived class, and protected class members will become protected in the derived class.
    Means if the mode of inheritance is **public**

| Base Class Access Specifier | Child Class Access Specifier when mode of inheritance is public |
|-----------------------------|-----------------------------------------------------------------|
| public                      | public                                                          |
| protected                   | protected                                                       |
| private                     | Not Accessible                                                  |
    

2. **Protected mode :** If we derive a subclass from a Protected base class. Then both public members and protected members of the base class will become protected in the derived class.

| Base Class Access Specifier | Child Class Access Specifier when mode of inheritance is protected |
| --------------------------- | --------------------------------------------------------------- |
| public                      | protected                                                          |
| protected                   | protected                                                       |
| private                     | Not Accessible                                                  |

4. **Private mode :** If we derive a subclass from a Private base class. Then both public members and protected members of the base class will become Private in the derived class.

| Base Class Access Specifier | Child Class Access Specifier when mode of inheritance is private |
|-----------------------------|-----------------------------------------------------------------|
| public                      | Not Accessible                                                          |
| protected                   | Not Accessible                                                       |
| private                     | Not Accessible                                                  |

![[inheritance_mode.png]]


#### Types of inheritance :
**1. Single inheritance**
**2. Multi-level inheritance**
**3. Multiple inheritance**
**4. Hierarchical inheritance** 
**5. Hybrid inheritance**

1. **Single inheritance :** In single inheritance, one class can extend the functionality of another class. In single inheritance, there is only one parent class and one child class.
2. **Multi-level inheritance :** When a class inherits from a derived class, and the derived class becomes the base class of the new class, it is called multilevel inheritance. In multilevel inheritance, there is more than one level.
	![[multilevel_inheritance.png]]

3. **Multiple inheritance :** In multiple inheritance, a class can inherit more than one class. This means that in this type of inheritance, *a single child class can have multiple parent classes*.

	![[multiple_inheritance.png]]

```cpp

class parent_class1 {

	//Body of parent class1
};
class parent_class2 {

	//Body of parent class2
};
class child_class: access_modifier parent_class1, access_modifier
parent_class2 {
	//Body of child class
};
```

4. **Hierarchical inheritance :** In hierarchical inheritance, one class serves as a base class for more than one derived class. Means in this type of inheritance *one parent class will have more than one child.*

![[hierarchical inheritance.png]]


```cpp

class parent_class {
	//Body of parent class
};
class child_class1: access_modifier parent_class {
	//Body of child class1
};
class child_class2: access_modifier parent_class {
	//Body of child class2
};
```

5. **Hybrid inheritance :** Hybrid inheritance is a combination of more than one type of inheritance. For example, A child and parent class relationship that follows multiple and hierarchical inheritances can be called hybrid inheritance.

![[hybrid_inheritance.png]]

```cpp

#include <iostream>
using namespace std;
// Parent class1
class Vehicle {
	public:
	Vehicle() {
		cout << "This is a Vehicle" << endl;
	}
	};
	//Parent class2
	class Fare {
	public:
	Fare() {
		cout << "Fare of Vehicle\n";
	}
};
//Child class1
class Car: public Vehicle {

};
//Child class2
class Bus: public Vehicle, public Fare {

};
// main function
int main() {
	// creating object of sub class will
	// invoke the constructor of base class
	Bus obj2;
	return 0;
}

```

**Output:** 
This is a Vehicle 
Fare of Vehicle

#### Inherit Ambiguity :
There may be a possibility that a class may inherit member functions with the same name from two or more base classes, and the derived class may not have functions with the same name as those of its base classes. If the derived class object needs to access one of the same-named member functions of the base classes, it results in ambiguity as it is not clear to the compiler which base’s class member function should be invoked.

```cpp

#include<iostream>
using namespace std;

class A {
    public:
        void abc() {
            cout << "Class A";
        }
};

class B {
    public:
        void abc() {
            cout << "Class B";
        }
};

class C: public A, public B {
    public:
};


//Main Code
int main() {
    C obj;
    obj.abc();
}
```

**Output:**
error: request for member ‘abc’ is ambiguous

>**Avoid ambiguity using scope resolution operator**
The ambiguity can be resolved by using the **scope resolution operator** by specifying the class in which the member function lies as given below:
>```cpp
>object.class_name::method_name();
>```

```cpp
#include<iostream>
using namespace std;

class A {
    public:
        void abc() {
            cout << "Class A";
        }
};

class B {
    public:
        void abc() {
            cout << "Class B";
        }
};

class C: public A, public B {
    public:
};

//Main Code
int main() {
    C obj;
    obj.A :: abc();
}
```

**Output:**
Class A


## Polymorphism :
Polymorphism is a concept that allows you to perform a single action in different ways. Polymorphism is the combination of two Greek words. The poly means **many**, and morphs means **forms**. So polymorphism means **many forms**. Let’s understand polymorphism with a real-life example.
**Real-life example:**  A person at the same time can have different characteristics. Like a man at the same time is a father, a husband, and an employee. So the same person possesses different behavior in different situations. This is called polymorphism.

##### **Types of polymorphism**

There are two types of polymorphism in C++.
-   Compile-time polymorphism
-   Runtime polymorphism

1. **Compile Time Polymorphism :**
Compile time polymorphism is also known as static polymorphism. This type of polymorphism can be achieved through function overloading or operator overloading.

- **Function overloading :**
When there are multiple functions in a class with the same name but different parameters, these functions are overloaded. The main advantage of function overloading is it increases the readability of the program. 
Functions can be overloaded by using 
<pre>
	1. different numbers of arguments
	2. by using different types of arguments.
</pre>

* Different number of arguments :
```cpp
#include <iostream>
using namespace std;
// Function with two parameters
int add(int num1, int num2) {
return num1 + num2;
}
// Function with three parameters
int add(int num1, int num2, int num3) {
return num1 + num2 + num3;
}
int main() {
cout << add(10, 20) << endl;
cout << add(10, 20, 30);
1
return 0;
}
```

**Output:** 
30 60

- Different types of arguments :
```cpp

#include <iostream>
using namespace std;
// Function with two integer parameters
int add(int num1, int num2) 
{
	return num1 + num2;
}
// Function with two double parameters
double add(double num1, double num2) 
{
	return num1 + num2;
}
int main(void) 
{
	cout << add(10, 20) << endl;
	cout << add(10.4, 20.5);
	return 0;
}
```

* **Operator Overloading :**

![[operator_overloading_img.png]]

2. **Run Time Polymorphism :**

Runtime polymorphism is also known as dynamic polymorphism. Method overriding is a way to implement runtime polymorphism.

* **Method Overriding :**
Method overriding is a feature that allows you to redifine the parent class method in the child class based on its requirement. In other words, whatever methods the parent class has by default are available in the child class. But sometimes a child class may not be satisfied with parent class method implementation. The child class is allowed to redifine that method based on its requirement. This process is called method overriding.

**Rules for method overriding :**

* The method of the parent class and the method of the child class must have the same name.
* The method of the parent class and the method of the child class must have the same parameters.

![[method_overriding_code.png]]


## Abstaraction :
