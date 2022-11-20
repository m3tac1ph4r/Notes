## Access Modifiers :

Access modifiers is used to tell the scope of variable, function and etc.

There are three types of access modifiers :

1. Public
2. Private
3. Protected

#### Public :

If we set access modifiers as public in the class then _we can access the functions and variables inside the class and outside the class_.

#### Private :

Private is **by default** in the class.
If we set access modifier as private in the class then _we can access the functions and variables only inside the class._

### Protected :

Protected modifier is similar as **private** modifier like you can use them only inside the class. But you have one advantage in protected that **you can access protected modifier in child class, means you can access protected variable or function in inheritance.**

```cpp

class base
{
	protected:
	string name="UPES";
	public:
	int num;

	void print()
	{
		cout<<"Name : "<<name<<endl;
	}
};
class derive: public base // here public is the mode of inheritance
{
	void print_base()
	{
		cout<<"Base Class : "<<name<<endl;
	}
};
int main()
{
	derive obj;
	obj.print_base();
	return 0;
}
```

## Getters and Setters :

#### Getter :

Getter is a function by which can use private members of class outside the class.
In the below example we have a class name **game**. And two variables level and health. Level is public and health is private. As we know we can't access private members of class outside. So we created a function **getHealth()** which will return health. As we know private members are accessbile inside the class so we will not get error in getHealth().

```cpp

class game{
	public:
	char level;
	private:
	int health;

	int getHealth()
	{
		return health;
	}
	void setHealth(int main_health)
	{
		health=main_health;
	}
};
int main()
{
	game obj1;
	int health=obj1.getHealth();
	// int health=obj1.health; will give error bcz health is private
	cout<<health<<endl;
	int main_health=70;
	obj1.setHealth(main_health);
	// obj1.health=70; will give error bcz it health is private
	return 0;
}
```

### Setter :

Setter is a function by which we can modify the private members of class outside the class.
In the below example we have a class name **game**. And two variables level and health. Level is public and health is private. As we know we can't access private members of class outside. So we created a function **setHealth()** in which we will pass a value for health. As we know private members are accessbile inside the class so we will not get error in getHealth().

```cpp

class game{
	public:
	char level;
	private:
	int health;

	int getHealth()
	{
		return health;
	}
	int
};
int main()
{
	game obj1;
	int health=obj1.getHealth();
	// int health=obj1.health; will give error bcz it is private
	cout<<health<<endl;
	return 0;
}
```

## Dynamically Allocated object :

We can create dynamically allocated object.

```cpp

class XYZ{
	public:
	int health;
	char level;

	int getHealth(){
		return health;
	}
};
int main()
{
	XYZ *obj1=new XYZ;
	cout<<(*obj1).getHealth()<<endl; // Method1 to call member of class
	cout<<obj1->getHealth()<<endl;   // Method2 to call member of class
	return 0;
}
```

## Constructor :

1. Invoke at the time of **object creation**
2. It does not have any return type
3. Constructor have same name as class
4. Constructors provides value to the variables of class

There are two types of constructor :

1. Default Constructor - does not have any parameter
2. Paramaterised Construcrtor - will have parameters

> **Copy Constructor uses Shallow Copy**

#### Shallow Copy :

In shallow copy we uses same memory address with more than one object.

```cpp

class XYZ{
	public:
	int health;
	string level;
}
```

## Destructor :

- Destructor have same name as class but also have **~** for ex : **~ClassName**
- In Static Allocation the destructor is called automatically

## static :

The **static keyword** in Java is used for memory management mainly. We can apply static keyword with variables, methods, blocks and nested classes. The static keyword belongs to the class than are an instance of the class.

1. **static variable:**

   - The static variable can be used to refer to the common property of all objects (which is not unique for each object), for example, the company name of employees, college name of students, etc.
   - The static variable gets memory only once in the class area at the time of class loading.
   - How to intialize the static variable in class. There are two ways to intialize the static variable in class
     ```cpp
     // METHOD 1
     class student
     {
     	public:
     	string name;
     	static string college="UPES";
     };
     int main()
     {
     	// we can access college variable without creating object
     	cout<<student::college<<endl;
     	return 0;
     }
     //
     class student
     {
     	public:
     	string name;
     	static string college;
     };
     string student::college="UPES"; // dataType className::variable_name="value";
     int main()
     {
     	// we can access college variable without creating object
     	cout<<student::college<<endl;
     	return 0;
     }
     ```

2. **static function :**
   - We can call static function without creating object.
   - static function does not have **this** keyword. Because **this keyword is pointer to current object** and we don't have object so this keyword will not work.
   - static functions can access only static members.


