# Knight Shortest Path
> Source: LintCode (https://www.lintcode.com/problem/611/)
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
1. BFS  
2. Here sample solution uses bidirectional bfs to optimize the time complexity  

Time Complexity: O(n*m)
Space Complexity: O(n)  
 
```
/**
 * Definition for a point.
 * struct Point {
 *     int x;
 *     int y;
 *     Point() : x(0), y(0) {}
 *     Point(int a, int b) : x(a), y(b) {}
 * };
 */

int DIRECTIONS[8][2] = 
{
    {1, 2},
    {1, -2},
    {-1, 2},
    {-1, -2},
    {2, 1},
    {2, -1},
    {-2, 1},
    {-2, -1}
};

class Solution {
public:
    /**
     * @param grid: a chessboard included 0 (false) and 1 (true)
     * @param source: a point
     * @param destination: a point
     * @return: the shortest path 
     */
    int shortestPath(vector<vector<bool>> &grid, Point &source, Point &destination) {
        if (grid.size() == 0 || grid[0].size() == 0) return -1;
        if (grid[destination.x][destination.y] == 1) return -1;
        if (source.x == destination.x && source.y == destination.y) return 0;
        
        int len_route = 0;
        queue<Point> forwardQueue;
        queue<Point> backwardQueue;
        vector<vector<bool>> forwardSet(grid.size(), vector<bool>(grid[0].size(), 0));
        vector<vector<bool>> backwardSet(grid.size(), vector<bool>(grid[0].size(), 0));
        
        forwardQueue.push(source);
        backwardQueue.push(destination);
        forwardSet[source.x][source.y] = 1;
        backwardSet[destination.x][destination.y] = 1;
        
        while (!forwardQueue.empty() && !backwardQueue.empty()) {
            len_route++;
            if (findNext(grid, forwardQueue, forwardSet, backwardSet)) {
                return len_route;
            }
            
            len_route++;
            if (findNext(grid, backwardQueue, backwardSet, forwardSet)) {
                return len_route;
            }
        }
        
        return -1;
    }
    
    bool findNext(const vector<vector<bool>>& grid, queue<Point>& curQueue, vector<vector<bool>>& sourceSet, vector<vector<bool>>& destSet) {
        int size = curQueue.size();
        while (size--) {
            int curX = curQueue.front().x;
            int curY = curQueue.front().y;
            curQueue.pop();
            
            for (int i = 0; i < 8; i++) {
                int nextX = curX + DIRECTIONS[i][0];
                int nextY = curY + DIRECTIONS[i][1];
                
                if (!isValid(nextX, nextY, grid, sourceSet)) {
                    continue;
                }
            
                if (destSet[nextX][nextY]) {
                    return true;
                }
                
                Point nextPoint(nextX, nextY);
                curQueue.push(nextPoint);
                sourceSet[nextX][nextY] = true;
            }
        }
        return false;
    }
    
    bool isValid(int x, int y, const vector<vector<bool>>& grid, const vector<vector<bool>>& sourceSet) {
        if (x < 0 || x >= grid.size() || y < 0 || y >= grid[0].size() || grid[x][y] || sourceSet[x][y]) {
            return false;
        }
        return true;
    }
    
};
```
