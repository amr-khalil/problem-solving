---
description: Leetcode 79 - Medium
---

# Word Search

Given an `m x n` grid of characters `board` and a string `word`, return `true` _if_ `word` _exists in the grid_.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

&#x20;

**Example 1:**

<img src="https://assets.leetcode.com/uploads/2020/11/04/word2.jpg" alt="" data-size="original">

<pre><code><strong>Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
</strong><strong>Output: true
</strong></code></pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg)

<pre><code><strong>Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
</strong><strong>Output: true
</strong></code></pre>

**Example 3:**

![](https://assets.leetcode.com/uploads/2020/10/15/word3.jpg)

<pre><code><strong>Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
</strong><strong>Output: false
</strong></code></pre>

&#x20;

**Constraints:**

* `m == board.length`
* `n = board[i].length`
* `1 <= m, n <= 6`
* `1 <= word.length <= 15`
* `board` and `word` consists of only lowercase and uppercase English letters.

&#x20;

**Follow up:** Could you use search pruning to make your solution faster with a larger `board`?

**Solution**

{% code lineNumbers="true" %}
```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        if not board: return False

        rows, cols = len(board), len(board[0])
        visited = set()

        def dfs(r, c, idx=0):
            # check if the word is full scanned
            if len(word) == idx:
                return True

            if (r < 0 or
                c < 0 or
                r >= rows or
                c >= cols or
                word[idx] != board[r][c] or
                (r, c) in visited):
                return False

            visited.add((r, c))
            res = (
                dfs(r+1, c, idx+1) or
                dfs(r-1, c, idx+1) or
                dfs(r, c+1, idx+1) or
                dfs(r, c-1, idx+1)
                )
            visited.remove((r, c))
            
            return res
        
        for r in range(rows):
            for c in range(cols):
               if dfs(r, c, 0):
                   return True
        
        return False
```
{% endcode %}

