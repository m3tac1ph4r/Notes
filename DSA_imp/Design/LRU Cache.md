# LRU CACHE


Design a data structure that follows the constraints of a **[Least Recently Used (LRU) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU)**.

Implement the `LRUCache` class:

-   `LRUCache(int capacity)` Initialize the LRU cache with **positive** size `capacity`.
-   `int get(int key)` Return the value of the `key` if the key exists, otherwise return `-1`.
-   `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the `capacity` from this operation, **evict** the least recently used key.

The functions `get` and `put` must each run in `O(1)` average time complexity.


**Example 1:**

**Input**
[ "LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[ [2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
**Output**
[null, null, null, 1, null, -1, null, -1, 3, 4]

**Explanation**
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4



### Approach 1 (Using Double Linkedlist and Hashtable) :

```cpp
class LRUCache {
public:
    class Node
    {
      public:
        int key,val;
        Node* next;
        Node* prev;
        Node(int _key,int _val)
        {
            key=_key;
            val=_val;
        }
    };
    Node* head=new Node(-1,-1);
    Node* tail=new Node(-1,-1);
    int cap;
    unordered_map<int,Node*> m;
    LRUCache(int capacity) {
        cap=capacity;
        head->next=tail;
        tail->prev=head;
    }
    void addNode(Node* newNode)
    {
        Node* temp=head->next;
        newNode->next=temp;
        newNode->prev=head;
        head->next=newNode;
        temp->prev=newNode;
    }
    
    void deleteNode(Node* delNode)
    {
        Node* oldPrev=delNode->prev;
        Node* oldNext=delNode->next;
        oldPrev->next=oldNext;
        oldNext->prev=oldPrev;
}
    
    int get(int key_check) {
        if(m.find(key_check)!=m.end())
        {
            Node* resNode=m[key_check];
            int res=resNode->val;
            m.erase(key_check);
            deleteNode(resNode);
            addNode(resNode);
            m[key_check]=head->next;
            return res;
        }
        return -1;
    }
    
    void put(int key_check, int value) {
        if(m.find(key_check)!=m.end())
        {
        Node* oldNode=m[key_check];
            m.erase(key_check);
            deleteNode(oldNode);
        }
        if(m.size()==cap)
        {
            m.erase(tail->prev->key);
            deleteNode(tail->prev);
        }
        addNode(new Node(key_check,value));
        m[key_check]=head->next;
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```


### Reference :
https://youtu.be/xDEuM5qa0zg

### Question :
https://leetcode.com/problems/lru-cache/