---
title: All paths from source to target
date: "2019-08-06T14:32:37.121Z"
layout: post
draft: false
path: "/posts/all-paths-from-source-to-target/"
category: "Algorithm"
tags:
  - "Graph"
  - "Learning to write"
description: "Description here"
---

Given a directed, acyclic graph of `N` nodes. Find all possible paths from node `0` to node `N-1`, and return them in any order.

The graph is given as follows: the nodes are `0, 1, ..., graph.length - 1`. `graph[i]` is a list of all nodes j for which the edge (i, j) exists.

##Example:

```
Input: [[1,2], [3], [3], []] 
Output: [[0,1,3],[0,2,3]] 
Explanation: The graph looks like this:
0--->1
|    |
v    v
2--->3
There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.
```

##Note:

- The number of nodes in the graph will be in the range `[2, 15]`.
- You can print different paths in any order, but you should keep the order of nodes inside one path.

## Solution:
```java
List<List<Integer>> allPathsSourceTarget(int[][] graph) {
    int[][] matrix = buildMatrix(graph);

    List<List<Integer>> paths = new ArrayList<>();
    List<Integer> path = new ArrayList<>();
    path.add(0);

    visit(0, matrix, path, paths);

    return paths;
}

private int[][] buildMatrix(int[][] graph) {
    int n = graph.length;
    int[][] matrix = new int[n][n];

    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < graph[i].length; ++j) {
            matrix[i][graph[i][j]] = 1;
        }
    }

    return matrix;
}

private void visit(int curNode, int[][] matrix, List<Integer> path, List<List<Integer>> paths) {
    if (curNode == matrix.length - 1) {
        paths.add(path);
    }
    for (int node = 0; node < matrix.length; ++node) {
        if (matrix[curNode][node] == 1) {
            List<Integer> newPath = new ArrayList<>(path);
            newPath.add(node);
            visit(node, matrix, newPath, paths);
        }
    }
}
```
