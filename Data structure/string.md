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
```python

def reverseString(string):
    if not string or len(string) < 2:
        return string
    
    lst = list(string)
    l = 0
    r = len(lst) - 1
    
    while l <= r:
        lst[l], lst[r] = lst[r], lst[l]
        l += 1
        r -= 1
    
    return "".join(lst)

```

3. 只reverse单词顺序，不reverse单词里的chars
```python

def reverseWords(string):
    if not string or len(string) < 2:
        return string
    
    lst = list(string)
    reverseHelper(lst, 0, len(lst)-1)
    
    l = 0
    r = 0
    i = 0
    
    while i < len(lst):
        if i == len(lst) - 1 or lst[i+1] == " ":
            r = i
            reverseHelper(lst, l, r)
            l = i + 2
        i += 1
    return "".join(lst)   
    

def reverseHelper(lst, l, r):
    while l < r:
        lst[l], lst[r] = lst[r], lst[l]
        l += 1
        r -= 1
    return

```

### 4. Substring / Strstr
长串里是否有子串，返回子串所在第一个字符的位置

```python
# 1. 暴力求解 O(m*n)
def bruteSolve(string, pattern):
    if not string or not pattern or len(string) < len(pattern):
        return -1
    
    end = len(string) - len(pattern) + 1# end cannot be arrive
    for i in range (end):
        if string[i] == pattern[0]:
            for j in range(len(pattern)):
                if string[i+j] != pattern[j]:
                    res = False
                    break
                res = True
            if res == True:
                return i
    return -1


# 2.1 RabinKarp O(m+n)
def RabinKarp(string, pattern):
    if not string or not pattern or len(string) < len(pattern):
        return -1
    
    dic = {"a":0, "b":1, "c":2, "d":3, "e":4, "f":5, "g":6, 
           "h":7, "i":8, "j":9, "k":10, "l":11, "m":12, "n":13, 
           "o":14, "p":15, "q":16, "r":17, "s":18, "t":19, 
           "u":20, "v":21, "w":22, "x":23, "y":24, "z":25}
    
    # 计算pattern的“hash”值
    # 计算从0位开始的和pattern等长的substring的”hash“值
    val_p = 0
    val_s = 0
    for i in range(len(pattern)):
        val_p = val_p * 26 + dic[pattern[i]]
        val_s = val_s * 26 + dic[string[i]]
    
    # 比较计算结果，相等返回0位
    if val_s == val_p:
        return 0
    
    # 从len(pattern)的位值开始循环到string的最后一位，看“hash”值是否相等
    else:
        n = len(pattern) # 位数
        for j in range(len(pattern), len(string)):
            # “(上一个”hash“值 - 最高位数值*进位值^(位数-1) ) * 进位值 + 新的最低位值
            val_s = (val_s -  dic[string[j-n]] * 26**(n-1))*26 + dic[string[j]]

            if val_s == val_p:
                return j - len(pattern) + 1 # 子串的第一位 = 现在计算的“hash”值的位数(即子串最后一位) - pattern长度 + 1
        return -1
        
                
# 2.2 RobinKarp(取模)
class RabinKp(object):
    def __init__(self):
        self.base = 26
        self.mod = 997
    
    def strstr(self, string, pattern):
        if len(pattern) > len(string):
            return -1
        s_hash, p_hash = 0, 0
        
        power = 1
        
        for i in range(len(pattern)):
            power = power * self.base % self.mod if i != 0 else 1
            
            s_hash = (s_hash * self.base + ord(string[i])) % self.mod          
            p_hash = (p_hash * self.base + ord(pattern[i])) % self.mod
        
        for i in range(len(pattern), len(string)):
            # 如果substring的hash值 = pattern的hash值，比对substring是否=pattern
            if s_hash == p_hash and pattern == string[i - len(pattern) : i]:
                return i - len(pattern)
            
            s_hash -= (power * ord(string[i - len(pattern)])) % self.mod
            
            if s_hash < 0:
                s_hash += self.mod
            s_hash = (s_hash * self.base + ord(string[i])) % self.mod
            
        if s_hash == p_hash and pattern == string[len(string) - len(pattern):]:
            return len(string) - len(pattern)
        return -1

# 3. KMP

```

