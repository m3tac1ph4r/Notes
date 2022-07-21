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

Protected modifier is similar as **private** modifier like you can them only inside the class. But you have one advantage in protected that **you can access protected modifier in child class, means you can access protected variable or function in inheritance.**

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

The **static keyword** in [Java](https://www.javatpoint.com/java-tutorial) is used for memory management mainly. We can apply static keyword with [variables](https://www.javatpoint.com/java-variables), methods, blocks and [nested classes](https://www.javatpoint.com/java-inner-class). The static keyword belongs to the class than an instance of the class.

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

# Questions :

1. **How much byte does an empty class object will have ?**
   1 byte. Compiler will give 1 byte to empty class object for track.
