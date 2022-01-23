# Heap
## Min Heap & Max Heap
1. Min/Max heap是CBT  
2. 每个node都比自己的孩子节点小/大 (<= / >=)  
(孩子节点之间没有关系）

## Implement a complete binary tree
Use array to implement a complete binary tree  
Ad: 1. save space.  
    2. from child node find its father node.  

在array实现的CBT中，可以根据一个节点的左孩子存不存在判断其是不是leaf。

```
假设当前节点index = x：
1. 左孩子 index = 2x + 1
2. 右孩子 index = 2x + 2
3. 父节点 index = (x - 1) // 2
```
