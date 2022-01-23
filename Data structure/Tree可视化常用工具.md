### 创建树
```python

class treeNode(object):
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

```

### 按层打印树，空的地方输出None
```python

from collections import deque

def levelPrintTree(root):
    res = []
    if not root:
        return res
    
    cur = deque([root])
    nxt = deque()
    
    while cur:
        node = cur.popleft()
        if node:
            res.append(node.val)
            nxt.append(node.left)
            nxt.append(node.right)
        else:
            res.append(None)
        
        if not cur:
            print(res)
            if nxt:
                cur = nxt
                nxt = deque()
                res = []             
    return 

```

### 把list按层转化为树
Use the level order traversal sequence with a special ***None*** denoting the null node.  
For Example: 
The sequence [1, 2, 3, None, None, 4] represents the following binary tree:  
   1  
 2   3  
N N 4   

```python

from collections import deque
def constructTree(lst):
    dq = deque(lst)
    root = treeNode(dq.popleft())
    cur = deque([root])
    
    while cur:
        node = cur.popleft()
        if dq:
            left_val = dq.popleft()
            if left_val:
                node.left = treeNode(left_val) 
        if dq:
            right_val = dq.popleft()
            if right_val:
                node.right = treeNode(right_val)
        if node.left:
            cur.append(node.left)
        if node.right:
            cur.append(node.right)
    return root
    
# 示例
lst = [1, None, 3, 2, 4, None, None, 5, None, 8]
consTree = constructTree(lst) # 构建Tree
levelPrint(consTree) #用上面分level打印tree的方法打印

>>  [1]
    [None, 3]
    [2, 4]
    [None, None, 5, None]
    [8, None]
    [None, None]

```
