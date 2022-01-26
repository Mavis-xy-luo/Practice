# 各数据结构题型总结
from：https://www.1point3acres.com/bbs/thread-840864-1-1.html
<ul><li>- [ ]  </li></ul>


## 一、数组和字符串相关 （array & string）
1. 括号相关题（另外见【栈】）
   921. Minimum Add to Make Parentheses Valid， 1249. Minimum Remove to Make Valid Parentheses
2. 排列（组合） Permutation
3. 区间题 Intervals [left, right, val]
   - [ ] 1. 按左右端点排序的思想 
        - [ ] 252. Meeting Rooms
   - [ ] 2. 插入，合并，删除区间： 
       - [ ] 56. Merge Intervals,
       - [ ] 57. Insert Interval,
       - [ ] 1272. Remove Interval,
       - [ ] 435. Non-overlapping Intervals
    4. 安排会议/任务  253. Meeting Rooms II， 1235 Maximum Profit in Job Scheduling， 2054 Two Best Non-Overlapping Events
区间更新 1094. Car Pooling
常规双指针
15 3Sum，
75 Sort Colors（Dutch national flag problem 经典题
1229 Meeting Scheduler，
680 Valid Palindrome II，
408 Valid Word Abbreviation. From 1point 3acres bbs
滑动窗口 Sliding window 模板
3 Longest Substring Without Repeating Characters
76 Minimum Window Substring
1004 Max Consecutive Ones III
209  Minimum Size Subarray Sum
1438 Longest Continuous Subarray With Absolute Diff Less Than or Equal to Limit
Subsequence-baidu 1point3acres
Greedy drop idea: 392 Is Subsequence， 792 Number of Matching Subsequences
经典题 727. Minimum Window Subsequence
940 Distinct Subsequences II
Subarray、substring （连续的）
Rolling hash （Rabin-Karp） 1062. Longest Repeating Substring， 1044. Longest Duplicate Substring
排列组合
46 Permutations, 31. Next Permutation
77 Combinations
Subset
78 Subsets
368 Largest Divisible Subset
数据流相关的问题
top k 问题 --> heap; buck sort -->  distributed system:
1146 Snapshot Array  (打version tag + binary search）
359 Logger Rate Limiter
LRU, LFU
Median 295. Find Median from Data Stream
Iterator  284. Peeking Iterator, 900. RLE Iterator
Bitmask 用bit来表示状态 847. Shortest Path Visiting All Nodes

## 1. 图 Graph
图的遍历  BFS ,  DFS ,  准备模板
图--三类
常规的node和edge的图, 建adj matrix然后遍历  (690. Employee Importance)
把矩阵看成图, 4周neighbor相连 （0-1 Islands系列, 79. Word Search, 417. Pacific Atlantic Water Flow）
把data(state)看成node, 把操作operation看成edge (127. Word Ladder, 1345. Jump Game IV) , 这种思路很多时候就变成了动态规划题
拓扑排序（topological sort) 准备模板. From 1point 3acres bbs
决定nodes先后顺序(关系) （210. Course Schedule II， 269. Alien Dictionary）
判断有向图是否有cycle (207. Course Schedule)
判断无向图是否有cycle (1192. Critical Connections in a Network)
图二分染色 (785. Is Graph Bipartite?)
最短（最长）路径
经典BFS题 994. Rotting Oranges, 909. Snakes and Ladders, 1091. Shortest Path in Binary Matrix, 1293. Shortest Path in a Grid with Obstacles Elimination
Dijkstra （用heap 写，准备模板） （1631. Path With Minimum Effort， 1066. Campus Bikes II）
并查集Union Find  准备模板
用于快速合并图的不同components （305. Number of Islands II）
用于快速判断两个nodes是不是连通
回溯法 Backtracking 本质就是想象成图，然后递归的DFS（有时可以剪枝）  526. Beautiful Arrangement, 22. Generate Parentheses
binarysearch+BFS： 用binary search 查找答案，然后在限制条件下做BFS。类似的用binary search 查找答案的思路见【7. 搜索和查询 中的binary search部分】
1102 Path With Maximum Minimum Value
778  Swim in Rising Water
1631 Path With Minimum Effort


2. 树 Tree
树的遍历
DFS (binary tree: in-order, pre-order,  post-order)
BFS: 314. Binary Tree Vertical Order Traversal， 199. Binary Tree Right Side View
递归大法 (大部分树的题都能递归，大的问题(root)，等于先解决几个子问题（subtree), 然后合并）:
124 Binary Tree Maximum Path Sum，
366 Find Leaves of Binary Tree
Lowest Common Ancestor系列
Binary Search Tree 判断和快速查找元素 98. Validate Binary Search Tree
树的编码和解码
297 Serialize and Deserialize Binary Tree
428 Serialize and Deserialize N-ary Tree
把树变成图： 863. All Nodes Distance K in Binary Tree
. check 1point3acres for more.


