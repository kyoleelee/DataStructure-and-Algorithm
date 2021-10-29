# Graph Valid Tree
> Source: LintCode (https://www.lintcode.com/problem/178/)
## Problem Description
```
Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to check whether these edges make up a valid tree.

You can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.
Example

Example 1:

Input: n = 5 edges = [[0, 1], [0, 2], [0, 3], [1, 4]]
Output: true.

Example 2:

Input: n = 5 edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]]
Output: false.
```

## C++ Solution
1. Union and Find  
2. First to create a UnionFindSet data structure class  
3. Loop through all edges, if find return false, otherwise union  
4. Check if the final union set is 1 or not, 1 means it's a valid tree  

Time Complexity: Union O(1) Find O(1)   
Space Complexity: O(n)  
 
```
class UnionFindSet {
public:
    UnionFindSet(int n) {
        father = vector<int>(n + 1, 0);
        for (int i = 0; i < father.size(); ++i) {
            father[i] = i;
        }
        numOfSet = n;
    }
    
    void Union(int a, int b) {
        int root_a = Find(a);
        int root_b = Find(b);
        if (root_a != root_b) {
            father[root_a] = root_b;
            numOfSet--;
        }
    }
    
    int Find(int x) {        
        if (x != father[x]) {
            father[x] = Find(father[x]);        
        }
        return father[x];
    }
    
    bool Connected(int a, int b) {
        return Find(a) == Find(b);
    }
    
    int GetNumOfSet() {
        return numOfSet;
    }
    
private:
    vector<int> father;
    int numOfSet;
};


class Solution {
public:
    /**
     * @param n: An integer
     * @param edges: a list of undirected edges
     * @return: true if it's a valid tree, or false
     */
    bool validTree(int n, vector<vector<int>> &edges) {
        UnionFindSet ufs(n);
        for (const auto edge : edges) {
            if (ufs.Connected(edge[0], edge[1])) {
                return false;
            }
            ufs.Union(edge[0], edge[1]);
        }
        
        return ufs.GetNumOfSet() == 1 ? true : false;
    }
};
```
