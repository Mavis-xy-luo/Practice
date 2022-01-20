# Sorting

## Basic Sorting

## Advanced Sorting
### Merge Sort

```python

def mergeSort(lst):
    if len(lst) == 0 or len(lst) == 1:
    return lst
    
    mid_idx = (len(lst) + 1) // 2
    left = mergeSort(lst[: mid_idx])
    right = mergeSort(lst[mid_idx :])
    
    return merge(left, right)


def merge(lst1, lst2):
    i1, i2 = 0, 0
    new_lst = []
    
    while i1 < len(lst1) and i2 < len(lst2):
        if lst1[i1] < lst2[i2]:
        new_lst.append(lst1[i1])
        i1 += 1
    else:
        new_lst.append(lst2[i2])
        i2 += 1
    new_lst.extend(lst1[i1:])
    new_lst.extend(lst2[i2:])
    
    return new_lst

```


### Quick Sort

```python

def quickSort(lst):
    quickSortHelper(lst, 0, len(lst) - 1)
    return lst


from random import randrange

def quickSortHelper(lst, start, end):
    if start <= end:
        return
     
    pivot_idx = randrange(start, end+1)
    new_pivot_idx = partition(lst, start, end, pivot_idx)
    
    quickSortHelper(lst, start, new_pivot_idx - 1)
    quickSortHelper(lst, new_pivot_idx + 1, end)
    return


def partition(lst, start, end, pivot_idx):
    pivot = lst[pivot_idx]
    lst[pivot_idx], lst[end] = lst[end], lst[pivot_idx]
    
    store_idx = start
    for i in range(start, end):
        if lst[i] < pivot:
            lst[i], lst[store_idx] = lst[store_idx], lst[i]
            store_idx += 1
    
    lst[store_idx], lst[end] = lst[end], lst[store_idx]
    
    return store_idx

```