3. 动态规划 Dynamic Programming
有状态转化方程，可以把大问题转化为几个小问题，或者可以按某种顺序依次解决问题。（用图的思想，data是node, operation是edge）
常见思路
用dp代表关于arr[0:i]的subproblem  (只到i 或者 从i开始的subproblem）
用dp[j] 代表关于arr[i:j+1]的subproblem （或者是关于两个数组的 arr[0:i] 和 arr2[0:j]的subproblem, 或者关于两个变量i,j的subproblem）
经典DP题目
LIS: 300. Longest Increasing Subsequence O(nlogn)  (2D version: 354. Russian Doll Envelopes)
LCS: 1143. Longest Common Subsequence
Longest Substring Without Repeating Characters
字符串操作： 72. Edit Distance， 44. Wildcard Matching, 10. Regular Expression Matching
Palindrome problems: 647. Palindromic Substrings, 5. Longest Palindromic Substring
Prefix sum/max/min 相关： 42. Trapping Rain Water, 1423. Maximum Points You Can Obtain from Cards， Range Sum Query - Immutable, 304. Range Sum Query 2D - Immutable
Word Break 系列
硬币零钱系列 Coin Change
买股票系列 Best Time to Buy and Sell Stock
跳跃游戏系列 Jump games
抢劫系列 House Robber
石头游戏系列（Alice & Bob) Stone Game
Unique Paths 系列
688 Knight Probability in Chessboard
摘樱桃 Pick cherry
174  Dungeon Game
1277 Count Square Submatrices with All Ones
加油站问题 871. Minimum Number of Refueling Stops


4. 堆 Heap, 栈 Stack, 队 Queue
栈 Stack
常规题
946 Validate Stack Sequences
Asteroid Collision
括号题
Valid Parentheses, Remove Invalid Parentheses
Basic Calculator 系列
Nested List Iterator 系列
Decode String， Number of Atoms
单调栈
Next Greater Element 系列
402 Remove K Digits
853 Car Fleet
739 Daily Temperatures
堆 Heap
Top k： 215. Kth Largest Element in an Array， 347. Top K Frequent Elements
中位数： double heap 295. Find Median from Data Stream
另外一道经典中位数题目 4. Median of Two Sorted Arrays
会议室问题 253. Meeting Rooms II
CPU分配 模板: LC 1834. Single-Threaded CPU, LC 1882. Process Tasks Using Servers
队 Queue, Deque
BFS related
239 Sliding Window Maximum  ---> 2D sliding window maximum ( 转化成两次1D的问题）
Moving Average from Data Stream


5. 链表 LinkedList
Fast and Slow pointer  (detect cycle, get middle,  get kth element)
141 Linked List Cycle
19 Remove Nth Node From End of List
Reverse Linked List (trick: dummy head)  206 Reverse Linked List, 25 Reverse Nodes in k-Group
LRU cache
Deep copy  (138 Copy List with Random Pointer)
Merge LinkedList  (2. Add Two Numbers)

6. 排序 Sort
Merge sort
非常规高频题 315 Count of Smaller Numbers After Self  --> (google题： 一堆点, 对每个点(x,y)数【严格大 (x,y)<(u,v)】的点的个数. 思路：先排序，x增序，y减序，然后把y单独拿出来看，对每个点数右边有多少大的元素，变成问题315 with bigger numbers after self)
Quick Sort --> QuickSelect O(n) time on average) 973. K Closest Points to Origin
Bucket Sort O(n) 通常是整体数据量可能很大，但是unique元素有限
Cycle Sort O(n) 通常是用于把0到n-1在array中排序 （不断交换的想法）
Python built-in sort
OrderedDict (linked list + hash) --> 自己实现： 用 hashtable 存double linkedlist 的 node
sorted containers (sorted list, sorted dict, sorted set)


7. 搜索和查询 Search and Query
hash (python: dictionary, set):
O(1)查找，
记录unique element的frequency
binary search  左开右闭模板
data是有顺序的，每次可以缩小搜索范围。 经典题：
33 Search in Rotated Sorted Array，
153 Find Minimum in Rotated Sorted Array，
162 Find Peak Element
解的范围是一个区间可以二分搜索
Binary search + greedy: 1231 Divide Chocolate, 1011 Capacity To Ship Packages Within D Days, 410. Split Array Largest Sum
378 Kth Smallest Element in a Sorted Matrix
-baidu 1point3acres
经典题 Search a 2D Matrix 系列
字典树 Trie 模板 （单词相关的查找）： 642. Design Search Autocomplete System， 472. Concatenated Words， 212. Word Search II
Range Query (Segment Tree 模板)  307. Range Sum Query - Mutable





补充内容 (2022-01-20 13:20 +8:00):
最近转码上岸了，总结了一下我做过的一些有代表的力扣题，回馈地里，希望对大家有帮助！-baidu 1point3acres
另外还有一篇【转码找工作的资料总结】还在审核中
链接： https://www.1point3acres.com/bbs/thread-840857-1-1.html
补充内容 (2022-01-21 02:13 +8:00):
转码资料的帖子通过审核啦！
Dynamic programming 那儿格式出了点问题，应该是 dp 和 dp[j] 这两种最常见的方式
补充内容 (2022-01-21 03:51 +8:00):
还是有问题。。。。
是 dp_i   和 dp_i,j
