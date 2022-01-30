# BST
## BST的特性

## 实现BST的操作 
1. Query
2. Insert
3. Delete

```python

class BST(object):
    def __init__(self):
        self._root = None
        
    def query(self, key):
        curr = self._root
        while curr and curr != key:
            if key < curr:
                curr = curr.left
            if key > curr:
                curr = curr.right
        return curr
    
    def _insert(self, root, key):
        if not root:
            return treeNode(key)
        if key < root.val:
            root.left = self._insert(root.left, key)
        elif key > root.val:
            root.right = self._insert(root.right, key)
        return root
    
    def insert(self, key):
        self._root = self._insert(self._root, key)
        
    def delete(self, key):
        self._root = self._delete(self._root, key)
        
    def _delete(self, root, key):
        if not root:
            return None
        if key < root.key:
            root.left = self._delete(root.left, key)
            return root
        elif key > root.key:
            root.right = self._dilete(root.right, key)
            return root
        else:
            if not root.left:
                return root.right
            if not root.right:
                return root.left
            if root.right.left is None:
                root.right.left = root.left
                return root.right
                
                smallest = self._findAndDelMin(root.right)
                smallest.left = root.left
                smallest.right = root.right
                return smallest
        
          
    def _findAndDelMin(root):
        prev = root
        cur = root.left
        while cur.left:
            prev = cur
            cur = cur.left
        prev.next = cur.right
        
        return cur

```

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




**Range Sum of BST**
