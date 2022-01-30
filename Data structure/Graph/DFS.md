# Graph - DFS

**[200. Number of Island](https://leetcode.com/problems/number-of-islands/)**

> 特征：matrix图，四个方向，  
> open start & open end

```python

def numIslands(self, grid: List[List[str]]) -> int:
        
    # 遍历所有元素，if是1: count += 1 dfs把其余相连1都改变
        
    row = len(grid)
    col = len(grid[0])
    count = 0
        
    for i in range(row):
        for j in range(col):
            if grid[i][j] == "1":
                count += 1
                self.dfs(grid, i, j)

    return count
    
# dfs traversal

def dfs(self, grid, i, j):
    directions = {(0, -1), (0, 1), (-1, 0), (1, 0)}
    
    grid[i][j] = "-1"

    for direct in directions:
        x = i + direct[0]
        y = j + direct[1]

            
        if x<0 or x>=len(grid) or y<0 or y>=len(grid[0]) or grid[x][y] != "1":
            continue

        self.dfs(grid, x, y)
            
#         用or判断只需要判断一个条件对就行，所以更快，而and需要所有条件都满足
            
#         if x >= 0 and x < len(grid) and y >= 0 and y < len(grid[0]) and grid[x][y] == "1":
#             self.dfs(grid, x, y)
            
    return 

```
<br>

**[332. Reconstruct Itinerary](https://leetcode.com/problems/reconstruct-itinerary/)**

```python



```
