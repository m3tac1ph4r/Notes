# Bitwise Operator in C++

There are six bitwise operator in C++

1. & (bitwise AND)
2. | (bitwise OR)
3. ~ (bitwise NOT)
4. << (left shift)
5. `>>` (right shift)
6. ^ (XOR)

## Bitwise AND (&)

Resukt of AND is 1 when both bits are 1

```
7 ---> 0 1 1 1
4 --> &0 1 0 0

4  <-- 0 1 0 0

7 & 4 = 4
```

```cpp
int main()
{
int x=1,y=2; //x= 1(0000 0001),y=2(0000 0010)
if(x&y)       // 1&2= 0(0000 0000)
	cout<<"Result of x&y is 1"<<endl;
if(x&&y)
	cout<<"Result of x&&y is 1";
}
```

---

## Bitwise OR(|)

Result of OR is 0 when both bits are 0

```
7 ---> 0 1 1 1
4 --> &0 1 0 0

7  <-- 0 1 1 1

7 | 4 = 7
```

---

## Left Shift Operator(<<)

```
 	First_Operand <<  Second_Operand
		|					|
		|					|
  Whose bits get 	Decides the number of places
 	shifted    			to shift the bits
```

**Important Points :**

- When bits are shifted left then trailing positions are filled with zeros

  ![[left_shift_1.png]]

- Left shifting is equivalent to multiplication by $2^right_operand$

  ![[left_shift_2.png]]

---

## Right Shift Operator(>>)

```
First_Operand >> Second_Operand
```

**Important Points :**

- When bits are shifted right then leading positions are filled with zeros

![[right_shift_1.png]]

One 1 will be truncated

- Right shifting is equivalent to division by 2^right_operand
  ![[right_shift_2.png]]

---

## Bitwise XOR Operator (^)

Before we understand XOR operator we should know OR operator

![[XOR.png]]

So in OR operator

> if A=0 and B=0 then A|B=0
> if A=1 and B=0 then A|B=1

But in XOR operator it is exclusive OR means

> if A=0 and B=0 then A^B=0
> if A=1 and B=0 then A^B=0

Result of XOR is 1 when both bits are different

```
7 ---> 0 1 1 1
4 ---> 0 1 0 0

3 <--- 0 0 1 1

7^4=3
```
