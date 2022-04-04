# Prblems Recodes

### 2 Sum
**Basic 2 sum**  
Determine if there exist two elements in a given array, the sum of which is the given target number.
> 用一个set存看过的数据，每次走到新的数时，看和target的差是否在set里，O(n)
```python
def existSum(lst, target):
    if not lst:
        return False
        
    s = set()
    for num in lst:
        if target - num in s:
            return True
        s.add(num)
    return False

```
****

**[2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)** <br>
用carry记录进位 <br>
用val记录当前相加位应该得到的值(node1.val + node2.val + carry)

**[43. Multiply Strings](https://leetcode.com/problems/multiply-strings/)** <br>
怎么得到结果存在[i + j + 1]位？？？？？？

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

**[394 Decode String](https://leetcode.com/problems/decode-string/)**
```
此题中括号是跟着走的，但不是字母（数字和括号是匹配的，单数字母和括号/数字和字母不匹配）所以操作如下：
1）遇到num

2）遇到char

3）遇到[
   此时nums append "["前的num，
      strs append "["前的chars（因为接下来str要记录后面的字母，后面这些字母才是和"["前的num匹配的

4）遇到]
   此时表示一段连续的字母的结束，这串连续的字母需要和[前的数字想乘，
   故：nums pop出来一个——count
      count * []内的str，并和前面的str相接，即str pop() + count * str
```

```python

```
