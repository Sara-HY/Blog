---
title: LeetCode_Clone Graph
date: 2019-03-14 15:15:35
categories: LeetCode
tags: 
  - medium
  - dfs
  - bfs
  - graph
---

## [Clone Graph](https://leetcode.com/problems/clone-graph/)

Given a reference of a node in a connected undirected graph, return a deep copy (clone) of the graph. Each node in the graph contains a val (int) and a list (List[Node]) of its neighbors.
（深度拷贝图）

<!--more-->

**Note:**
1. The number of nodes will be between 1 and 100.
2. The undirected graph is a simple graph, which means no repeated edges and no self-loops in the graph.
3. Since the graph is undirected, if node p has node q as neighbor, then node q must have node p as neighbor too.
4. You must return the copy of the given node as a reference to the cloned graph.

**Example:** 

<div align=center>
	<img src="/images/leetcode_133.png" width = "500" align=center/>
</div>

### 1. DFS (递归) 

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val, neighbors):
        self.val = val
        self.neighbors = neighbors
"""
class Solution:
    def dfs(self, node):
        for _node in node.neighbors:
            if _node not in self.map_dict:
                copy_neighbor = Node(_node.val, [])
                self.map_dict[_node] = copy_neighbor
                self.map_dict[node].neighbors.append(copy_neighbor)
                self.dfs(_node)
            else:
                self.map_dict[node].neighbors.append(self.map_dict[_node])        
        return
            
    def cloneGraph(self, node: 'Node') -> 'Node':
        if not node:
            return None
        
        self.map_dict = {}
        copy_node = Node(node.val, [])
        self.map_dict[node] = copy_node
        self.dfs(node)
        
        return copy_node
```


### 2. DFS (栈) 

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val, neighbors):
        self.val = val
        self.neighbors = neighbors
"""
class Solution:            
    def cloneGraph(self, node: 'Node') -> 'Node':
        if not node:
            return None
        
        map_dict = {}
        copy_node = Node(node.val, [])
        map_dict[node] = copy_node
        
        stack = [node]
        while stack:
            _node = stack.pop()
            for neighbor in _node.neighbors:
                if neighbor not in map_dict:
                    copy_neignbor = Node(neighbor.val, [])
                    map_dict[neighbor] = copy_neignbor
                    map_dict[_node].neighbors.append(copy_neignbor)
                    stack.append(neighbor)
                else:
                    map_dict[_node].neighbors.append(map_dict[neighbor])
                
        return copy_node
```

### 3. BFS (队列)

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val, neighbors):
        self.val = val
        self.neighbors = neighbors
"""
class Solution:        
    def cloneGraph(self, node: 'Node') -> 'Node':
        if not node:
            return None
        
        map_dict = {}
        copy_node = Node(node.val, [])
        map_dict[node] = copy_node
        
        queue = [node]
        while queue:
            _node = queue.pop(0)
            for neighbor in _node.neighbors:
                if neighbor not in map_dict:
                    copy_neignbor = Node(neighbor.val, [])
                    map_dict[neighbor] = copy_neignbor
                    map_dict[_node].neighbors.append(copy_neignbor)
                    queue.append(neighbor)
                else:
                    map_dict[_node].neighbors.append(map_dict[neighbor])
                
        return copy_node
```
