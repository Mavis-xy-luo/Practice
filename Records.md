# Prblems Recodes

**[696](https://leetcode.com/problems/count-binary-substrings/)**
```python

def countBinarySubstrings(self, s):
    prev = 0   # 前面一个出现的数据类别的数目
    cur = 1   # 目前正在走的数据类别的计数（走到目前走的指针和后一位数据类别不一样时停止计数，得到此数据种类的数目）
    count = 0
        
    for i in range(1, len(s)):
        if s[i] != s[i-1]:
            count += min(prev, cur)
            prev = cur
            cur = 1
        else:
            cur += 1
                
    return count +min(prev, cur)

```

****