## Friend Function :
Friend functions are those functions that have the right to access the private data members of class even though they are not defined inside the class. It is necessary to write the prototype of the friend function. One main thing to note here is that if we have written the prototype for the friend function in the class it will not make that function a member of the class. An example program to demonstrate the concept of friend function is shown below.

### Properties of Friend Function :
1. Not in the scope of class
2. Since it is not in the scope of the class, so cannot be called using object of that class.
3. Can be invoked without the help of any object.
4. Usually cantains the object as arguments.

```cpp
#include<iostream>
using namespace std;

// 1 + 4i
// 5 + 8i
// -------
// 6 + 12i 
class Complex{
    int a, b;
    friend Complex sumComplex(Complex o1, Complex o2);
    public:
        void setNumber(int n1, int n2){
            a = n1;
            b = n2;
        }

        // Below line means that non member - sumComplex funtion is allowed to do anything with my private parts (members)
        void printNumber(){
            cout<<"Your number is "<<a<<" + "<<b<<"i"<<endl;
        }
};

Complex sumComplex(Complex o1, Complex o2){
    Complex o3;
    o3.setNumber((o1.a + o2.a), (o1.b+o2.b))
    ;
    return o3;
}

int main(){
    Complex c1, c2, sum;
    c1.setNumber(1, 4);
    c1.printNumber();

    c2.setNumber(5, 8);
    c2.printNumber();

    sum = sumComplex(c1, c2);
    sum.printNumber();

    return 0;
}
```


## Friend Class :
Friend classes are those classes that have permission to access private members of the class in which they are declared. The main thing to note here is that if the class is made friend of another class then it can access all the private members of that class. An example program to demonstrate friend classes in C++ is shown below.

```cpp
// C++ program to demonstrate the working of friend class

#include <iostream>
using namespace std;

// forward declaration
class ClassB;

class ClassA {
    private:
        int numA;

        // friend class declaration
        friend class ClassB;

    public:
        // constructor to initialize numA to 12
        ClassA() : numA(12) {}
};

class ClassB {
    private:
        int numB;

    public:
        // constructor to initialize numB to 1
        ClassB() : numB(1) {}
    
    // member function to add numA
    // from ClassA and numB from ClassB
    int add() {
        ClassA objectA;
        return objectA.numA + numB;
    }
};

int main() {
    ClassB objectB;
    cout << "Sum: " << objectB.add();
    return 0;
}
```


## Virtual Function :

- A virtual function is a member function  which *is declared within base class* and is *re-defined(Overriden) by derived class*.
- When you refer to a derived class object using a **pointer** or a reference to the base class, you can call a *virtual function* for that object and execute the derived class's version of the function.
- They are mainly used to acheive *Runtime Polymorphism*
- Functions are declared with a *virtual* keyword in base class.

```cpp
// CPP program to illustrate
// concept of Virtual Functions

#include<iostream>
using namespace std;

class base {
public:
	virtual void print()
	{
		cout << "print base class\n";
	}

	void show()
	{
		cout << "show base class\n";
	}
};

class derived : public base {
public:
	void print()
	{
		cout << "print derived class\n";
	}

	void show()
	{
		cout << "show derived class\n";
	}
};

int main()
{
	base *bptr;
	derived d;
	bptr = &d;

	// Virtual function, binded at runtime
	bptr->print();

	// Non-virtual function, binded at compile time
	bptr->show();
	
	return 0;
}
```

>print derived class
>show base class


**real world example of virtual function :**

```cpp
#include <iostream>

using namespace std;

class Animal
{
    public:
    virtual void eat()
    {
        cout<<"This is Base Eat"<<endl;
    }
};
class Dog:public Animal
{
    public:
    void eat()
    {
        cout<<"This is Dog eat"<<endl;
    }
};
class Cat:public Animal
{
    public:
    void eat()
    {
        cout<<"This is cat eat"<<endl;
    }
};
void function(Animal* obj)
{
    obj->eat();
}
int main()
{
    Animal *obj;
    Cat objcat;
    Dog objdog;
    obj=&objdog;
    function(obj);
    return 0;
}
```

## Pure Virtual Function and Abstract Class :

* Sometimes implementation of all function cannot be provided in a base class because we don't know the implementation. Such a class is called *abstract class.*
* A **pure virtual function (or Abstract function)** in C++ is a virtual function for which *we don't have the implementation*, we only *declare it*  in the base class. A pure virtual is declared *by assigning 0 in declaration*.
* A class is **abstract** if it has at least one pure virtual function.
* If we do not override the pure virtual function in derived class, then derived class also becomes abstract class.