# Binary Tree


## Type of Binary Tree
### Balanced binary tree
commonly defined as a binary tree in which the depth of the left and right subtrees of every node differ by 1 or less.  
1. 对于每一个节点，其左右子树高度差相差 <= 1

### Complete binary tree
is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible.  
1. 除最后一层外，其余层必须满
2. 若最后一层不满，必须靠左排列

### Binary Search Tree
for every single node in the tree, the values in its left subtree are all smaller than its value, and the values in its right subtree are all larger than its value.  
对于tree中的每一个节点：  
1. 其左子树中所有值都要比这个节点的值小
2. 其右子树中所有值都要比这个节点的值大
<br>

--------
<br>

## Recursion的2种形式
### Bottom Up


### Top Down


--------

## Base Case的选择



--------

## 涉及题目
### 遍历树
**Recursion——先序遍历，中序遍历，后序遍历**

```python
class treeNode(object):
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None
```

**Pre-order**
```python
def preOrder(root):
    res = []
    traverse(root, res)
    return res


def traverse(root, res):
    if not root:
        return
    
    res.append(root.val)
    traverse(root.left, res)
    traverse(root.right, res)
    return
```

**In-order**
```python
def inOrder(root):
    res = []
    traverse(root, res)
    return res


def traverse(root, res):
    if not root:
        return
    
    traverse(root.left, res)
    res.append(root.val)
    traverse(root.right, res)
    return
```

**Post-order**
```python
def postOrder(root):
    res = []
    traverse(root, res)
    return res
    
    
def traverse(root, res):
    if not root:
        return 
    
    traverse(root.left, res)
    traverse(root.right, res)
    res.append(root.val)
    return

```


**Iteration——先序遍历，中序遍历，后序遍历**
**Pre-order**
```python

def preOrder(root):
    res = []
    if not root:
        return res
    
    stack = [(root, 1)]
    while stack:
        node, count = stack.pop()
        if count == 1:
            res.append(node.val)
            stack.append((node, count+1))
            if node.left:
                stack.append((node.left, 1))
        elif count == 2:
            if node.right:
                stack.append((node.right, 1))
    return res
    
```


**In-order**
```python

def preOrder(root):
    res = []
    if not root:
        return res
    
    stack = [(root, 1)]
    while stack:
        node, count = stack.pop()
        if count == 1:
            stack.append((node, count+1))
            if node.left:
                stack.append((node.left, 1))
        elif count == 2:
            res.append(node.val)
            if node.right:
                stack.append((node.right, 1))
    return res
    
```


**Post-order**
```python

def preOrder(root):
    res = []
    if not root:
        return res
    
    stack = [(root, 1)]
    while stack:
        node, count = stack.pop()
        if count == 1:
            stack.append((node, count+1))
            if node.left:
                stack.append((node.left, 1))
        elif count == 2:
            stack.append((node, count+1))
            if node.right:
                stack.append((node.right, 1))
        elif count == 3:
            res.append(node.val)
    return res

```

**Level**
```python
from collections import deque

def levelOrder(root):
    res = []
    if not root:
        return res
    
    cur = deque([root])
    nxt = deque()
    while cur:
        node = cur.popleft()
        res.append(node.val)
        if node.left:
            nxt.append(node.left)
        if node.right:
            nxt.append(node.right)
            
        if not cur:
            print(res)
            if nxt:
                cur = nxt
                nxt = deque()
                res = []
    return

```

**Zig Zag level**
```python
from collections import deque

def zigZag(root):
    res = []
    if not root:
        return res
    
    cur = deque([root])
    nxt = deque()
    sig = -1
    
    while cur:
        if sig == 1:
            node = cur.popleft()
            res.append(node.val)
            if node.left:
                nxt.append(node.left)
            if node.right:
                nxt.append(node.right)
        
        elif sig == -1:
            node = cur.popleft()
            res.append(node.val)
            if node.right:
                nxt.appendleft(node.right)
            if node.left:
                nxt.appendleft(node.left)
        if not cur:
            if nxt:
                cur = nxt
                nxt = deque()
                sig = -1 * sig
    return res

```

### BST
**isBST Validation**  
（In-order, Pre-order, Post-order）

**实现BST的操作** 
1. Query
2. Insert
3. Delete

**Range Sum of BST**



### Path
**Find the length of the longest consecutive sequence path**  
(From parent to children)

**从 Root -> Leaf 的最大路径和**

**从 Root -> Leaf 的路径和是否 = Target**

**BT的最大路径和(Root -> Leaf途中) Longest Subarray Sum Problem**

**BT的最大路径和(Only Leaf Node -> Another Leaf) Longest Subarray Sum Problem**

**BT的最大路径和(Any Node -> Any Node) Longest Subarray Sum Problem**



### Other
**Get Height of a Tree**
```python

def getHeight(root):
    if not root:
        return 0
        
    left_h = getHeight(root.left)
    right_h = getHeight(root.right)
    
    return max(left_h, right_h) + 1

```

**翻转树**

**给每个节点存上其左子树大总节点数**

**找到高度差最大的节点**

**找到树的最小深度**（from root to leaf）


