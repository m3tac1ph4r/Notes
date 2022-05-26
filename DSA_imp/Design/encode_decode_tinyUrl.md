# Encode and Decode TinyUrl

TinyURL is a URL shortening service where you enter a URL such as `https://leetcode.com/problems/design-tinyurl` and it returns a short URL such as `http://tinyurl.com/4e9iAk`. Design a class to encode a URL and decode a tiny URL.

There is no restriction on how your encode/decode algorithm should work. You just need to ensure that a URL can be encoded to a tiny URL and the tiny URL can be decoded to the original URL.

Implement the `Solution` class:

-   `Solution()` Initializes the object of the system.
-   `String encode(String longUrl)` Returns a tiny URL for the given `longUrl`.
-   `String decode(String shortUrl)` Returns the original long URL for the given `shortUrl`. It is guaranteed that the given `shortUrl` was encoded by the same object.

**Example 1:**

**Input:** url = "https://leetcode.com/problems/design-tinyurl"
**Output:** "https://leetcode.com/problems/design-tinyurl"

**Explanation:**
Solution obj = new Solution();
string tiny = obj.encode(url); // returns the encoded tiny url.
string ans = obj.decode(tiny); // returns the original url after deconding it.

### Approach (Using Hashing) :

We will use map for hashing. Key will be shortUrl and value will be bigUrl.
* **ShortUrl :** We will create URL using number. 
	```  "http://tinyurl.com/" +(number)```
	
```C++
class Solution {
public:
    map<string,string> mp;
    int n=0;
    // Encodes a URL to a shortened URL.
    string encode(string longUrl) {
        string res="http://tinyurl.com/"+to_string(n);
        n++;
        mp[res]=longUrl;
        return res;
    }

    // Decodes a shortened URL to its original URL.
    string decode(string shortUrl) {
        return mp[shortUrl];
    }
};
```

### Question :

https://leetcode.com/problems/encode-and-decode-tinyurl/

### Reference:
https://www.youtube.com/watch?v=fPh7VOdIPjA&ab_channel=TechAdorabyNivedita