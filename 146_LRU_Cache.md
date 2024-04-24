Design a data structure that follows the constraints of a Least Recently Used (LRU) cache.  

Implement the LRUCache class:  

LRUCache(int capacity) Initialize the LRU cache with positive size capacity.  
int get(int key) Return the value of the key if the key exists, otherwise return -1.  
void put(int key, int value) Update the value of the key if the key exists. Otherwise, add the key-value pair to the cache. If the number of keys exceeds the capacity from this operation, evict the least recently used key.  
The functions get and put must each run in O(1) average time complexity.  

Example 1:  
```
Input
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
Output
[null, null, null, 1, null, -1, null, -1, 3, 4]

Explanation
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
```

Code:  
```c++
class Node {
public:
    int key, value;
    Node* prev;
    Node* next;

    Node(int k, int v) {
        key = k;
        value = v;
    }
};

class LRUCache {
private:
    Node* head;
    Node* tail;
    map<int, Node*> k_n;
    int capacity;
public:
    LRUCache(int capacity) {
        this -> capacity = capacity;
        head = new Node(-1, -1);
        tail = new Node(-1, -1);
        head -> next = tail;
        tail -> prev = head;
    }
    
    int get(int key) {
        if(k_n.find(key) == k_n.end()) return -1;

        Node* reNode = k_n[key];

        reNode -> prev -> next = reNode -> next;
        reNode -> next -> prev = reNode -> prev;

        reNode -> prev = head;
        reNode -> next = head -> next;

        head -> next -> prev = reNode;
        head -> next = reNode;

        return reNode -> value;
    }
    
    void put(int key, int value) {
        Node* newNode;
        if(k_n.find(key) != k_n.end()) {
            newNode = k_n[key];
            newNode -> value = value;

            newNode -> prev -> next = newNode -> next;
            newNode -> next -> prev = newNode -> prev;

            newNode -> prev = head;
            newNode -> next = head -> next;
        
            head -> next -> prev = newNode;
            head -> next = newNode;
        }
        else {
            if(k_n.size() >= capacity) {
                Node* rmNode = tail -> prev;
                tail -> prev = rmNode -> prev;
                rmNode -> prev -> next = tail;
                k_n.erase(rmNode -> key);
                delete rmNode;
            }
            
            newNode = new Node(key, value);
            k_n[key] = newNode;

            newNode -> prev = head;
            newNode -> next = head -> next;
        
            head -> next -> prev = newNode;
            head -> next = newNode;
        }
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```

Performance:  
Time: 338 ms, Beats 71.01% of users with C++.  
Memory: 169.09 MB, Beats 68.56% of users with C++.  
