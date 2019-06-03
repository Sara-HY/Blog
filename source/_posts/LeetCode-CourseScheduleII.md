---
title: LeetCode_Course Schedule II
date: 2019-06-03 13:46:20
categories: LeetCode
tags: 
  - medium
  - dfs
  - bfs
  - graph
  - topological-sort
---

## [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)

There are a total of **n** courses you have to take, labeled from 0 to n-1. Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]. Given the total number of courses and a list of prerequisite pairs, return the ordering of courses you should take to finish all courses. There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.
（课程清单，给出具体的结果）

<!--more-->

**Example:** 

<div align=center>
    <img src="/images/leetcode_210.png" width = "500" align=center/>
</div>


### 1. 拓扑排序-BFS
根据 "Course Schedule" 的步骤可以得出具体的结果，时间复杂度为O(n)，空间复杂度为O(n)。具体实现过程如下：

```python
import collections

class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        graph = collections.defaultdict(list)
        indegrees = collections.defaultdict(int)
        order_list = []

        for u, v in prerequisites:
            graph[v].append(u)
            indegrees[u] += 1

        queue = [u for u in range(numCourses) if indegrees[u] == 0]

        if not queue:
            return []

        while queue:
            v = queue[0]
            order_list.append(v)
            for u in graph[v]:
                indegrees[u] -= 1
                if indegrees[u] == 0:
                    queue.append(u)
            queue.remove(v)

        for u in range(numCourses):
            if indegrees[u] != 0:
                return []
        
        return order_list
```


### 2. 拓扑排序-DFS
同样地，时间复杂度为O(n)，空间复杂度为O(n)。具体实现过程如下：

```python
class Solution:
    def dfs(self, graph, order_list, visited, i):
        if visited[i] == 1:
            return False
        if visited[i] == 2:
            return True

        visited[i] = 1
        for j in graph[i]:
            if not self.dfs(graph, order_list, visited, j):
                return False
        visited[i] = 2
        order_list.append(i)
        return True

    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        graph = collections.defaultdict(list)
        visited = [0]*numCourses
        order_list = []

        for u, v in prerequisites:
            graph[v].append(u)
            
        for i in range(numCourses):
            if not self.dfs(graph, order_list, visited, i):
                return []
        order_list.reverse()
        return order_list
```


