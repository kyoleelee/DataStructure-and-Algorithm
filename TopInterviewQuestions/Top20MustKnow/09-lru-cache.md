# LRU Cache
> Source: LintCode (https://www.lintcode.com/problem/134/)
## Problem Description
```
Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and set.

    get(key) Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
    set(key, value) Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

Finally, you need to return the data from each get.
Example

Example1

Input:

LRUCache(2)

set(2, 1)

set(1, 1)

get(2)

set(4, 1)

get(1)

get(2)

Output: [1,-1,1]

Explanation：

cache cap is 2，set(2,1)，set(1, 1)，get(2) and return 1，set(4,1) and delete (1,1)，because （1,1）is the least use，get(1) and return -1，get(2) and return 1.

Example 2:

Input：

LRUCache(1)

set(2, 1)

get(2)

set(3, 2)

get(2)

get(3)

Output：[1,-1,2]

Explanation：

cache cap is 1，set(2,1)，get(2) and return 1，set(3,2) and delete (2,1)，get(2) and return -1，get(3) and return 2.
```

## C++ Solution
1. LRU design problem  
2. See code comments for detail  

Time Complexity: O(1)  
Space Complexity: O(n)  
 
```
#include <iostream> 
#include <list> 
#include <iterator> 
using namespace std; 

class LRUCache {
public:
    /*
    * @param capacity: An integer
    */LRUCache(int capacity) {
        size = capacity;
    }

    /*
     * @param key: An integer
     * @return: An integer
     */
    int get(int key) {
        // 1. if key is not exist return -1
        auto it = keyListMap.find(key);
        if (it == keyListMap.end()) {
            return -1;
        }
        
        // 2. key is exist
        //   - put the key-value pair to the top of listNode
        //   - return the value 
        listNode.splice(listNode.begin(), listNode, it->second);
        return it->second->second;
    }

    /*
     * @param key: An integer
     * @param value: An integer
     * @return: nothing
     */
    void set(int key, int value) {
        // 1. if the key is exist
        //   - update the key-value with the new input value
        //   - put the key-value pair to the top of list and return
        auto it = keyListMap.find(key);
        if (it != keyListMap.end()) {
            it->second->second = value;
            listNode.splice(listNode.begin(), listNode, it->second);
            return;
        }
        
        // 2. keyListMap size equals the LRUCache capacity
        //   - remove the last key-value pair from listNode
        //   - delete the last key from keyListMap
        if (keyListMap.size() == size) {
            int keyToRemove = listNode.back().first;
            listNode.pop_back();
            keyListMap.erase(keyToRemove);
        }
        
        // 3. key is not exist and size is enough
        //   - add the input key-value to top of listNode
        //   - insert the key to keyListMap
        listNode.emplace_front(key, value);
        keyListMap[key] = listNode.begin();
    }
    
    
private:
    int size;

    // key-value pair saved in a List (double linked-list) 
    // new inserted key-value always in the top of List
    list<pair<int, int>> listNode;
    
    // hash map
    // key is the input key
    // value is the key-value pair list iterator
    // hash map key maps the list node of key-value pair
    unordered_map<int, list<pair<int, int>> :: iterator> keyListMap;
};
```
 