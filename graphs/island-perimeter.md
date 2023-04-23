---
description: Leetcode 463 - Easy
---

# Island Perimeter

You are given `row x col` `grid` representing a map where `grid[i][j] = 1` represents land and `grid[i][j] = 0` represents water.

Grid cells are connected **horizontally/vertically** (not diagonally). The `grid` is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells).

The island doesn't have "lakes", meaning the water inside isn't connected to the water around the island. One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.

&#x20;

**Example 1:**

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

<pre><code><strong>Input: grid = [[0,1,0,0],[1,1,1,0],[0,1,0,0],[1,1,0,0]]
</strong><strong>Output: 16
</strong><strong>Explanation: The perimeter is the 16 yellow stripes in the image above.
</strong></code></pre>

**Example 2:**

<pre><code><strong>Input: grid = [[1]]
</strong><strong>Output: 4
</strong></code></pre>

**Example 3:**

<pre><code><strong>Input: grid = [[1,0]]
</strong><strong>Output: 4
</strong></code></pre>

&#x20;

**Constraints:**

* `row == grid.length`
* `col == grid[i].length`
* `1 <= row, col <= 100`
* `grid[i][j]` is `0` or `1`.
* There is exactly one island in `grid`.

**Solution 1**

{% code lineNumbers="true" %}
````python
```python3
class Solution:
    def islandPerimeter(self, grid: List[List[int]]) -> int:
        # check if the grid is empty
        if not grid: return 0

        # initiate variables
        rows, cols = len(grid), len(grid[0])
        visited = set()
        total_perimeter = 0

        # use depth first search
        def dfs(r, c):
            # initiate stack and vars
            stack = []
            stack.append((r, c))
            visited.add((r, c))
            perimeter = 0

            # loop and pop the stack
            while stack:
                row, col = stack.pop()
                # check the direcktions
                directions = [[0, 1], [0, -1], [1, 0], [-1, 0]]
                for dr, dc in directions:
                    r = row + dr
                    c = col + dc

                    # check if grid range is valid
                    if r in range(rows) and c in range(cols):
                        cell = grid[r][c]
                        cell_pos = (r, c)
                        # check if the cell is 'island' and not visited
                        if cell == 1 and cell_pos not in visited:
                            visited.add(cell_pos)
                            stack.append(cell_pos)

                        if cell == 0 and cell_pos not in visited:
                            # hit water cell
                            perimeter += 1
                    else:
                        # hit out of the boundry
                        perimeter += 1

            return perimeter

        for r in range(rows):
            for c in range(cols):
                # select a cell
                cell = grid[r][c]
                cell_pos = (r, c)
                # check if the cell is 'island' and not visited
                if cell == 1 and cell_pos not in visited:
                    perimeter = dfs(r, c)
                    total_perimeter += perimeter
    
        
        return total_perimeter
```
````
{% endcode %}

**Solution 2**

````python
```python3
class Solution:
    def islandPerimeter(self, grid: List[List[int]]) -> int:
        # check if the grid is empty
        if not grid: return 0

        # initiate variables
        rows, cols = len(grid), len(grid[0])
        visited = set()

        # use depth first search
        def dfs(r, c):
            # case 1: check if the index out of the grid
            if r not in range(rows) or c not in range(cols):
                return 1

            # case 2: check if this cell is 'water'
            if grid[r][c] == 0:
                return 1
            
            # case 3: check if this cell is visited
            if (r, c) in visited:
                return 0
            
            visited.add((r, c))
            perimeter = dfs(r, c + 1)
            perimeter += dfs(r, c - 1)
            perimeter += dfs(r + 1, c)
            perimeter += dfs(r - 1, c)
            
            return perimeter


        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == 1:
                    return dfs(r, c)

```
````
