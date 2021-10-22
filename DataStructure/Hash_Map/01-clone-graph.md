# Clone Graph
> Source: LintCode (https://www.lintcode.com/problem/137/)
## Problem Description
```
Clone an undirected graph. Each node in the graph contains a label and a list of its neighbors. Nodes are labeled uniquely.

You need to return a deep copied graph, which has the same structure as the original graph, and any changes to the new graph will not have any effect on the original graph.

You need return the node with the same label as the input node.
How we represent an undirected graph: http://www.lintcode.com/help/graph/
Example

Example1

Input:

{1,2,4#2,1,4#4,1,2}

Output: 

{1,2,4#2,1,4#4,1,2}

Explanation:

1------2  

 \     |  

  \    |  

   \   |  

    \  |  

      4   

```

 ### C++ Solution
The problem is solved by using BFS and Hashmap. See the code comment of each 4 steps and the helper functions.

 
 ```
/**
 * Definition for undirected graph.
 * struct UndirectedGraphNode {
 *     int label;
 *     vector<UndirectedGraphNode *> neighbors;
 *     UndirectedGraphNode(int x) : label(x) {};
 * };
 */

class Solution {
public:
    /**
     * @param node: A undirected graph node
     * @return: A undirected graph node
     */
    UndirectedGraphNode* cloneGraph(UndirectedGraphNode* node) {
        if (node == nullptr) return node;

        // step 1: Find all nodes, we use BFS method here
        vector<UndirectedGraphNode*> nodes = getNodes(node);

        // step 2: Copy all nodes, we use a hash table to store old and new nodes map
        unordered_map<UndirectedGraphNode*, UndirectedGraphNode*> mapping = copyNodes(nodes);

        // step 3: Find all edges, and Copy all edges 
        copyEdges(nodes, mapping);

        // step 4: return the clone graph from the old - new nodes map
        return mapping[node];

    }
    
    // get node function
    vector<UndirectedGraphNode*> getNodes(UndirectedGraphNode* node) {
        unordered_set<UndirectedGraphNode*> visited;
        visited.insert(node);

        queue<UndirectedGraphNode*> q;
        q.push(node);

        while (!q.empty()) {
            auto cur_node = q.front();
            q.pop();

            for (auto neighbor : cur_node->neighbors) {
                if (visited.count(neighbor)) {
                    continue;
                }
                q.push(neighbor);
                visited.insert(neighbor);
            }
        }

        vector<UndirectedGraphNode*> nodes(visited.begin(), visited.end());
        
        return nodes;
    }

    // copy nodes function
    unordered_map<UndirectedGraphNode*, UndirectedGraphNode*> copyNodes(vector<UndirectedGraphNode*> nodes) {
        unordered_map<UndirectedGraphNode*, UndirectedGraphNode*> nodes_map;
        for (auto node : nodes) {
            nodes_map[node] = new UndirectedGraphNode(node->label);
        }
        return nodes_map;
    }

    // find and copy edges function
    void copyEdges(vector<UndirectedGraphNode*> nodes, unordered_map<UndirectedGraphNode*, UndirectedGraphNode*> mapping) {
        for (auto node : nodes) {
            auto new_node = mapping[node];
            for (auto neighbor : node->neighbors) {
                auto new_neighbor = mapping[neighbor];
                new_node->neighbors.push_back(new_neighbor);
            }
        }
    }

};
 ```
 