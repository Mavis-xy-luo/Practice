# Binary Tree


## Type of Binary Tree
### 1. Balanced binary tree
commonly defined as a binary tree in which the depth of the left and right subtrees of every node differ by 1 or less.  
```
1. 对于每一个节点，其左右子树高度差相差 <= 1
```

### 2. Complete binary tree
is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible.  
```
1. 除最后一层外，其余层必须满
2. 若最后一层不满，必须靠左排列
```

### 3. Binary Search Tree
for every single node in the tree, the values in its left subtree are all smaller than its value, and the values in its right subtree are all larger than its value.  
```
对于tree中的每一个节点：  
1. 其左子树中所有值都要比这个节点的值小
```
<br/>

--------
<br/>

## Recursion的2种形式
### Bottom Up
**Bottom Up的特点:** 
由**下->上**返值，故信息随着返回(return)的值传递

```
三部曲思考方式
1. 要从左孩子拿什么值
   要从右孩子拿什么值
2. 在当前节点要做什么？
3. 要向父节点返回什么？
```

### Top Down
**Top Down的特点:** 
由**上->下**传值，故信息随着调用函数时的参数传递
```
1. 以参数传递信息，结果通常由“global variable”记录；
2. 通常不需要返回值，且尽量不要返（因为结果已被记录）
3. 思维上更直接，但代码不如Bottom Down简洁
```
<br>

--------

<br>

## Base Case的选择
以**叶子节点**为Base case还是以叶子节点下面的**None**作为Base case？ 
```
**叶子节点为base case的特点**  
当需要区分叶子节点和非叶子节点时，选择leaf作为base case

**None为base case的特点**   
缺点：从None返回后并不能知道其父节点是否是叶子节点
```
<br>

--------

<br>

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
**1. In-order:**  
   当对BST实现中序遍历时，得到的应该是一个从小到大排列的有序序列，即前一个node永远比后一个node小
```python

def isBSTInOrder(root):
    res = [-float('inf')]
    return isBSTInOrderHelper(root, res)
    
def isBSTInOrderHelper(root, res):
    if not root:
        return True
    
    left = isBSTInOrderHelper(root.left, res)
    if root.val <= res[0]:
        return False
    res[0] = root.val
    right = isBSTInOrderHelper(root.right, res)
    
    return left and right

```


**2. Pre-order:**  
   对于每一个节点：  
   如果它是父节点的左子节点：其值应该落在(parent_lower_bound, parent_value)  
                右子节点：其应该落在(parent_value, parent_upper_bound)
                
```python

def isBSTPreOrder(root):
    min_val = -float('inf')
    max_val = float('inf')
    
    return isBSTPreOrderHelper(root, min_val, max_val)

def isBSTPreOrderHelper(root, min_val, max_val):
    if not root:
        return True
    
    if root.val <= min_val or root.val >= max_val:
        return False
    
    left = isBSTPreOrderHelper(root.left, min_val, root.val)
    right = isBSTPreOrderHelper(root.right, root.val, max_val)
    
    return left and right

```


**3. Post-order:**    
   对于每一个节点：其值应该大于左子树的最大值，小于右子树的最小值   
   即 left_max < root.val < right_min  
      return (left_min, right_max)  (如果不存在左/右节点，那个位置的值用自己替代)
```python

def isBSTPostOrder(root):
    return isBSTPostOrderHelper(root)[0]


def isBSTPostOrderHelper(root):
    if not root:
        return (True, None, None)
    
    bl, l_min, l_max = isBSTPostOrderHelper(root.left)
    br, r_min, r_max = isBSTPostOrderHelper(root.right)
    
    if not bl or not br:
        return (False, None, None)
    if l_max and root.val <= l_max:
        return (False, None, None)
    if r_min and root.val > r_min:
        return (False, None, None)
    return (True, l_min if l_min else root.val, r_max if r_max else root.val)
#     return (True, l_min or root.val, r_min or root.val)

```



**实现BST的操作** 
1. Query
2. Insert
3. Delete

**Range Sum of BST**

<br>

--------

<br>

### Path
**1. Find the length of the longest consecutive sequence path**  
(From parent to children, cannot be the reverse)

`注意：因为helper中需要传入父节点，但是root的父节点传入是None，故在后面判断root.val == parent.val前需要加一个判断父节点是否存在的条件。`  

```python

# Top down
def consecutivePath(root):
    res = [0]
    consecutivePathHelper(root, None, 0, res)
    return res[0]
    
def consecutivePathHelper(root, p_val, count, res):
    if not root:
        return
    
    if p_val and root.val == p_val + 1:
        count += 1
    else:
        count = 1
        
    if count > res[0]:
        res[0] = count
    
    consecutivePathHelper(root.left, root.val, count, res)
    consecutivePathHelper(root.right, root.val, count, res)
    return


# Bottom Up
def cosecutivePathBU(root):
    return consecutivePathBUHelper(root, None, 0)
    
def consecutivePathBUHelper(root, parent, count):
    if not root:
        return 0
    
    if parent and root.val == parent.val + 1:
        count += 1
    else:
        count = 1
        
    max_count_l = consecutivePathBUHelper(root.left, root, count)
    max_count_r = consecutivePathBUHelper(root.right, root, count)
    return max(count, max_count_l, max_count_r)
```


