Given a reference of a node in a connected undirected graph.  

Return a deep copy (clone) of the graph.  

Each node in the graph contains a value (int) and a list (List[Node]) of its neighbors.  

Example 1:  
```
Input: adjList = [[2,4],[1,3],[2,4],[1,3]]
Output: [[2,4],[1,3],[2,4],[1,3]]
Explanation: There are 4 nodes in the graph.
1st node (val = 1)'s neighbors are 2nd node (val = 2) and 4th node (val = 4).
2nd node (val = 2)'s neighbors are 1st node (val = 1) and 3rd node (val = 3).
3rd node (val = 3)'s neighbors are 2nd node (val = 2) and 4th node (val = 4).
4th node (val = 4)'s neighbors are 1st node (val = 1) and 3rd node (val = 3).
```
Example 2:  
```
Input: adjList = [[]]
Output: [[]]
Explanation: Note that the input contains one empty list. The graph consists of only one node with val = 1 and it does not have any neighbors
```
Example 3:  
```
Input: adjList = []
Output: []
Explanation: This an empty graph, it does not have any nodes.
```

Code:  
```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> neighbors;
    Node() {
        val = 0;
        neighbors = vector<Node*>();
    }
    Node(int _val) {
        val = _val;
        neighbors = vector<Node*>();
    }
    Node(int _val, vector<Node*> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
};
*/

class Solution {
public:
    Node* cloneGraph(Node* node) {
        // if the node is NULL
        if(!node) return NULL;
        // if the size of visitedNode is not enough, resize it.
        if((node -> val) >= visitedNode.size()) {
            visitedNode.resize(node -> val + 1);
        }
        // if the node has been visited.
        if(visitedNode[node -> val] != NULL) return visitedNode[node -> val];

        Node* head_ptr;
        Node head(node -> val);
        head_ptr = new Node(head);
        visitedNode[node -> val] = head_ptr;
        
        for(int i = 0; i < node -> neighbors.size(); ++i) {
            Node* neighbor = cloneGraph(node -> neighbors[i]);
            if(neighbor) head_ptr -> neighbors.push_back(neighbor);
        }
        return head_ptr;
    }
private:
    vector<Node*> visitedNode;
};
```

Runtime: 10 ms, faster than 31.28% of C++ online submissions for Clone Graph.  
Memory Usage: 9 MB, less than 35.14% of C++ online submissions for Clone Graph.
