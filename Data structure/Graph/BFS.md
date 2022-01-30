# Graph - BFS

**[542. 01 Matrix](https://leetcode.com/problems/01-matrix/)**

```python

from collections import deque
    
def updateMatrix(self, mat: List[List[int]]) -> List[List[int]]:
    row = len(mat)
    col = len(mat[0])
        
    q = deque()
    for i in range(row):
        for j in range(col):
            if mat[i][j] == 0:
                q.append([i,j])
            else:
                mat[i][j] = "#"
                    
    directions = {(-1, 0), (1, 0), (0, -1), (0, 1)}            
    while q:
        cur = q.popleft()
        for direct in directions:
            x = cur[0] + direct[0]
            y = cur[1] + direct[1]
                
                
#             if 0 <= x and x <row and 0 <= y and y < col and mat[x][y] == "#":
#                 mat[x][y] = mat[cur[0]][cur[1]] + 1
#                 q.append([x, y])
                    
                
            if x < 0 or x >= row or y < 0 or y >= col or mat[x][y] != "#":
                continue
                
            mat[x][y] = mat[cur[0]][cur[1]] + 1
            q.append([x, y])
                
    return mat
```