**2. 从 Root -> Leaf 的最大路径和**  
Given a binary tree in which each node contains an interger number. Find the maximum possible path sum from a leaf to root. 
Assumptions: the rootof a given binary tree is not null.

```python
# Bottom Up
def maxPathSumLeafToRoot(root):
    if root is None:
        return -float('inf')
    if not root.left and not root.right:
        return root.val
    
    left = maxPathSumLeafToRoot(root.left)
    right = maxPathSumLeafToRoot(root.right)
    return max(left, right) + root.val
    
# Top Down

```

**3. 从 Root -> Leaf 的路径和是否 = Target**  
Given a binary tree and a target sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given target.  

Top Down，从上往下传值（传入到parent为止的sum，target）
在leaf得到sum，和target比较，如果==，返回True

```python

def sumToTarget(root, target):
    return sumToTargetHelper(root, 0, target)
    
    
def sumToTargetHelper(root, cur_sum, target):
    if not root:
        return False
    if not root.left and not root.right:
        res = cur_sum + root.val
        if res == target:
            return True
    bl = sumToTargetHelper(root.left, cur_sum + root.val, target)
    br = sumToTargetHelper(root.right, cur_sum + root.val, target)
    
    return bl or br

```

**BT的最大路径和(Root -> Leaf途中) Longest Subarray Sum Problem**  
Given a binary tree in which each node contains an integer number. Find the maximum possible sum from any node to any node(the two nodes can be the same node and they can only be on the path from root to one of the leaf nodes).

```python

def longestSubpathSum(root):
    res = [0]
    longestSubpathSumHelper(root, 0, res)
    return res[0]
      
    
def longestSubpathSumHelper(root, cur, res):
    if not root:
        return
    if cur < 0:
        cur = root.val
    else:
        cur += root.val
    res[0] = max(cur, res[0])
    
    longestSubpathSumHelper(root.left, cur, res)
    longestSubpathSumHelper(root.right, cur, res)
    return

```

**BT的最大路径和(Only Leaf Node -> Another Leaf) Longest Subarray Sum Problem**  
Given a binary tree in which each node cantains a number. Find the maximum possible sum from one leaf node to another.(The maximum sum path may or may not go through root.)

```python

def mSubSumLeafToLeaf(root):
    res = [-float('inf')]
    mSubSumLeafToLeafHelper(root, res)
    return res[0]


def mSubSumLeafToLeafHelper(root, res):
    if not root:
        return -float('inf')
    if not root.left and not root.right:
        return root.val
    left = mSubSumLeafToLeafHelper(root.left, res) if root.left else -float('inf')
    right = mSubSumLeafToLeafHelper(root.right, res) if root.right else -float('inf')
    
    res[0] = max((left + right + root.val), res[0])
    return max(left, right) + root.val

```

**BT的最大路径和(Any Node -> Any Node) Longest Subarray Sum Problem**  
Get Maximum sum of path cost from any node to any node

```python

def maxPathSum(root):
    res = [-float('inf')]
    helper(root, res)
    return res[0]
  

def maxPathSumHelper(root, res):
    if not root:
        return 0
    
    left = maxPathSumHelper(root.left, res) if root.left else -float('inf')
    right = maxPathSumHelper(root.right, res) if root.right else -float('inf')

    cur = root.val
    if left > 0:
        cur += left
    if right > 0:
        cur += right
    res[0] = max(cur, res[0])

    return max(left, right, 0) + root.val

```


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

**找到节点差最大的节点**  
Find the node with the max difference in the total number of descendants in its left subtree and right subtree.
```python

def get_max_diff(root):
    res = []
    res.append(0)
    res.append(root)
    
    node_diff(root, res)
    return res[1]
    
def node_diff(root, res):
    if not root:
        return 0
    
    left_total = node_diff(root.left, res)
    right_total = node_diff(root.right, res)
    
    diff = abs(right_total - left_total)
    if diff > res[0]:
        res[0] = diff
        res[1] = root
        
    return left_total+right_total+1

```

**找到树的最小深度**  
Find minimum height of a binary tree.（from root to leaf）
```python

def get_minimum_height(root):
    if not root:
        return 0
    if not root.left and not root.right:
        return 1
    if not root.left:
        return get_minimum_height(root.right) + 1
    if not root.right:
        return get_minimum_height(root.left) + 1
    return min(get_minimum_height(root.left), get_minimum_height(root.right)) + 1
    
# or

def get_minimum_height(root):
    if not root:
        return 0
    if not root.left and not root.right:
        return 1
    
    left = getHeight(root.left) if root.left else float('inf')
    right = getHeight(root.right) if root.right else float('inf')
    return min(left, right) + 1

```


