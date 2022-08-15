# Valid Palindrome II

Given a string 's', return 'true' _if the_ 's' _can be palindrome after deleting **at most one** character from it_.

**Ex 1 :-**
**Input:** s = "aba"
**Output:** true

**Ex 2 :-**
**Input:** s = "abca"
**Output:** true
**Explanation:** You could delete the character 'c'.

**Ex 3 :-**
**Input:** s = "abc"
**Output:** false

### Approach 1 (two pointer)

1. We will take two pointer **i** (start) and **j** (end) . We will intialize i=0 and j=n-1
2. Now take one variable for counting how many character skipped from starting. Suppose we take count=0
3. If _string[i] == string[j]_ then increase i and decrease j
4. else if _string[i] ! string[j]_ then increase i and count . As we are skipping the charachter string[i].
5. Now in the question it is clearly mentioned we have to only skip one charachter. So we will check if(count>1) then **break**
6. Sometimes if we delete char from ending then string will be palindrome.
   for ex : s=**cbbcc** So here if we delete char from starting it will not be palindrome.
   If we delete last char then it will be a palindrome.
7. So we will do all the steps 1 to 5 for ending. In ending we will decrease j when charachter doesn't matches.

```cpp
bool validPalindrome(string s) {
     int i=0,j=s.length()-1;
        int count=0;
        while(i<=j)
        {
            if(s[i]==s[j])
            {
                i++;
                j--;
            }
            else
            {
                i++;
                count++;
            }
            if(count>1)
                break;
		}
        i=0,j=s.length()-1;
        int count1=0;
        while(i<=j)
        {
            if(s[i]==s[j])
            {
                i++;
                j--;
            }
            else
            {
                count1++;
                j--;
			}
            if(count1>1)
                break;
		}
        if(count==0||count1==0)		// string is already palindrome
            return true;
        else if(count==1||count1==1)
			// string will be palindrome after deleteing one char
            return true;
        return false;
}
```

### Approach 2 (recursion) :-

```cpp
    bool check_palindrome(string s,int i,int j)
    {
        while(i<=j)
        {
            if(s[i]==s[j])
            {
                i++;
                j--;
            }
            else
                return false;
        }
        return true;
}
	// base function
    bool validPalindrome(string s) {
        int i=0,j=s.length()-1;
        while(i<=j)
        {
            if(s[i]==s[j])
            {
                i++;
                j--;
            }
            else
                return (check_palindrome(s,i+1,j)||check_palindrome(s,i,j-1));
}
        return true;
    }
```

### Question :-

https://leetcode.com/problems/valid-palindrome-ii/
