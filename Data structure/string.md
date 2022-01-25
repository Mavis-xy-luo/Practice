# String

## 常见string操作

## 常见string题目
removal, de-dupilcation, reversal, strstr


### 1. Removal
1. Remove some particular chars from a string



2. Remove empty spaces  
Remove all leading/trailing and duplicate empty spaces(only leave one empty space if duplicated spaces heappen from the input string).
```python

def remove_space(st):
    if not st:
        return st
    
    lst = list(st)
    i = 0
    j = 0
    
    while j < len(lst):
        if lst[j] != " " or (i != 0 and lst[i-1] != " "):
            lst[i] = lst[j]
            i += 1

        j += 1
        
    if i > 0 and lst[i-1] == " ":
        return "".join(lst[:(i-1)])
    return "".join(lst[:i])

```


### 2. De-duplication
1. 消除连续重复的chars只保留1个
Remove duplicated and adjacent letters (leave only one letter in each duplicated section) in a string.
```python

def deDuplication(st):
    if not st:
        return st
    
    lst = list(st)
    i = 1
    j = 1
    
    while j < len(st):
        if i > 0 and lst[j] != lst[i-1]:
            lst[i] = lst[j]
            i += 1
        j += 1
        
    return "".join(lst[:i])

```

2. 消消乐（消除后遇到重复接着消）
De-duplication adjacent letters repeatedly
```python

def deDuplicateRepeatedly(st):
    if not st or len(st) < 2:
        return st
    
    stack = []
    i = 0
    while i < len(st):
        if len(stack) > 0 and st[i] == stack[-1]:
            while i < len(st) and st[i] == stack[-1]:
                i += 1
            stack.pop()
        else:
            stack.append(st[i])
            i += 1
    return "".join(stack)
    
# 下面是错误答案：错在一遇到重复的就把之前存进去的pop掉了，再进来的则变成没有重复的了
# stack = [b1], b2进来, stack = [], b3进来，stack没有和其重复的，所以错误

def deDuplicateRepeate(st):
    if not st or len(st) < 2:
        return st
    
    stack = []
    for i in range(len(st)):
        if not stack or (stack and st[i] != stack[-1]):
            stack.append(st[i])
        else:
            stack.pop()
    return "".join(stack)

```


### 3. Reversal / Swap
1. reverse整句话

3. 只reverse单词顺序，不reverse单词里的chars
```python



```

### 4. Substring / Strstr
长串里是否有子串，返回子串所在第一个字符的位置

```python


```

