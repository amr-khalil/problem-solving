---
description: Leetcode 200 - Medium
---

# Number of Islands

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return _the number of islands_.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

&#x20;

**Example 1:**

<pre><code><strong>Input: grid = [
</strong>  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
<strong>Output: 1
</strong></code></pre>

**Example 2:**

<pre><code><strong>Input: grid = [
</strong>  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
<strong>Output: 3
</strong></code></pre>

&#x20;

**Constraints:**

* `m == grid.length`
* `n == grid[i].length`
* `1 <= m, n <= 300`
* `grid[i][j]` is `'0'` or `'1'`.

**Solution**

{% code lineNumbers="true" %}
````python
```python
from typing import List

class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        # check if the grid empty
        if not grid: return 0

        # initiate variables
        visited = set()
        rows, cols = len(grid), len(grid[0])
        islands_count = 0

        # use depth first search
        def dfs(r, c):
            # initiate the stack
            stack = []
            visited.add((r, c)) # {(0,0)}
            stack.append((r, c)) # [(0,0)]

            # check if the stack have values
            while stack:
                # pop the stack
                row, col = stack.pop()

                # check the neighbours cells vertically and horizontally
                directions = [[0, 1], [0, -1], [1, 0], [-1, 0]]
                for dr, dc in directions:
                    r = row + dr
                    c = col + dc
                    
                    # check if grid range is valid
                    if r in range(rows) and c in range(cols):
                        cell = grid[r][c]
                        # check if the cell is 'island' and not visited
                        if cell == '1' and (r, c) not in visited:
                            # add the cell index to the visited set and to the stack
                            visited.add((r, c))
                            stack.append((r, c))
        

        for r in range(rows):
            for c in range(cols):
                # select a cell
                cell = grid[r][c]
                # check if the cell is 'island' and not visited
                if cell == '1' and (r, c) not in visited:
                    dfs(r, c)
                    islands_count += 1
        
        return islands_count
        
s = Solution()

grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]

print(s.numIslands(grid))
```
````
{% endcode %}

