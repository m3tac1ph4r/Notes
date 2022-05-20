### Z Algorithm(Linear time pattern searching)

This is algorithm is same as Rabin Karp algorithm. 
The main difference between Rabin Karp and Z algorithm is in time complexity.

| Algorithm   | Worst Case  |
| ----------- | ----------- |
| Rabin Karp  | O(mn)       |
| Z algorithm | O(m+n)      |


In this algorithm we construct Z array.

#### Z-Array
For example :- s="abcaba"

| a | b  |c | a | b | a |
|---|---|---|---|---|---|
| 0 | 1  |2 | 3 | 4 | 5|

Now the Z array would be:

| 0 |  0|  0|  2|  0|  1|
|---|---|---|---|---|---|

The values in Z-array are called **Z values**

Now I will explain how to find the Z values.
Firstly Z[0] will always be 0. We will start index from **1** .  

```
At index=1 'b' is not equal to s[0] i.e 'b'!='a' so, Z[1]=0
At index=2 'c' same it is also not equal so,Z[2]=0
At index=3 'a' it is equaled to s[0] i.e 'a' is a prefix new_text
	Now we will increase count to 1 bcz new_text[0]==new_text[index] i.e 'a'=='a'
	Again we will increase count to 2 bcz new_text[1]==new_text[index+1] i.e
	'b'=='b'
	new_text[2]!=new_text[index+1] so it means we will store count to Z[3]=2
	
At index=4 'b' is not equal to 'b'!='a' so, Z[4]=0
At index=5 'a' is equal to 'a'(new_text[0])
	Now we will increase count to 1. As index was last so we will store Z[5]=1(count) {as 'a' is the prefix of new_text}
```

So the summary of the above is that we have to store how many characters are the prefix of new_text from that index.


As we can see that we have to check the string from index to n and i to n in worst case which is equal to O(n^2)

To overcome this we store the previous computed values if we got the match of current char is prefix or not. This will do the algorithm in O(n+m).

>So now question comes how we copy precomputed values into new ?

This **if(k > right)** will be false when we have a match of prefix and is greater than equal to the pattern. So it will not find the upcoming values as he knows there might be a substring which is matched with current string text[k..right]. So it will just copy the elements from  that substring.
This **if (Z[k1]< right - k + 1)** will be true when the charachter which we are searching for prefix is not the last charachter of window size [left..right] . So if the charachter is not last char then we will copy the precomputed values.
```C++
int k1 = k - left;
if (Z[k1] < right - k + 1)
{
Z[k] = Z[k1];
}
```

So if it is last char of the window then it will  resize the window to [k..right] and then again check for the prefix is there or not.


![[z algo approach.png]]

#### Code: 

```C++
int zAlgorithm(string s,string p,int n,int m)
{
    string new_s=p+'$'+s;
    int new_len=new_s.length();
    int Z[new_len];
    Z[0] = 0;
    int left = 0, right = 0;
    for (int k = 1; k < new_len; k++)
    {
        if (k > right)
        {
            left = k;
            right = k;
            while (right < new_len and new_s[right] == new_s[right - left])
            {
                right++;
            }
            Z[k] = right - left;
            right--;
        }
        else
        {
            int k1 = k - left;
            if (Z[k1] < right - k + 1) //copy precomputed values
            {
                Z[k] = Z[k1];
            }
            else
            {
                left = k;
                while (right < new_len and new_s[right] == new_s[right - left])
                {
                    right++;
                }
                Z[k] = right - left;
                right--;
            }
        }
    }
    int count=0;
    for(int i=0;i<new_len;i++)
    {
        if(Z[i]==p.length())
            count++;
    }
    return count;
}    
int main()
{
    string s,p;
    cin>>s;
    cin>>p;
    cout<<zAlgorithm(s,p,s.length(),p.length());
    return 0;
}
```


### Resources

* If you want to dry run and find how Z-array is made for any string then check out this link.
[*https://personal.utdallas.edu/~besp/demo/John2010/z-algorithm.htm*](https://personal.utdallas.edu/~besp/demo/John2010/z-algorithm.htm)

* For understanding how Z-algorithm works try this video.
	[*https://youtu.be/CpZh4eF8QBw*](https://youtu.be/CpZh4eF8QBw)

### Questions
* Coding Ninjas : [*https://www.codingninjas.com/codestudio/problems/1112619*](https://www.codingninjas.com/codestudio/problems/1112619)