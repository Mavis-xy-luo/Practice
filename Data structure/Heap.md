# Heap
## Min Heap & Max Heap
1. Min/Max heap是CBT  
2. 每个node都比自己的孩子节点小/大 (<= / >=)   
(孩子节点之间没有关系，父节点不需要比同级父节点的子节点小/大）

## Implement a complete binary tree
Use array to implement a complete binary tree  
Ad: &nbsp;1. save space.  
&emsp;&emsp;2. from child node find its father node.

### Python heapq library
```python
import heapq  # 不是collections里的，因为不是数据结构
# create
hp = []

# push
heapq.heappush(hp, item)

# pop the top element
item = heapq.heappop(hp)

# see the top element without removing it
item = hp[0]

# transform list into a heap
heapq.heapify(lst)

#用例(可以看出heap本质是list，不是一个名为heap的数据结构)
lst = [0, 6, 4, 2, 9]
heapq.heapify(lst)
print(lst)
print(type(lst))
>> [0, 2, 4, 6, 9]
>>  <class 'list'>

item = heapq.heapreplace(heap, item) # pop and return smallest item, and add new item, the size of heap is unchanged
```

### 用Array实现Heap
1. push()
2. pop()
3. heapify(list)
在array实现的CBT中，可以根据一个节点的左孩子存不存在判断其是不是leaf。

```
假设当前节点index = x：
1. 左孩子 index = 2x + 1
2. 右孩子 index = 2x + 2
3. 父节点 index = (x - 1) // 2
```



#### sift up & sift down  
**sift up**   
做sift up的前提：除要sift up的元素，其余部分都满足heap的条件（插入最后一个元素前，所以tree已满足heap的条件）  

**sift down**  
做sift down的前提：sift down的元素的下面子树都满足heap的条件

```python

class Heap(object):l
    def __init__(self):
        self.lst = []
        
    def heapPush(self, val):
        self.lst.append(val)
        self.siftUp(self.lst, len(self.lst)-1)
        
    def siftUp(self, lst, idx):
        parent_idx = (idx - 1) // 2
        if parent_idx < 0 or lst[parent_idx] < lst[idx]:
            return
        lst[parent_idx], lst[idx] = lst[idx], lst[parent_idx]
        self.siftUp(lst, parent_idx)
        return
    
    
    def heapPop(self):
        res = self.lst[0]
        self.lst[-1], self.lst[0] = self.lst[0], self.lst[-1]
        self.lst.pop()
        
        self.siftDown(self.lst, 0)
        return res
        
    def siftDown(self, lst, idx):
        left = 2 * idx + 1
        right = 2 * idx + 2
        min_idx = idx
        
        if left < len(lst) and lst[left] < lst[min_idx]:
            min_idx = left
        if right < len(lst) and lst[right] < lst[min_idx]:
            min_idx = right
        
        if min_idx != idx:
            lst[min_idx], lst[idx] = lst[idx], lst[min_idx]
            self.siftDown(lst, min_idx)
            
        return
    
    
    def heapify(self, lst):
        for i in range((len(lst)-1-1) // 2, -1, -1):  # 右边界是开区间，所以要走到0位置，这里要写-1才能走到0
            self.siftDown(lst, i)
        self.lst = lst
        return
        
```



## 相关题目

#### Q1. Find smallest k elements from an unsorted array of size n.

```python
import heapq

# 使用 min heap
def findKsmallest(lst, k):
    res = []
    if not lst:
        return res
    
    heapq.heapify(lst)
    for i in range(min(k, len(lst))):
        res.append(heapq.heappop(lst))
    return res

# 使用 max heap 
#(找k smallest elements为什么要用max heap呢：因为当构建k个元素的heap是，top是这里面最小的元素，但我们每次想淘汰的是k个里面最大的那个，
# 故应该和k个元素里最大的那个元素比较，比最大的小的话，放进来。)

def findKsmallestMheap(lst, k):
    if not lst:
        return lst
    if k >= len(lst):
        return lst
    
    res = [-num for num in lst[:k]]
    heapq.heapify(res)
    for i in range(k, len(lst)):
        if lst[i] < -res[0]:
            heapq.heapreplace(res, -lst[i])
    return [-num for num in res]

```


#### Q2. Merge K sorted Array

``` python

import heapq
def merge(arrayOfArrays):

    import heapq
    if not arrayOfArrays:
        return arrayOfArrays
    
    hp = []
    for i in range(len(arrayOfArrays)):
        if len(arrayOfArrays[i]):   # 这一步判断用于处理arrays里面有空的array
            hp.append((arrayOfArrays[i][0], i, 0))
            # 其中i表示element是arrays里的第几个array里的，第三个参数“0”表示这个element在其array中是第几位

    heapq.heapify(hp)
    res = []
    while hp:
        ele_val, ele_array, ele_idx = heapq.heappop(hp)
        res.append(ele_val)
        if ele_idx + 1 < len(arrayOfArrays[ele_array]):
            heapq.heappush(hp, (arrayOfArrays[ele_array][ele_idx+1], ele_array, ele_idx+1))
    
    return res
    
    
# test
arrays = [[1, 3, 5, 7, 10],
          [-1, 0, 2, 9, 12, 13, 15],
          []]
merge(arrays)

>> [-1, 0, 1, 2, 3, 5, 7, 9, 10, 12, 13, 15]

```


```python

import heapq

def smallestRange(arrays):
    

```

#### Q3. Smallest Range
Given k sorted integer arrays, pick k elements (one element from each of sorted arrays), what is the smallest range.  
We define the range [a,b] is smaller than range [c,d] if b-a < d-c or a < c if b-a == d-c.  
Examples:  
[[ 1, 4, 6 ],  
 [ 2, 5 ],  
 [8, 10, 15]]  
pick one element from each of 3 arrays, the smallest range is {5, 8} (pick 6 from the first array, pick 5 from the second array and pick 8 from the third array).  

**解题思想**  

res = [low, up]  
heap(a1, b1, c1)  

新push进heap的x只有2种可能：
1. \> 现存的上界限  
&nbsp;此时x无法帮助改进res的结果，因为只会扩大范围；故作为新的max，看和heap里最小值 <em>(下一轮pop出的元素)</em> 组合是否是更small的range  
2. < 现存的上界限  
&nbsp;此时x所在array一定和上界限up所在array不是同一个array（因为是有序array，故新push进heap的element一定比已经pop出heap的同array的element数值要大）；  
&nbsp;所以x一定比下界low要大，则可以帮助使得现存range变小

```python

def smallestRange(arrays):
    heap = []
    k = len(arrays)
    
    max_val = -float('inf')
    for i in range(len(arrays)):
        if len(arrays[i]):
            heap.append((arrays[i][0], i, 0))
            max_val = max(arrays[i][0], max_val)
    heapq.heapify(heap)
    
    res = [-float('inf'), float('inf')]
    while len(heap) == k:  # 因为出去的是第x个array的值，进来的是第x个array下一大的值，如果没有了，表示第x个array里用来参与决策range的元素用完了
                           # 故这里的k帮助确保range是由k个array里的元素共同确定的
        min_val, array_idx, ele_idx = heapq.heappop(heap)
        
        if max_val - min_val < res[1] - res[0]:
            res = [min_val, max_val]
        if ele_idx + 1 < len(arrays[array_idx]):
            max_val = max(max_val, arrays[array_idx][ele_idx + 1])
            heapq.heappush(heap, (arrays[array_idx][ele_idx + 1], array_idx, ele_idx + 1))
    return res

```
