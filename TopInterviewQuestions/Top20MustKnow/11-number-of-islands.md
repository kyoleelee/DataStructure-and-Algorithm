# Number of Islands
> Source: LintCode (https://www.lintcode.com/problem/433/)
## Problem Description
```
Given a boolean 2D matrix, 0 is represented as the sea, 1 is represented as the island. If two 1 is adjacent, we consider them in the same island. We only consider up/down/left/right adjacent.

Find the number of islands.
Example

Example 1:

Input:

[

  [1,1,0,0,0],

  [0,1,0,0,1],

  [0,0,0,1,1],

  [0,0,0,0,0],

  [0,0,0,0,1]

]

Output:

3

Example 2:

Input:

[

  [1,1]

]

Output:

1
```

## C++ Solution
1. BFS method  
2. DFS method can also do it, but not recommand becuase there is risk to overflow at recursive calls due to large input dataset  


Time Complexity: O(n^2)  
Space Complexity: O(n^2)  
 
```
class Solution {
public:
    /**
     * @param grid: a boolean 2D matrix
     * @return: an integer
     */
    int numIslands(vector<vector<bool>> &grid) {
        if (grid.empty() || grid[0].empty()) return 0;

        int ans = 0;
        int n = grid.size();
        int m = grid[0].size();
        vector<vector<bool>> visited(n, vector<bool>(m, false));

        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {
                if (grid[i][j] && !visited[i][j]) {
                    bfs(i, j, n, m, grid, visited);
                    ans++;
                }
            }
        }

        return ans;
    }

    void bfs(int x, int y, int n, int m, vector<vector<bool>>& grid, vector<vector<bool>>& visited) {
        queue<pair<int, int>> q;
        q.push({x, y});
        visited[x][y] = true;

        while (!q.empty()) {
            int cur_x = q.front().first;
            int cur_y = q.front().second;
            q.pop();

            for (int i = 0; i < 4; ++i) {
                int next_x = cur_x + deltaX[i];
                int next_y = cur_y + deltaY[i];

                if (isValid(next_x, next_y, n, m, grid, visited) == false) {
                    continue;
                }

                q.push({next_x, next_y});
                visited[next_x][next_y] = true;
            }
        }
    }
    
    bool isValid(int x, int y, int n, int m, vector<vector<bool>>& grid, vector<vector<bool>>& visited) {
        if (x < 0 || x >= n || y < 0 || y >= m || !grid[x][y] ||visited[x][y]) {
            return false;
        }
        return true;
    }

private:
    int deltaX[4] = {-1, 1, 0, 0};
    int deltaY[4] = {0, 0, -1, 1};
};
```
 