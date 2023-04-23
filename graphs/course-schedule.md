---
description: Leetcode 207 - Medium
---

# Course Schedule

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `bi` first if you want to take course `ai`.

* For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.

&#x20;

**Example 1:**

<pre><code><strong>Input: numCourses = 2, prerequisites = [[1,0]]
</strong><strong>Output: true
</strong><strong>Explanation: There are a total of 2 courses to take. 
</strong>To take course 1 you should have finished course 0. So it is possible.
</code></pre>

**Example 2:**

<pre><code><strong>Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
</strong><strong>Output: false
</strong><strong>Explanation: There are a total of 2 courses to take. 
</strong>To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
</code></pre>

**Solution**



````python
```python3
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        # map each course to prereq list
        preMap = {i:[] for i in range(numCourses)}
        for crs, pre in prerequisites:
            preMap[crs].append(pre)
        
        # visitSet = all courses along the curr DFS path
        visitSet = set()
        def dfs(crs):
            # if course is visited, return false
            if crs in visitSet:
                return False
            # if course don't have any prerequisites, return True
            if preMap[crs] == []:
                return True

            # add course to visit set
            visitSet.add(crs)
            # loop through all the prerequisites
            for pre in preMap[crs]:
                if not dfs(pre):
                    return False
            # remove course
            visitSet.remove(crs)
            preMap[crs] = []
            return True
        
        for crs in range(numCourses):
            if not dfs(crs):
                return False

        return True
```
````

