## 算法秋招复习（leetcode、 剑指offer）
```
总结:
【二分查找】
4. Median of Two Sorted Arrays
81. Search in Rotated Sorted Array II
154. Find Minimum in Rotated Sorted Array II
287. Find the Duplicate Number
540. Single Element in a Sorted Array

【排序】
147. Insertion Sort List 
148. Sort List

【搜索】
22. Generate Parentheses
47. Permutations II
79. Word Search
93. Restore IP Addresses
127. Word Ladder
130. Surrounded Regions
131. Palindrome Partitioning
200. Number of Islands

【动态规划】
91. Decode Ways
123. Best Time to Buy and Sell Stock III
139. Word Break
152. Maximum Product Subarray
174. Dungeon Game
221. Maximal Square
279. Perfect Squares
300. Longest Increasing Subsequence
322. Coin Change
377. Combination Sum IV
416. Partition Equal Subset Sum
474. Ones and Zeroes
最长公共子序列/子串

【数据结构】
2. Add Two Numbers
3. Longest Substring Without Repeating Characters
20. Valid Parentheses
31. Next Permutation
73. Set Matrix Zeroes
80. Remove Duplicates from Sorted Array II
82. Remove Duplicates from Sorted List II
92. Reverse Linked List II
95. Unique Binary Search Trees II
96. Unique Binary Search Trees
109. Convert Sorted List to Binary Search Tree
111. Minimum Depth of Binary Tree
113. Path Sum II
114. Flatten Binary Tree to Linked List
117. Populating Next Right Pointers in Each Node II
205. Isomorphic Strings
222. Count Complete Tree Nodes
229. Majority Element II
232. Implement Queue using Stacks
378. Kth Smallest Element in a Sorted Matrix
594. Longest Harmonious Subsequence
617. Merge Two Binary Trees

【其他】
6. ZigZag Conversion
15. 3Sum
16. 3Sum Closest
29. Divide Two Integers
75. Sort Colors
89. Gray Code
137. Single Number II
201. Bitwise AND of Numbers Range
209. Minimum Size Subarray Sum

【数学】
12. Integer and Roman
13. Roman to Integer
60. Permutation Sequence
168. Excel Sheet Column Title
171. Excel Sheet Column Number
204. Count Primes
223. Rectangle Area 
343. Integer Break

【贪心】
134. Gas Station
406. Queue Reconstruction by Height
665. Non-decreasing Array
763. Partition Labels 

【剑指 offer】
1. 字符流中第一个不重复的字符
2. 丑数
3. 孩子们的游戏(圆圈中最后剩下的数)
4. 不用加减乘除做加法
5. 二叉树的下一个结点
6. 机器人的运动范围
7. 二叉搜索树与双向链表
8. 数组中的逆序对
9. 正则表达式匹配
10. 表示数值的字符串
11. 序列化二叉树
12. 滑动窗口的最大值
```

## 20190811
### 链表的插入排序 (147. Insertion Sort List)
```python
def sortList(head):
    if not head or not head.next:
        return head
    dummy = ListNode(0)
    dummy.next = head
    cur = head
    while cur.next:
        tmp = cur.next # 待插入节点，前面的节点都已经有序
        if tmp.val >= cur.val:
            cur = cur.next # 有序的情况直接判断下一个，否则进行调整，找到插入点
        else:
            pre = dummy
            while tmp.val >= pre.next.val:
                pre = pre.next
            cur.next = cur.next.next
            tmp.next = pre.next # 注意这里，tmp 要插入 pre 和 pre.next 之间
            pre.next = tmp
    return dummy.next
```

### 链表的归并排序 (148. Sort List)
这题要求时间复杂度 O(nlogn), 空间复杂度 O(1)

链表的归并排序不需要像数组一样开辟一个新的存储空间来存储一次二路归并的结果，只需要改变指针的指向即可。

可以用快慢指针法找到链表的终点，然后将链表划分为左右两部分，再递归将链表分成单位长度为 1 的部分。
```python
class Solution:
    def sortList(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        fast = slow = head
        while fast.next and fast.next.next:
            fast = fast.next.next
            slow = slow.next
        right = self.sortList(slow.next)
        slow.next = None
        left = self.sortList(head)
        return self.merge(left, right)
        
    def merge(self, head1, head2):
        dummy = ListNode(0)
        cur = dummy
        while head1 and head2:
            if head1.val <= head2.val:
                cur.next = head1
                head1 = head1.next
            else:
                cur.next = head2
                head2 = head2.next
            cur = cur.next
        if head1:
            cur.next = head1
        if head2:
            cur.next = head2
        return dummy.next
```

## 二分查找及其变种
1. 循环条件都是 while left <= right
2. 找第一个等于，第一个大于等于，判断条件都是 if nums[mid] >= target
   第一个大于： nums[mid] > target， 都是返回 left
   最后要注意判断一下 left 是否越界，return left if left < len(nums) else -1

3. 找最后一个等于，最后一个小于等于，判断条件都是 nums[mid] <= target
   最后一个小于： nums[mid] < target，都是返回 right
   需要判断 right 是否越界，return right if right >= 0 else -1

### 34. Find First and Last Position of Element in Sorted Array
```python
def searchRange(self, nums: List[int], target: int) -> List[int]:
    if not nums:
        return [-1, -1]
    left, right = 0, len(nums) - 1
    while left <= right:
        mid = left + (right-left) // 2
        if nums[mid] >= target:
            right = mid - 1
        else:
            left = mid + 1
    if left >= len(nums) or nums[left] != target: # 注意找不到的情况有两种
        return [-1, -1]
    # 要求时间复杂度为 O(nlogn)，所以不能找到一个再往后面遍历，因为全部为一样的数字时会退化为 O(n)
    # right = left
    # while right < len(nums)-1 and nums[right] == nums[right+1]:
    #     right += 1
    # return [left, right]
    l = left
    right = len(nums) - 1
    while left <= right:
        mid = left + (right-left) // 2
        if nums[mid] <= target:
            left = mid + 1
        else:
            right = mid - 1
    return [l, right]
```

### 旋转数组的查找
#### 33. Search in Rotated Sorted Array
无重复数字，根据 nums[mid] 和 nums[left] 比较，来判断哪边是有序的，然后再分区间判断，情况较多
```python
def search(self, nums: List[int], target: int) -> int:
    if not nums:
        return -1
    left, right = 0, len(nums)-1
    while left <= right:
        mid = left + (right-left) // 2
        if nums[mid] == target:
            return mid
        if nums[mid] >= nums[left]: # 注意这里，mid 可能等于 left，别忘了等号！！！
            if target > nums[mid]:
                left = mid + 1
            else:
                if target >= nums[left]:
                    right = mid - 1
                else:
                    left = mid + 1
        else:
            if target < nums[mid]:
                right = mid - 1
            else:
                if target <= nums[right]:
                    left = mid + 1
                else:
                    right = mid - 1
    return -1
```

数组中有重复数字的话，与上一题相比只需要增加一步，也就是 nums[mid] == nums[left] 时，比如 [1,3,1,1,1]，或者 [1,1,1,3,1]，要去找 3，就无法判断到底是左边作序还是右边有序，因此额外讨论，此时只能让 left+1
```python
def search(self, nums: List[int], target: int) -> bool:
    if not nums:
        return False
    left, right = 0, len(nums)-1
    while left <= right:
        mid = left + (right-left)//2
        if nums[mid] == target:
            return True
        if nums[mid] == nums[left]: # 上一题直接一起讨论 nums[mid]>=nums[left] 是因为 mid == left，下标是相同的，但是这题数字有重复，相等的时候没办法判断到底哪边是有序的
            left += 1 # 只有此处与上题不同，下面的判断逻辑是一样的
        elif nums[mid] > nums[left]:
            if target > nums[mid]:
                left = mid + 1
            else:
                if target >= nums[left]:
                    right = mid - 1
                else:
                    left = mid + 1
        else:
            if target < nums[mid]:
                right = mid - 1
            else:
                if target <= nums[right]:
                    left = mid + 1
                else:
                    right = mid - 1
    return False
```

#### 旋转数组的最小数字
1. 无重复数字（leetcode）
```python
def findMin(self, nums: List[int]) -> int:
    if not nums:
        return 
    left, right = 0, len(nums)-1
    if nums[left] < nums[right]: # 没旋转
        return nums[left]
    while left + 1 < right: # 循环终止时，left 指向最大值，right 指向最小值
        mid = left + (right-left) // 2
        if nums[mid] > nums[left]:
            left = mid
        else:
            right = mid
    return nums[right]
```
2. 有重复数字
注意最特殊的情况：nums[left] == nums[mid] and nums[right] == nums[mid] 时
可能是 [1,0,1,1,1] 或 [1,1,1,0,1] 或 [1,1,1,1,1]

```python
def findMin(self, nums: List[int]) -> int:
    if not nums:
        return 
    left, right = 0, len(nums)-1
    if nums[left] < nums[right]:
        return nums[left]
    while left + 1 < right:
        mid = left + (right-left) // 2
        if nums[left] == nums[mid] and nums[right] == nums[mid]: # 只能顺序查找
            for i in range(left+1, right+1):
                if nums[i] < nums[left]:
                    return nums[i] # 找到第一个比 nums[left] 小的数，就是最小的数
                if i == right: # 全部是一样的数字的情况
                    return nums[right]
        elif nums[mid] >= nums[left]:
            left = mid
        else:
            right = mid
    return nums[right]
```

#### 287. Find the Duplicate Number
限制条件较多：要求时间小于 O(n^2)，空间为 O(1)，且不能修改数组；也就是说时间要 O(nlogn)

已知有 n+1 的数字，数字的都是在 [1, n] 区间中的，只有一个数字是重复的，这个数字可能重复多次

思路： 可以先找到 [1, n] 区间的中间数 mid = (n+1)//2， 然后计算 nums 中比 mid 更小的数的个数，如果超过数组的一半，那么说明重复数字在左边； 否则在右边

比如 nums = [3,3,1,3,4,2] ，区间是 [1,2,3,4,5]
第一轮 left = 1，right = 5， mid = 3，计算 nums 中小于等于 mid 的个数，如果这个数比 mid 更大，那么就说明重复数字在 [left, mid]； 否则就在 [mid+1, right] 中

```python
def findDuplicate(self, nums: List[int]) -> int:
    left, right = 1, len(nums)-1
    while left < right:
        mid = left + (right-left)//2
        cnt = 0
        for i in range(len(nums)):
            if nums[i] <= mid:
                cnt += 1
        if cnt > mid:
            right = mid
        else:
            left = mid + 1
    return left       
```

### 540. Single Element in a Sorted Array
题意： 数组中除了某个数只出现一次，其余的数都出现了两次，找出这个数，要求时间复杂度为 O(logn), 空间 O(1)

思路： 由于有时间复杂度限制，不能用异或方法（因为要遍历一遍数组，时间 O(n)）
显然时间 O(logn) 需要用二分查找，固定一个数 nums[mid], 通过比较他与前后的数字是否相等，来判断单数字出现在左边还是右边区间。

```python
def singleNonDuplicate(self, nums: List[int]) -> int:
    if not nums:
        return
    if len(nums) == 1:
        return nums[0]
    left,right = 0, len(nums)-1
    while left < right:
        mid = left + (right-left) // 2
        if nums[mid] != nums[mid-1] and nums[mid] != nums[mid+1]:
            return nums[mid]
        elif (mid % 2 == 0 and nums[mid] == nums[mid+1]) or (mid % 2 == 1 and nums[mid] == nums[mid-1]): # 注意这里的情况比较复杂，需要自己举例子去找出，mid 是奇数还是偶数需要考虑
            left = mid + 1
        else:
            right = mid - 1
    return nums[left]
```

## 20190812
### 搜索-回溯
#### 生成括号 22. Generate Parentheses
题意： 给定整数 n，也就是给的左括号和右括号都是 n 个，求出所有能够生成的正确的括号

思路： 初始的左括号和右括号数量都是 n，在生成括号的过程中，肯定是左括号先用的，那么剩余的左括号数量肯定是小于或等于右括号数量的，当用了一个左括号，就给 string+'('
```python
def generateParenthesis(self, n: int) -> List[str]:
    if not n:
        return []
    
    def dfs(left, right, string):
        if left > right: # 剩余的左括号数大于右括号数时，右括号会在左括号前面，不符合条件。
            return 
        if left == 0 and right == 0:
            res.append(string)
            return 
        if left:
            dfs(left-1, right, string+'(')
        if right:
            dfs(left, right-1, string+')')
    
    res = []
    dfs(n, n, "")
    return res
```

#### 47. Permutations II
给定一个有重复数字的数组，如 [1,1,2]， 给出元素能组成的所有的排列

本题要注意加快效率的方法，有重复的数字会和之前的数字得到相同的结果，因此可以跳过。
```python
def permuteUnique(self, nums: List[int]) -> List[List[int]]:
    if not nums:
        return []
    def dfs(nums, arr):
        if not nums and arr not in res:
            res.append(arr)
            return 
        for i in range(len(nums)):
            if i > 0 and nums[i] == nums[i-1]: 
                continue # 遍历到重复数字就跳过，因为 nums[i] 会和 nums[i-1] 得到相同的结果
            dfs(nums[:i]+nums[i+1:], arr+[nums[i]])
    res = []
    nums.sort() # 先排序
    dfs(nums, [])
    return res
```

### N 皇后问题（51.52. N-Queens）
一行行的放置皇后，在 i,j  位置上放皇后的时候，需要满足同一行、同一列、同一对角线上没有皇后。

用一个二维数组 board[i][j] = 1 来表示第 i,j 位置上放了皇后

```python
def solveNQueens(self, n: int) -> List[List[str]]:
    def check(i, j):
        for row in range(i): # 前 i 行
            if board[row][j] == 1: # 判断是否同一列有皇后
                return False
            for col in range(n):
                 if (board[row][col] == 1 and abs(row-i)==abs(col-j)): # 判断同一对角线
                    return False
        return True
    
    def dfs(row, arr):
        if row == n:
            res.append(arr)
            return
        for j in range(n):
            if check(row, j):
                board[row][j] = 1
                s = '.' * j + 'Q' + '.' * (n-j-1)
                dfs(row+1, arr+[s])
                board[row][j] = 0 # 用二维数组存储，当遍历完这个节点发现不能放后，或者已经全部遍历完了一遍，找到了一个解后，这个位置要置为原样，表示现在不能放置。
    board = [[0 for _ in range(n)] for _ in range(n)]           
    res = []
    dfs(0, [])
    return res
```

优化空间复杂度，可以使用一维数组来存储，用 board[i] = j, 表示第 i 行，第 j 列放了皇后
```python
def solveNQueens(self, n: int) -> List[List[str]]:
    def check(row, j):
        for i in range(row):
            if board[i] == j or abs(row-i) == abs(j-board[i]): # 直接可以一起判断
                return False
        return True
    
    def dfs(row, arr):
        if row == n:
            res.append(arr)
            return
        for j in range(n):
            if check(row, j):
                board[row] = j # 表示第 row 行，第 j 列放置了皇后
                s = '.' * j + 'Q' + '.' * (n-j-1)
                dfs(row+1, arr+[s])
                board[row] = -1
    board = [-1 for _ in range(n)] # 改一维数组，初始化为 -1，因为 0,0 位置可能放              
    res = []
    dfs(0, [])
    return res         
```

如果把题目改成输出有多少种可行的结果，那么要用 __init__ 先初始化一个 self.res = 0，然后在回溯函数中，符合条件就让 self.res + 1

## 20190813
### 搜索
#### 93. Restore IP Addresses
题意： 给定一个字符串 s，将其划分为合法的 ip 地址

思路： ip 地址分为四部分，每个部分长度都是 1-3 位，大小为 0-255

```python
def restoreIpAddresses(self, s):
    if len(s) > 12:
        return []
    res = []
    def dfs(s, ip):
        if not s and len(ip) == 4:
            res.append('.'.join(ip))
        for i in range(1, 4):
            if i <= len(s):
                number = int(s[:i])
                if number <= 255 and str(number) == s[:i]:
                    dfs(s[i:], ip+[s[:i]])
            else:
                break
    dfs(s, [])
    return res
```

#### 127. Word Ladder
题意： 给定两个单词 begin 和 end，以及一个数组，求用数组中的单词，使 begin 变为 end 需要转变的最少的次数，每次可以改变 begin 中的一个单词，但变换的词都是给定数组中的

思路：

```python

```

#### 131. Palindrome Partitioning
给出 s，输出 s 的所有回文子串分割
```python
def partition(self, s):
        res = []
        def dfs(s, arr):
            if not s:
                res.append(arr)
                return 
            for i in range(len(s)):
                a = s[:i+1]
                if a == a[::-1]: # 简单法判断回文子串
                    dfs(s[i+1:], arr+[s[:i+1]])
        dfs(s, [])
        return res
```

#### 130. Surrounded Regions
题意： 将二维数组 board 中被 'X' 包围的 'O' 全部改为 'X'

思路： 想一想什么地方的 'O' 是没有被 'X' 包围的？ 是处于边缘的 'O' 以及这个 'O' 去 DFS 找到的其他连通的 'O'
因此遍历第一行和最后一行，第一列和最后一列，找到 'O' 时，就把它变成另外一个字母 'A'，再去上下左右找其他连通的 'O'，这样遍历一遍所有边缘的 'O' 都变成了 'A'
再遍历一遍，把所有的 'O' 都变为 'X'，也就是被包围的； 把所有的 'A' 都变回原样，也就是 'O'

```python
def solve(self, board: List[List[str]]) -> None:
    if not board:
        return 
    n = len(board)
    m = len(board[0])
    
    def dfs(i, j):
        if i < 0 or i >= n or j < 0 or j >= m or board[i][j] != 'O': # 不要写成 board[i][j] == 'X'
            return # 当 board = [["O","O"],["O","O"]] 时，就会造成 RuntimeError: maximum recursion depth exceeded in cmp， 因为 board[i][j] == 'A' 时，就会一直循环下去，这个时候也要 return
        board[i][j] = 'A'
        dfs(i-1, j)
        dfs(i+1, j)
        dfs(i, j-1)
        dfs(i, j+1)
    
    for j in range(m):
        if board[0][j] == 'O':
            dfs(0, j)
        if board[n-1][j] == 'O':
            dfs(n-1, j)
            
    for i in range(1, n-1):
        if board[i][0] == 'O':
            dfs(i, 0)
        if board[i][m-1] == 'O':
            dfs(i, m-1)
            
    for i in range(n):
        for j in range(m):
            if board[i][j] == 'O':
                board[i][j] = 'X'
            elif board[i][j] == 'A':
                board[i][j] = 'O'
```

### 200. Number of Islands
题意： 1 代表岛屿，0 代表海水，找到 grid 中岛屿的个数

思路： 遍历二维数组，当遇到 1 时，就说明出现了一个岛屿，然后上下左右去 DFS 找到这个岛屿最大的范围，并把找到的 1 标记为 0（就是表明已经被访问过，这个岛已经计数了），一个岛屿就 res + 1； 然后再去找下一个。

```python
def numIslands(self, grid: List[List[str]]) -> int:
    def dfs(i, j):
        if i < 0 or i >= n or j < 0 or j >= m or grid[i][j] != '1':
            return 
        grid[i][j] = '0'
        dfs(i+1, j)
        dfs(i-1, j)
        dfs(i, j+1)
        dfs(i, j-1)
    
    n = len(grid)
    m = len(grid[0])
    res = 0
    
    for i in range(n):
        for j in range(m):
            if grid[i][j] == '1':
                dfs(i, j)
                res += 1
    return res
```

## 20190814
### 动态规划
#### 背包问题
一维费用的 01 背包，逆序遍历 j ; dp[j] = max(dp[j], dp[j-w[i]] + v[i])
一维费用的完全背包，正序遍历 j，和 01 的公式一样

二维费用的背包： dp[j][k] = max(dp[j][k], dp[j-w1[i]][k-w2[i]] + v[i])

#### 139. Word Break
题意：分割单词，给定字符串 s，如果 s 能被 wordDict 里面的单词分割开来，就返回 true

思路： 用 dp[i] 表示到第 i 个字符的时候能够被正确分割，初始 dp[0] = True
比如 leetcode，要想 dp[8] 被正确分割，那么就需要 dp[4] = True

dp[i] = True 的条件是： 某个单词刚好在 wordDict 中，且这个单词前的字符串能够被正确分割。

```python
def wordBreak(self, s: str, wordDict: List[str]) -> bool:
    dp = [False for i in range(len(s)+1)]
    dp[0] = True
    
    for i in range(1, len(s)+1):
        for word in wordDict:
            if i-len(word) >= 0 and s[i-len(word): i] == word and dp[i-len(word)]:
                dp[i] = True
    return dp[-1]
```

#### 322. Coin Change
题意： 给定零钱 coins，求出能够组成 amount 的最少的零钱个数，每个面值的零钱都有无数个

思路： 是一个完全背包问题，用 dp[j] 表示能够组成 j 的最少零钱数，要求最小值，那么初始化 dp 数组为无穷大。
写出转态转移公式 dp[i][j] = min(dp[i-1][j], dp[i][j-coins[i]]+1)

```python
def coinChange(self, coins: List[int], amount: int) -> int:
    dp = [float('inf')] * (amount+1)
    dp[0] = 0
    for i in range(len(coins)):
        for j in range(coins[i], amount+1): # 直接从 coins[i] 开始计数，减少计算
            dp[j] = min(dp[j], dp[j-coins[i]]+1)
    return dp[-1] if dp[-1] != float('inf') else -1
```

#### 377. Combination Sum IV
题意： 给定 nums，求用 nums 中的数能够组成 target 的解的个数

思路：本题用回溯解会超时，由于只要输出解的个数，不用输出每个解，因此用动态规划。
对于 nums = [1,3,5], target = 10 ，那么 dp[10] = dp[9] + dp[7] + dp[5]

```python
def combinationSum4(nums, target):
    dp = [0] * (target + 1)
    dp[0] = 1 # 想清楚为什么是 1
    for i in range(1, target + 1):
        for j in range(len(nums)):
            if i >= nums[j]:
                dp[i] += dp[i - nums[j]]
        print(dp)
    return dp[-1]
```

#### 416. Partition Equal Subset Sum
思路: 可以看到将 nums 放入一个 sum(nums)//2 的背包，得到的最大价值与之相等的话，就返回 true
```python
def canPartition(self, nums: List[int]) -> bool:
    if sum(nums) % 2 == 1:
        return False
    s = sum(nums) // 2
    dp = [0 for _ in range(s+1)]
    nums.sort()
    
    for i in range(len(nums)):
        if nums[i] > s:
            break
        for j in range(s, -1, -1):
            if j >= nums[i]:
                dp[j] = max(dp[j], dp[j-nums[i]] + nums[i])
            else:
                break
    return True if dp[-1] == s else False
```

#### 474. Ones and Zeroes
题意：给定一个字符串数组 strs，里面的字符串都是有 0 1 组成 ，用 m 个 0，n 个 1 组成 strs 中的字符串，求最多能组成多少个

思路： 二维费用的 0-1 背包，使用一个二维数组 dp 来存储，注意遍历 j，k 时是逆序遍历

```python
def findMaxForm(self, strs: List[str], m: int, n: int) -> int:
    dp = [[0 for k in range(n+1)] for j in range(m+1)]
    for i in range(len(strs)):
        zero = strs[i].count('0')
        one = strs[i].count('1')
        for j in range(m, zero-1, -1): # 注意这里的下界直接是 zero，这样就不用再判断一次
            for k in range(n, one-1, -1):
                dp[j][k] = max(dp[j][k], dp[j-zero][k-one] + 1)
    return dp[-1][-1]
```

#### 494. Target Sum
题意： 给定数组 nums，里面的数字可以加正号或符号，求出得到的和等于 S 的组合的个数

思路： 假设加正号的数的和为 s1，加负号的数的和为 s2
那么有： s1 + s2 = sum(nums), s1 - s2 = S
则 s1 = (sum(nums) + S) // 2
相当于是从 nums 中找到一些数，其和等于 s1，转变为了一个 01 背包问题

```python
def findTargetSumWays(self, nums: List[int], S: int) -> int:
    if (sum(nums) + S) % 2 != 0 or sum(nums) < S: # 注意这个条件！！！
        return 0
    v = (sum(nums) + S) // 2
    dp = [0 for _ in range(v+1)]
    dp[0] = 1
    for i in range(len(nums)):
        for j in range(v, nums[i]-1, -1): # 注意下界
            dp[j] = dp[j] + dp[j-nums[i]] # 放 nums[i] 的数 + 不放 nums[i] 的数
    return dp[-1]
```

#### 91. Decode Ways
思路： 理清楚几种情况，就能得到最终解。 由于可以解码的数是在 1-26 之间，因此用前后两位来判断。
num = int(s[i-2: i])
1. num == 10 or num == 20： 这个数只有一种解码方法，因此 dp[i] = dp[i-2]
2. 10 < num <=26, 即 num != 10, num != 20： 这个数有两种解码方法，因此 dp[i] = dp[i-1] + dp[i-2]
3. s[i-1] != '0', 只有一种解码方法，dp[i] = dp[i-1]

```python
def numDecodings(self, s):
    if not s or s[0] == '0':
        return 0
    dp = [0 for _ in range(len(s)+1)]
    dp[0] = dp[1] = 1
    for i in range(2, len(s)+1):
        num = int(s[i-2: i])
        if num == 10 or num == 20:
            dp[i] = dp[i-2]
        elif num > 10 and num <= 26:
            dp[i] = dp[i-2] + dp[i-1]
        elif s[i-1] != '0': # 可能有 101， 230 这种情况
            dp[i] = dp[i-1]
        else:
            return 0
    return dp[-1]
```

#### 279. Perfect Squares
```python
def numSquares(self, n: int) -> int:
    dp = [float('inf') for _ in range(n+1)]
    dp[0] = 0
    for i in range(1, n+1):
        for j in range(1, int(n**0.5)+1):
            dp[i] = min(dp[i], dp[i-j*j] + 1) 
    return dp[-1]
```

## 20190815
### 动态规划
#### 152. Maximum Product Subarray
思路： 用 dp[i] 记录以 nums[i] 结尾的子数组的最大积，由于可能出现负负得正的情况，最大积只可能在
nums[i], dp[i-1] * nums[i], min[i-1] * nums[i]; 需要记录下以 nums[i-1] 为结尾的子数组的最大积和最小积

```python
def maxProduct(self, nums: List[int]) -> int:
    dp_max = maxi = mini = nums[0]
    for i in range(1, len(nums)):
        lastmax = maxi # 注意这里一定要用一个变量记下 maxi，否则下面 maxi 变了之后，mini 无法得到正确结果
        maxi = max(nums[i], lastmax * nums[i], mini * nums[i])
        mini = min(nums[i], lastmax * nums[i], mini * nums[i])
        dp_max = max(dp_max, maxi)
    return dp_max
``` 

#### 300. Longest Increasing Subsequence
最长递增子序列，用 dp[i] 存储以 nums[i] 结尾的最长递增子序列的长度，比如 [10,9,2,5,3,7,101,18]
i = 3, nums[i] = 5 时，dp[3] = max(dp[0], dp[1], dp[2]+1)，只有 nums[2] < nums[3]

```python
def lengthOfLIS(self, nums: List[int]) -> int:
    if not nums:
        return 0
    dp = [0] * len(nums)
    for i in range(len(nums)):
        dp_i = 1
        for j in range(i): # 两层循环
            if nums[i] > nums[j]:
                dp_i = max(dp_i, dp[j] + 1) 
        dp[i] = dp_i
    return max(dp)
```

时间 O(nlogn) 的解法，用 dp[] 存储对应长度 LIS 的最小末尾，比如 [7,2,1,5,6,4,3,8,9]
初始 dp = [nums[0]] = 7
遍历 nums，发现 nums[i] 比 dp[-1] 更大的话就直接添加到 dp 的后面，相等就不管
若 nums[i] < dp[-1]，就要用 nums[i] 去替换 dp 中比 nums[i] 大的第一个数，可以用二分查找去找这个数

遍历一遍 dp 的值为：
[7]
[2]
[1]
[1, 5]
[1, 5, 6] # 比 dp[-1] 更大就直接追加
[1, 4, 6] # 用 4 替换掉 5，LIS 长度不会改变，dp 并不是 LIS，如果后面再出现 5,6，可以加进去，但如果不替换的话，后面再出现的数无法插入，因此长度为 2 的递增子序列的末尾的最小值是 4，也就是 [1, 4] 这个序列比 [1,5] 更优秀，后面还有 5 的话，可以继续加到 [1, 4] 中来
[1, 3, 6]
[1, 3, 6, 8]
[1, 3, 6, 8, 9]

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        if not nums:
            return 0
        dp = [nums[0]]
        for i in range(1, len(nums)):
            if nums[i] > dp[-1]:
                dp.append(nums[i])
            else:
                self.replace(dp, nums[i])
        return len(dp)
    
    def replace(self, dp, k): # 找到 dp 中第一个比 k 大的数，把它替换掉。
        left, right = 0, len(dp) - 1
        while left <= right:
            mid = left + (right-left) // 2
            if dp[mid] == k:
                return
            elif dp[mid] > k:
                right = mid - 1
            else:
                left = mid + 1
        dp[left] = k
```

#### 最长公共子序列 1143. Longest Common Subsequence
dp 设置为比 text1 和 text2 的长度多一行和多一列，全部初始化为 0，这样就不用去先额外初始化第一行和第一列
但要注意的是，比较字符是否相等时，应该是 if text1[i-1] == text2[j-1]，比填充 dp 的行列更小一位

```python
def longestCommonSubsequence(self, text1: str, text2: str) -> int:
    if not text1 or not text2:
        return 0 
    dp = [[0 for j in range(len(text2)+1)] for i in range(len(text1)+1)]
    for i in range(1, len(text1)+1):
        for j in range(1, len(text2)+1):
            if text1[i-1] == text2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i][j-1], dp[i-1][j])
    return dp[-1][-1]
```

最长公共子串：
```python
def longestCommonSubstring(self, text1: str, text2: str) -> int:
    if not text1 or not text2:
        return 0 
    dp = [[0 for j in range(len(text2)+1)] for i in range(len(text1)+1)]
    max_len = 0
    for i in range(1, len(text1)+1):
        for j in range(1, len(text2)+1):
            if text1[i-1] == text2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
                max_len = max(max_len, dp[i][j])
            else:
                dp[i][j] = 0
    return max(dp)
```

## 20190817
### 动态规划
#### 174. Dungeon Game
思路： 用 dp[i][j] 在进入到 (i,j) 这一格前，你至少要有 dp[i][j] 的能量才能不死，因为在第 (i,j) 格需要消耗的能量是 dungeon[i][j]，在每一格 dp[i][j] >= 1，才不会死亡。

当 dungeon[i][j] < 0 时，就要保证在这格消耗掉 dungeon[i][j] 能量后不死
当 dungeon[i][j] >= 0 时，因为只要 1 就能不死，拥有的能量加上这个房间的能量后能继续游戏。

从最后一格往前计算，比如最后一格需要消耗 -5 能量，那么进入最后一格之前最少要有 6 能量，才能保证在最后一格不死，从而通关，如果最后一格不需要消耗，那么 dp[i][j] = 1

先填充边界，最后一行和最后一列。 
在最后一行 i=-1，只能往右走，dp[i][j] = max(1, dp[i][j+1] - dungeon[i][j])
在最后一列 j=-1，只能往下走，dp[i][j] = max(1, dp[i+1][j] - dungeon[i][j])
在其他位置，可以往下或者往右，dp[i][j] 就是上面两个值中较小的一个。

```python
def calculateMinimumHP(self, dungeon):
    n = len(dungeon)
    m = len(dungeon[0])
    dp = [[0 for _ in range(m)] for _ in range(n)]
    dp[-1][-1] = max(1, 1-dungeon[-1][-1])
    for i in range(n-2, -1, -1):
        dp[i][-1] = max(1, dp[i+1][-1] - dungeon[i][-1])
    for j in range(m-2, -1, -1):
        dp[-1][j] = max(1, dp[-1][j+1] - dungeon[-1][j])
        
    for i in range(n-2, -1, -1):
        for j in range(m-2, -1, -1):
            down = max(1, dp[i+1][j] - dungeon[i][j])
            right = max(1, dp[i][j+1] - dungeon[i][j])
            dp[i][j] = min(down, right)
    return dp[0][0]
```
#### 221. Maximal Square
思路： 用 dp[i][j] 存储以 matrix[i][j] 为右下角的正方形的最大边长，那么边长只与在 (i,j) 周围的三个点有关， dp[i][j] = min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1]) + 1
 
```python
def maximalSquare(self, matrix: List[List[str]]) -> int:
    if not matrix:
        return 0
    n, m = len(matrix), len(matrix[0])
    dp = [[int(matrix[i][j]) for j in range(m)] for i in range(n)]
    max_len = 0
    for i in range(n):
        max_len = max(max_len, dp[i][0])
    for j in range(m):
        max_len = max(max_len, dp[0][j])
    for i in range(1, len(matrix)):
        for j in range(1, len(matrix[0])):
            if matrix[i][j] == '1':
                dp[i][j] = min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1]) + 1
                max_len = max(dp[i][j], max_len)
    return max_len ** 2
```

#### 123. Best Time to Buy and Sell Stock III
思路： 如果把数组分成两个部分，再分别计算只能买卖一次的最大值，会超时

考虑用空间换时间，用两个数组来存储前后两个部分的买卖一次的最大值
max_profit1[i] 存储前 i 天的最大值，从前往后计算
max_profit2[i] 存储第 i 天之后的那部分的最大值（包括第 i 天），要从后往前计算，且记录的是 max_p
包括第 i 天是因为在这天可以先卖出再买入。

```python
def maxProfit(prices):
    if len(prices) <= 1:
        return 0
    max_profit1 =  [0 for _ in range(len(prices))]
    max_profit2 = [0 for _ in range(len(prices))] # 注意列表千万不可以两个一起赋值，是引用

    min_p = prices[0]
    for i in range(1, len(prices)):
        max_profit1[i] = max(max_profit1[i - 1], prices[i] - min_p)
        min_p = min(min_p, prices[i])

    max_p = prices[-1]
    for i in range(len(prices) - 2, -1, -1): 
        max_profit2[i] = max(max_profit2[i + 1], max_p - prices[i])
        max_p = max(max_p, prices[i])

    res = 0
    for i in range(len(prices)):
        res = max(res, max_profit1[i] + max_profit2[i])
    return res
```

### 栈和队列
#### 20. Valid Parentheses
思路： 用栈来存储左括号，当遇到右括号时，从栈中弹出一个左括号（此时栈中必须有元素），并判断是否是相应的括号对（这里的括号对可以用 dict 存储，减少判断）
最后栈为空就返回 True

```python
def isValid(self, s: str) -> bool:
    stack = []
    dict = {'(' : ')', '{' : '}', '[' : ']'} 
    for char in s:
        if char in dict:
            stack.append(char)
        else:  
            if not stack or dict[stack.pop()] != char:
                return False
    return True if not stack else False
```

#### 3. Longest Substring Without Repeating Characters
思路： 用 dict 存储字符及该字符上一次出现的位置。
如果出现了重复字符，并且上一次出现这个字符在上一个不重复子串之中，那就从重复字符的下一个字符位置开始算
如果没有出现重复字符，或者出现重复字符，但计算的起始位置比上一次出现重复字符的位置更大，就计算长度，并保留最大的长度

```python
def lengthOfLongestSubstring(self, s):
    dict = {}
    max_len, start = 0, 0
    for i in range(len(s)):
        if s[i] not in dict or start > dict[s[i]]:
            max_len = max(max_len, i-start+1)
        else:
            start = dict[s[i]] + 1
        dict[s[i]] = i
    return max_len
```

#### 205. Isomorphic Strings
同构字符串
思路： 用 dict 存储对应位置的字符对，当 s 遍历到的字符 s[i] 在 dict 的 key 中时，要保证 t[i] 和 dict 中存的值一样；当 s[i] 不在 dict 的 key 中时，要保证 t[i] 不在 dict 的所有值中（比如 ab aa 的情况） 

```python
def isIsomorphic(self, s: str, t: str) -> bool:
    if len(s) != len(t):
        return False
    dict = {}
    for i in range(len(s)):
        if s[i] not in dict:
            if t[i] in dict.values(): # 注意这一步，容易忽略
                return False
            dict[s[i]] = t[i]
        else:
            if dict[s[i]] != t[i]:
                return False
    return True
```

#### 594. Longest Harmonious Subsequence
最长和谐子序列： 子序列中最大值和最小值只相差 1
在 LHS 中，只会有两个数存在，我们可以先对每一个数计数，然后再判断这个数 +1 是否在序列中，如果再就计算两个数总共出现次数

```python
def findLHS(self, nums: List[int]) -> int:
    import collections
    cnt = collections.Counter(nums)
    max_len = 0
    for num in cnt:
        if num+1 in cnt:
            max_len = max(max_len, cnt[num] + cnt[num+1])
    return max_len
```

## 20190818
### 二叉树
#### 111. Minimum Depth of Binary Tree
只有四种情况： 空，返回 0；没有左子树，返回右子树高度；没有右子树，返回左子树高度；都有，返回左右子树中高度更小的

```python
def minDepth(self, root: TreeNode) -> int:
    if not root:
        return 0
    if not root.left:
        return self.minDepth(root.right) + 1
    elif not root.right:
        return self.minDepth(root.left) + 1
    else:
        return min(self.minDepth(root.left), self.minDepth(root.right)) + 1
```

#### 112. Path Sum
```python
def hasPathSum(self, root: TreeNode, sum: int) -> bool:
    if not root:
        return False
    sum -= root.val
    if not root.left and not root.right and sum == 0:
        return True
    return self.hasPathSum(root.left, sum) or self.hasPathSum(root.right, sum)
```

#### 113. Path Sum II
```python
def pathSum(self, root: TreeNode, sum: int) -> List[List[int]]:
    if not root:
        return []
    def dfs(root, sum, arr):
        sum -= root.val
        if not root.left and not root.right and sum == 0:
            res.append(arr+[root.val])113. Path Sum II
        if root.left:
            dfs(root.left, sum, arr+[root.val])
        if root.right:
            dfs(root.right, sum, arr+[root.val])
    res = []
    dfs(root, sum, [])
    return res
```

#### 117. Populating Next Right Pointers in Each Node II
思路一： 递归解法，分情况讨论
1. 有左子树和右子树，root.left.next = root.right; 而 root.right.next 的下一个要根据 root.next 是否有左右孩子还决定
2. 只有左子树，root.left.next 根据 root.next 的左右孩子决定
3. 只有右子树，root.right.next 根据 root.next 的左右孩子决定
4. 都没有，不管

对于 root.next：
1. 没有 root.next， 返回 None
2. 有左孩子，返回左孩子
3. 没有左孩子，有右孩子，返回右孩子
4. 都没有，再去找 root.next.next 是否有左右孩子

```python
def connect(self, root):
    if not root:
        return root
    if root.left and root.right:
        root.left.next = root.right
        root.right.next = self.helper(root.next)
    elif root.left and not root.right:       
        root.left.next = self.helper(root.next)
    elif not root.left and root.right:
        root.right.next = self.helper(root.next)
        
    self.connect(root.right)
    self.connect(root.left)
    return root

def helper(self, node):
    if not node:
        return None
    if node.left:
        return node.left
    elif node.right:
        return node.right
    else:
        return self.helper(node.next)
```

思路二：层次遍历
```python
def connect(self, root):
    if not root:
        return root
    nodes = [root]
    while nodes:
        tmp = []
        for i in range(1, len(nodes)):
            nodes[i-1].next = nodes[i]
        for node in nodes:
            if node.left:
                tmp.append(node.left)
            if node.right:
                tmp.append(node.right)
        nodes = tmp
    return root
```

思路三： 层次遍历，但是不把每层的节点都记录到临时数组中，这样空间复杂度就是 O(n) , n 是节点最多的那层的数量。 可以把每层当做一个链表，只要记录链表的表头即可，这样就只用了 O(1) 的空间

用 dummy 指向一下层的第一个节点，然后遍历当前层的每一个元素，根据是否有左右孩子就可以去连接下一层元素
```python
def connect(self, root):
    if not root:
        return 
    cur = root # 当前层
    while cur:
        dummy = ListNode(0) # 指向下一层的第一个节点
        p = dummy
        tmp = cur 
        while tmp: # 遍历当前层，连接成链表
            if tmp.left:
                p.next = tmp.left
                p = p.next
            if tmp.right:
                p.next = tmp.right
                p = p.next
            tmp = tmp.next
        cur = dummy.next 
    return root
```

#### 617. Merge Two Binary Trees
```python
def mergeTrees(self, t1: TreeNode, t2: TreeNode) -> TreeNode:
    if not t1 and not t2:
        return None
    if not t1:
        return t2
    if not t2:
        return t1
    root = TreeNode(t1.val + t2.val)
    root.left = self.mergeTrees(t1.left, t2.left)
    root.right = self.mergeTrees(t1.right, t2.right)
    return root
```

#### 96. Unique Binary Search Trees
用 dp[n] 存储 1-n 个数字组成的不同的 BST 的数量，用 F(i, n) 表示以 i 为根节点，1-n 个数字组成的 BST 数量， 那么 dp[n] = F(1, n) + F(2, n) + ... + F(i, n) + ... + F(n, n)

以 i 为根节点， 1-n 个数字组成的 BST，左边有 i-1 个元素，右边有 n-i 个元素，那么 F(i, n) = dp[i-1] * dp[n-i]

则: dp[n] = dp[0] * dp[n-1] + dp[1] * dp[n-2] + ... + dp[n-1] * dp[0]
用两层循环来计算即可。

```python
def numTrees(self, n: int) -> int:
    if n == 0:
        return 0
    dp = [0 for i in range(n+1)]
    dp[0] = dp[1] = 1
    for i in range(2, n+1):
        for j in range(i):
            dp[i] += dp[j] * dp[i-j-1]
    return dp[n]
```

#### 95. Unique Binary Search Trees II
用 1-n 构建 BST，求出所有不同的 BST
思路： 以 i 为根节点的 BST，[1, i-1] 构成他的左子树，[i+1, n] 构成他的右子树
可以递归的去构造出左子树和右子树的数组，里面存的是每个左子树、右子树的根节点，然后遍历两个数组，组成不同的 BST

```python
class Solution:
    def generateTrees(self, n: int) -> List[TreeNode]:
        if n == 0:
            return []
        return self.helper(1, n) # 递归开始数值
    
    def helper(self, begin, end):
        if begin > end: # 注意这里终止递归的条件
            return [None]
        res = []
        for i in range(begin, end+1):
            left = self.helper(begin, i-1) # 得到一个以 [begin, i-1] 这些数字构成的所有的子树的根节点集合
            right = self.helper(i+1, end)
            for l in left:
                for r in right:
                    root = TreeNode(i)
                    root.left = l # l 是左子树的根节点
                    root.right = r
                    res.append(root)
        return res
```

#### 109. Convert Sorted List to Binary Search Tree
题意： 将有序链表转化为 BST

思路一： 将链表转化为数组，再按照数组转化成 BST 的方法构建，空间 O(n)

思路二： 用快慢指针法找到链表的中间，也就是 root，将链表分成左右两个部分，构建成 root 的左子树和右子树，空间 O(1)。 但是这种方法的缺点是会修改原有链表。
```python
def sortedListToBST(self, head: ListNode) -> TreeNode:
    if not head:
        return None
    if not head.next:
        return TreeNode(head.val) # 注意
    fast = head.next # 注意 fast 的初始值
    slow = head
    while fast.next and fast.next.next:
        fast = fast.next.next
        slow = slow.next
        
    r = slow.next
    slow.next = None
    root = TreeNode(r.val)
    root.left = self.sortedListToBST(head)
    root.right = self.sortedListToBST(r.next)
    return root
```

思路三： 如果要求不能修改原来的链表，且要空间 O(1)，则可以设置一个 end 位置，fast 到 end 就停止遍历，这样就得到了左右子树所在区间。
```python
class Solution:
    def sortedListToBST(self, head: ListNode) -> TreeNode:
        return self.helper(head, None)
        
    def helper(self, head, end):
        if head == end:
            return None
        fast = slow = head
        while fast != end and fast.next != end:
            fast = fast.next.next
            slow = slow.next
        root = TreeNode(slow.val)
        root.left = self.helper(head, slow)
        root.right = self.helper(slow.next, end)
        return root
```

#### 236. Lowest Common Ancestor of a Binary Tree
```python
def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
    if not root or root == p or root == q:
        return root
    left = self.lowestCommonAncestor(root.left, p, q)
    right = self.lowestCommonAncestor(root.right, p, q)
    if left and right:
        return root
    if left:
        return left
    return right
```

#### 222. Count Complete Tree Nodes
对于完全二叉树： 除了最后一行外，其余行的节点都是满的，且最后一行的节点是靠左边排列的，因此左子树高度 >= 右子树高度。 对于一棵满二叉树，节点数为 `2**h - 1`，因此可以根据左右子树的高度来计算完全二叉树的节点数。

1. 左子树高度 == 右子树高度，左子树肯定是满二叉树
2. 左子树高度 > 右子树高度，右子树肯定是满二叉树

```python
class Solution:
    def countNodes(self, root: TreeNode) -> int:
        if not root:
            return 0
        l = self.get_height(root.left)
        r = self.get_height(root.right)
        if l == r:
            return 1 + 2**l-1 + self.countNodes(root.right) # 记得 + 1，是 root 节点
        else:
            return 1 + 2**r-1 + self.countNodes(root.left)
         
    def get_height(self, root): # 计算高度只要计算最左边的即可
        height = 0
        while root:
            height += 1
            root = root.left
        return height
```

#### 114. Flatten Binary Tree to Linked List
题意： 将二叉树变平成为一个链表

变成链表后的顺序相当于是二叉树的前序遍历重新组织，因此先获得前序遍历的结果，再重新组织二叉树，每个节点的 left 都为空
```python
class Solution:
    def flatten(self, root: TreeNode) -> None:
        """
        Do not return anything, modify root in-place instead.
        """
        pre = []
        def preOrder(root):
            if not root:
                return None
            pre.append(root)
            preOrder(root.left)
            preOrder(root.right)
        preOrder(root)
        
        for i in range(1, len(pre)):
            root.left = None
            root.right = pre[i]
            root = root.right
```

### 数组
#### 80. Remove Duplicates from Sorted Array II
题意： 删除重复数字，重复数字最多可以出现两次

思路： 对每个数字计数，当 cnt == 1 或 cnt == 2 时，说明数字会在结果集中，用一个指针 j 指向结果集的数字，直接覆盖 nums[j] = nums[i]

```python
def removeDuplicates(self, nums: List[int]) -> int:
    if len(nums) <= 2:
        return len(nums)
    cnt = 1
    j = 1
    for i in range(1, len(nums)):
        if nums[i] == nums[i-1]:
            cnt += 1
        else:
            cnt = 1
        if cnt == 1 or cnt == 2:
            nums[j] = nums[i]
            j += 1
    return j
```

#### 31. Next Permutation
思路：
1. 从后往前遍历，找到第一组相邻的升序序列，记 nums[i] （如果找不到就直接对 nums 排序，也就是输出最小的数）
2. 从后往前遍历，找到第一个比 nums[i] 更大的数，交换两个数
3. 对于 nums[i+1:] 的数，进行升序排序

```python
def nextPermutation(self, nums: List[int]) -> None:
    """
    Do not return anything, modify nums in-place instead.
    """
    if len(nums) <= 1:
        return 
    flag = 0
    for i in range(len(nums)-2, -1, -1):
        if nums[i] < nums[i+1]:
            flag = 1
            for j in range(len(nums)-1, i, -1):
                if nums[j] > nums[i]:
                    nums[i], nums[j] = nums[j], nums[i]
                    nums[i+1:] = sorted(nums[i+1:]) # 这里一定不能用 .sort()，因为切片就生成了新的列表，必须赋值才能排序
                    break
            break # 注意着两层 break
    if not flag:
        nums.sort()
```

## 20190819
### 数组
#### 229. Majority Element II
摩尔投票法： 有两个计数器和两个候选数字

```python
def majorityElement(self, nums: List[int]) -> List[int]:
    if len(nums) <= 1:
        return nums
    cnt1, cnt2 = 0, 0
    major1, major2 = None, None # 注意 cnt 和 major 的初始化
    for i in range(len(nums)):
        if nums[i] == major1:
            cnt1 += 1
        elif nums[i] == major2:
            cnt2 += 1
        elif cnt1 == 0: # 注意一次只进行一步判断
            cnt1 = 1
            major1 = nums[i]
        elif cnt2 == 0:
            cnt2 = 1
            major2 = nums[i]
        else:
            cnt1 -= 1
            cnt2 -= 1
    return [m for m in [major1, major2] if nums.count(m) > len(nums)/3]             
```

### 矩阵
#### 73. Set Matrix Zeroes
思路： 要想空间复杂度为 O(1) ，可以把要置 0 的行列储存在第一行和第一列，这样的话会改变第一行和第一列的值，只需要额外用一个遍历记录下第一行或第一列是否要置 0 即可。

第 0 列一定要单独判断，因为如果直接判断的话，当发现第 0 列有 0 时，就会把 matrix[0][0] 置 0 ，但如果第0 行没有 0 的话，最后去置 0 的时候就会把第 0 行全部置为 0，这样就错了。 比如 [[1,1,1],[0,1,2]] 的情况。

```python
def setZeroes(self, matrix: List[List[int]]) -> None:
    """
    Do not return anything, modify matrix in-place instead.
    """
    n, m = len(matrix), len(matrix[0])
    flag = 0
    for i in range(n):
        if matrix[i][0] == 0:
            flag = 1
        for j in range(1, m):
            if matrix[i][j] == 0:
                matrix[i][0] = 0
                matrix[0][j] = 0
    
    for i in range(n-1, -1, -1):
        for j in range(m-1, 0, -1):
            if matrix[i][0] == 0 or matrix[0][j] == 0:
                matrix[i][j] = 0
        if flag:
            matrix[i][0] = 0
```

378. Kth Smallest Element in a Sorted Matrix

### 链表
#### 2. Add Two Numbers
直接遍历链表，对相应位置的值进行相加，如果超过 10 就要进位，用一个数记录下进位

```python
def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
    dummy = ListNode(0)
    cur = dummy
    n = 0
    while l1 or l2 or n: # 这里还要 or n 是因为，如果到末尾还要进位，l1 和 l2 都是 None 了，还要新创建一个值为 n 的节点。
        if l1:
            n += l1.val
            l1 = l1.next
        if l2:
            n += l2.val
            l2 = l2.next
        carry = n % 10
        n = n // 10
        cur.next = ListNode(carry)
        cur = cur.next
    return dummy.next
```

#### 82. Remove Duplicates from Sorted List II
删除链表中的重复节点，不保留，只有当 cur.val != cur.next.val 时，原有结构保持不变，继续往下面遍历。
只要发生了上面的情况，就过滤掉全部的重复节点，此时 pre.next = cur.next，但不要改变 pre 的指向，因为下一个可能还是重复节点！！！

```python
def deleteDuplicates(self, head: ListNode) -> ListNode:
    if not head or not head.next:
        return head
    dummy = ListNode(0)
    dummy.next = head
    pre = dummy
    cur = head
    while cur and cur.next: # 这里一定要加 cur.next 这个条件，不然会死循环
        if cur.val != cur.next.val:
            pre = cur
            cur = cur.next
        else:
            while cur.next and cur.val == cur.next.val:
                cur = cur.next
            pre.next = cur.next
            cur = cur.next
    return dummy.next
```

#### 92. Reverse Linked List II
题意： 反转链表的 m 到 n 部分

思路： 将链表分成三个部分
第一部分 phead1 = head， 找到 pend1
第二部分，反转的部分，找到 rhead 和 rend
第三部分，phead2

那么重新将三个部分连接起来： pend1.next = rhead; rend.next = phead2
要注意的是当 m == 1 时没有第一部分，一定要单独拿出来讨论！！！
```python

class Solution:
    def reverseBetween(self, head: ListNode, m: int, n: int) -> ListNode:
        if not head or not head.next or m == n:
            return head
        
        cur = head
        for _ in range(m-2):
            cur = cur.next
        rend = cur.next if m != 1 else head # 反转部分的 end
        pend1 = cur # 第一部分的 end
        
        pre = None
        cur = rend
        for _ in range(n-m+1):
            tmp = cur.next
            cur.next = pre
            pre = cur
            cur = tmp
        
        rhead = pre # 反转部分的 head
        phead2 = cur # 最后一部分的 head
        if m != 1:
            pend1.next = rhead
        rend.next = phead2
        return head if m!=1 else rhead
```

### 双指针
#### 15. 3Sum
题意： 找出 nums 中 a+b+c = 0 的三个数，所有的组合

思路：由于 nums 中有重复，可以先对 nums 排序，这样重复数字就在相邻位置，重复数字只需要记录一次
1. 先固定一个数 a，然后用双指针 left 和 right 指向剩下的数组成的数组的头和尾
2. 由于是排序的数，只要根据三个数的和与 0 的大小比较，就可以判断 left 和 right 哪个要移动。
3. 若三个数的和 = 0，那么就找到了这三个数，但是由于可能有重复数字，为加快效率，就让 left 指向重复数字最右边的一个，right 指向重复数字最左边的一个。
```python
def threeSum(self, nums: List[int]) -> List[List[int]]:
    res = []
    n = len(nums)
    nums.sort()
    for i in range(n-2):
        if i > 0 and nums[i] == nums[i-1]:
            continue
        left = i + 1
        right = n - 1
        while left < right:
            sum = nums[i] + nums[left] + nums[right]
            if sum < 0:
                left += 1
            elif sum > 0:
                right -= 1
            else:
                res.append([nums[i], nums[left], nums[right]])
                while left < right and nums[left] == nums[left+1]:
                    left += 1
                while left < right and nums[right] == nums[right-1]:
                    right -=1
                left += 1
                right -= 1
    return res
```

#### 16. 3Sum Closest
```python
def threeSumClosest(self, nums: List[int], target: int) -> int:
    n = len(nums)
    res = float('inf')
    nums.sort()
    for i in range(n-2):
        if i > 0 and nums[i] == nums[i-1]:
            continue
        left, right = i+1, n-1
        while left < right:
            s = nums[i] + nums[left] + nums[right]
            if s == target:
                return s
            elif s < target:
                left += 1
            else:
                right -= 1
            if abs(target-s) < abs(target-res): # 条件变了
                res = s
    return res
```

#### 75. Sort Colors
题意： nums 中只有三种数字 0,1,2 ，对 nums 进行排序，要求不使用库函数，直接原地操作

思路： 由于 0 会排在前面，2 排在后面，中间全是 1，因此可以用两个指针 p0 指向 0 放的位置，p2 指向 2 放的位置。
遍历一遍数组，注意从 0 开始，到 p2 结束（不能用 for，因为 for 循环每次都得向前一步）
1. nums[i] == 0，就将其和 p0 指向的值交换，并将 i+1， p0+1
2. nums[i] == 2，就将其和 p2 指向的值交换，并将 p2+1，这里不将 i+1 是因为换过来的 nums[i] 可能是 0 也可能是 1，无法判断情况，所以留到下一轮再判断一次
3. nums[i] == 1，跳过，即 i+1，但 p0 和 p2 指向都不变，这样后面遇到 0,2 时就交换结果，能够保证所有的 1 都在中间
```python
def sortColors(self, nums: List[int]) -> None:
    """
    Do not return anything, modify nums in-place instead.
    """
    p0, p2 = 0, len(nums)-1
    i = 0
    while i <= p2:
        if nums[i] == 0:
            nums[i], nums[p0] = nums[p0], nums[i]
            p0 += 1
            i += 1
        elif nums[i] == 2:
            nums[i], nums[p2] = nums[p2], nums[i]
            p2 -= 1
        else:
            i += 1
```

#### 209. Minimum Size Subarray Sum
思路： 相当于是一个长度可变的滑动窗口，当窗口中的和比 s 更小时，就往右边添加元素；当窗口中的和 >= s 时，就删除左边的元素，并记录下满足条件的长度最小的窗口。

```python
def minSubArrayLen(self, s: int, nums: List[int]) -> int:
    length = float('inf')
    sum_array = 0
    left, right = 0, 0
    n = len(nums)
    while right < n:
        while right < n and sum_array < s:
            sum_array += nums[right]
            right += 1
        while sum_array >= s:
            length = min(length, right-left) # 注意这里窗口的长度是 right-left，因为 right 已经到了满足条件的窗口之外
            sum_array -= nums[left]
            left += 1
    return length if length != float('inf') else 0
```

## 20190820
### 位运算
#### 29. Divide Two Integers
题意： 不用乘法、除法、取模运算做两数相除
```python
def divide(self, dividend: int, divisor: int) -> int:
    if dividend == 0:
        return 0
    flag = 1
    if (dividend < 0 and divisor > 0) or (dividend > 0 and divisor < 0):
        flag = -1
    dividend, divisor = abs(dividend), abs(divisor)
    quotient = 0
    while dividend >= divisor:
        tmp = divisor # 注意在里面初始化即可
        i = 1
        while dividend >= tmp: # 一直在内层循环计算
            dividend -= tmp
            quotient += i
            tmp <<= 1
            i <<= 1                
    res = quotient * flag
    if res > 2**31 - 1:
        return 2**31 -1 
    if res < -2**31:
        return -2**31 
    return res
```

#### 89. Gray Code
格雷码： 任意两个相邻的数的二进制只有一位是不同的，其余的位都相同
方法： 从 0 到 `2**n -1` 的每一个数都与其右移一位的数进行异或操作

```python
def grayCode(self, n: int) -> List[int]:
    res = []
    for i in range(2**n):
        gray_code = i ^ (i >> 1)
        res.append(gray_code)
    return res
```

#### 137. Single Number II
```python
def singleNumber(self, nums: List[int]) -> int:
    res = 0
    for i in range(32):
        s = 0
        for j in range(len(nums)):
            if (nums[j] >> i) & 1:
                s += 1
        n = s % 3
        if n == 1:
            res += n * (2**i)
    if res >= 2 ** 31:
        res -= 2 ** 32
    return res
```

#### 201. Bitwise AND of Numbers Range
思路： 列举几个数出来，会发现 [m, n] 中所有数的按位与结果会等于 m 和 n 左边的公共部分，后面全部都是 0，因为这个区间里的数有 0 也有 1

```python
def rangeBitwiseAnd(self, m: int, n: int) -> int:
    cnt = 0
    while m != n:
        m >>= 1
        n >>= 1
        cnt += 1
    return m << cnt
```

### 数学
#### 12. Integer and Roman
根据 1994 的罗马数字是 "MCMXCIV" 可以知道，是从高到低，每一位的罗马数字的组合
1000: M , 900: CM, 90: XC, 4: IV
因此我们可以枚举出每一位的 0-9 的组成，再根据数字中每一位是几得到该位的罗马数字。

```python
def intToRoman(self, num: int) -> str:
    I = ['', 'I', 'II', 'III', 'IV', 'V', 'VI', 'VII', 'VIII', 'IX']
    X = ['', 'X', 'XX', 'XXX', 'XL', 'L', 'LX', 'LXX', 'LXXX', 'XC']
    C = ['', 'C', 'CC', 'CCC', 'CD', 'D', 'DC', 'DCC', 'DCCC', 'CM']
    M = ['', 'M', 'MM', 'MMM']
    return M[num//1000] + C[num//100%10] + X[num//10%10] + I[num%10] 
```

#### 13. Roman to Integer
按照罗马数字的组成，前面的字母值一般会大于后面的字母值，但如果出现了 IV, IX 这种特殊情况，前一个字母值小于后一个字母值的话，就要减掉两倍的前一个字母值。

```python
def romanToInt(self, s: str) -> int:
    dic = {'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}
    res = 0
    for i in range(len(s)):
        res += dic[s[i]]
        if i > 0 and dic[s[i]] > dic[s[i-1]]:
            res -= 2 * dic[s[i-1]]
    return res
```

#### 168. Excel Sheet Column Title
十进制转 26 进制，注意起始位 1：A
```python
def convertToTitle(self, n: int) -> str:
    res = ""
    while n:
        res = chr((n-1)%26 + 65) + res
        n = (n-1) // 26
    return res
```

#### 171. Excel Sheet Column Number
26 进制转十进制，比上一题更简单
```python
def titleToNumber(self, s: str) -> int:
    res = 0
    for char in s:
        res = res * 26 + ord(char) - 64
    return res
```

#### 204. Count Primes
题意： 计算小于 n 的素数的个数
思路： 用厄拉多塞筛法，先删掉 2 的倍数，再删掉 3 的倍数...
首先初始化一个数组 primes 全部为 1 ，代表数字 i 是素数，由于 0 和 1 不是素数,primes[0]=primes[1]=0
删除数字从 i=2 开始，然后把 i 的倍数的 primes[i] 置 0，最后的素数的个数就是 primes 数组中 1 的个数
```python
def countPrimes(self, n: int) -> int:
    if n <= 2:
        return 0
    primes = [1] * n
    primes[0] = primes[1] = 0
    for i in range(2, int(n**0.5)+1): # 只需要遍历到 n**0.5 即可，后面的数要么是素数，要么是前面数的倍数
        if primes[i]:
            for j in range(i*i, n, i):
                primes[j] = 0
    return primes.count(1)
```
如果要找出所有的素数，就 `return [i for i in range(len(primes)) if primes[i] == 1]`

#### 223. Rectangle Area 
```python
def computeArea(self, A: int, B: int, C: int, D: int, E: int, F: int, G: int, H: int) -> int:
    s = (D - B) * (C - A) + (H - F) * (G - E)        
    length = max(0, min(C, G) - max(A, E))
    height = max(0, min(H, D) - max(B, F))
    return s - length * height
```

### 贪心
#### 134. Gas Station
只要 sum(gas) >= sum(cost) 就一定有解

从 i = 0 开始遍历一遍，当前的汽油量 < 0 时，就重置起点，从 i+1 位置开始走，并重置汽油量为 0
```python
def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
    if sum(gas) < sum(cost):
        return -1
    total = 0
    start = 0
    for i in range(len(gas)):
        total = total + gas[i] - cost[i]
        if total < 0:
            total = 0
            start = i + 1
    return start
```

#### 665. Non-decreasing Array
题意： 修改 nums 中的一个数字，使 nums 变为非减数组

思路： 计数 nums 中逆序对的个数，但逆序对 >= 2 时，修改一个数字不能成功，返回 False
找到逆序对后，需要修改 nums[i] 或 nums[i+1] 的值，但具体修改哪一个需要比较， nums[i-1] 和 nums[i+1] 的大小

```python
def checkPossibility(self, nums: List[int]) -> bool:
    cnt = 0
    for i in range(len(nums)-1):
        if nums[i] > nums[i+1]:
            cnt += 1
            if i-1 >= 0 and nums[i+1] <= nums[i-1]:
                nums[i+1] = nums[i]
            nums[i] = nums[i+1]
        if cnt == 2:
            return False
    return True
```

#### 763. Partition Labels 
思路： 对一个字符，先找到它最后出现的位置，用 str.rfind 方法； 遍历字符串，如果最后出现的位置就等于当前遍历的位置，那么就找到了一个符合条件的字符串，加到结果集中，start 和 end 就重置。
```python
def partitionLabels(self, S: str) -> List[int]:
    if not S:
        return []
    res = []
    start = 0
    end = S.rfind(S[0])
    for i in range(len(S)):
        i_end = S.rfind(S[i])
        end = max(end, i_end)
        if i == end:
            res.append(end-start+1)
            start = i + 1
            end = i + 1
    return res
```

## 20190821
### 剑指 offer
#### 字符流中第一个不重复的字符
请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从字符流中只读出前两个字符"go"时，第一个只出现一次的字符是"g"。当从该字符流中读出前六个字符“google"时，第一个只出现一次的字符是"l"。

在 python2 中字典是无序的，python3 中的字典是按照存储顺序排的

```python
# -*- coding:utf-8 -*-
class Solution:
    # 返回对应char
    def __init__(self):
        self.s = ""
        self.dict = {}
    def FirstAppearingOnce(self):
        # write code here
        for key in self.s: # 不要去遍历 self.dict，因为可能是无序的
            if self.dict[key] == 1:
                return key
        return '#'
    def Insert(self, char):
        # write code here
        self.s += char
        if char not in self.dict:
            self.dict[char] = 1
        else:
            self.dict[char] += 1 
```

#### 丑数
把只包含质因子2、3和5的数称作丑数（Ugly Number）。例如6、8都是丑数，但14不是，因为它包含质因子7。 习惯上我们把1当做是第一个丑数。求按从小到大的顺序的第N个丑数。

思路： 丑数只可能由之前的丑数 * 2， * 3 或 * 5 得到，且下一个最小的丑数，只能在（某个数 * 2， 某个数 * 3， 某个数 * 5）中产生。 用一个数组记下前 N 个丑数，用 i2 记录第一个 * 2 会大于当前最大丑数的那个数的坐标，i3 i5 亦如此，因此下一个丑数必在这三个数中产生。

```python
def GetUglyNumber_Solution(self, index):
    # write code here
    if index == 0:
        return 0
    ugly_nums = [1]
    i2 = i3 = i5 = 0
    while index>1:
        minnum = min(ugly_nums[i2]*2, ugly_nums[i3]*3, ugly_nums[i5]*5) 
        ugly_nums.append(minnum) # minnum 是当前 ugly_nums 数组中最大的丑数
        while ugly_nums[i2] * 2 <= minnum: # 找到第一个 * 2 会大于 minnum 的那个数的坐标，下次判断下一个丑数时就只要在这三个数中选择最小的那个。
            i2 += 1
        while ugly_nums[i3] * 3 <= minnum:
            i3 += 1
        while ugly_nums[i5] * 5 <= minnum:
            i5 += 1
        index -= 1
    return ugly_nums[-1]
```

#### 圆圈中最后剩下的数
0，1，...，n-1这n个数字排成一个圆圈，从数字0开始每次从这个圆圈里删除第m个数字。求出这个圆圈里剩下的最后一个数字。

约瑟夫环问题，需要找到删除数字的规律。

思路一： 用数组代替环形链表，循环遍历下去，删除特定的数字，直到数组长度为 1 。空间复杂度为 O(n)，每删除一个数字需要 m 步，共有 n 个数字，因此时间复杂度为 O(mn)， 空间复杂度 O(n)

```python
def LastRemaining_Solution(self, n, m):
    if n < 1 or m < 1: # 特殊情况 n=0 m=0 时，要看了用例才知道
        return -1
    m = m - 1 # 第 m 个数字的下标为 m-1
    nums = [i for i in range(n)]
    i = 0
    while len(nums) > 1:
        i += m
        if i >= len(nums):
            i = i % len(nums)
        nums.pop(i)
    return nums[0]
```

思路二： 用数学的方法来解。
f(n, m) = 0, 当 n = 1 时
f(n, m) = [f(n-1, m) + m] % n, 当 n > 1 时

f(n, m) 表示每次在 n 个数字 [0, 1, 2, ..., n-2, n-1] 中删除第 m 个数字，最后剩下的那个数字。

1. 首先我们可以知道第一个被删除的数字下标为 (m-1)%n, 记 k = (m-1)%n，那么删除 k 之后，剩下的序列为 [0, 1, ..., k-1, k+1, ..., n-2, n-1]，共有 n-1 个数字

2. 下一次删除是从 k+1 这个数开始计数的，那么我们重排序列，把 k+1 这个数排在前头，得到新序列为 [k+1,...n-2, n-1, 0, 1, ..., k-1]，这个序列最后剩下的数也应该是关于 n 和 m 的函数，但与 f(n, m) 不同的是开头的数字变为了 k+1，所以我们把这个新序列每次删除第 m 个数字后剩下的那个数记为 f'(n-1, m),两个数字应该是相同的，即 f(n, m) = f'(n-1, m)

3. 将剩下的 n-1 个序列进行一个映射，把它变为之前序列一样的形式即 [0, 1, 2, ..., n-2]，映射规则为：
[k+1,...n-2, n-1, 0, 1, ..., k-1] ->[0, ..., n-2]
```
k+1 -> 0
k+2 -> 1
...
n-1 -> n-k-2
0 -> n-k-1
1 -> n-k
...
k-1 -> n-2
```
那么原来的数 x 就变为了 x-k-1, p(x) = x-k-1，原来的数 = 新的数+k+1，但要注意这样得到的数字可能会超过 n-1，因此最后还要对 n 取模，因此有 原来的数 = (新的数+k+1) % n，得到逆映射 p(x) 的反函数为 g(x) = (x+k+1)%n

4. 映射之后的序列 [0, ..., n-2] 最后剩下的数为 f(n-1, m) 和最初的序列形式相同，因此也可以用函数 f 来表示，记为 f(n-1, m)，那么我们就要找到它映射前是什么数字，那个数字就等于 f(n, m)，映射之前序列中最后剩下的数字为 f'(n-1, m) = g(f(n-1, m)) = (f(n-1, m) + k + 1) % n
f'(n-1, m) 是原来的数，f(n-1, m) 是新的数，套用映射函数，将 k = (m-1)%n 带入上式
得到最终的 f'(n-1, m) = (f(n-1, m) + m)%n = f(n, m)

原来的数为 f(n, m) = f'(n-1, m), 经过映射之后新的数为 f(n-1, m)，因此有 f(n, m) = (f(n-1, m)+k+1)%n

5. f(n, m) = (f(n-1, m) + m) % n， 要得到 n 个数字的序列中最后剩下的数字，就只需要知道 n-1 个数字的数列中最后剩下的数字，并以此类推。 当 n=1 时，序列为 [0]，那么 f(1, m) = 0, 因此最后的递推式为：
```
f(n, m) = 0, 当 n = 1 时
f(n, m) = [f(n-1, m) + m] % n, 当 n > 1 时
```

时间复杂度 O(n)， 空间复杂度 O(1)，效率比去删减数字快得多。

```python
# -*- coding:utf-8 -*-
class Solution:
    def LastRemaining_Solution(self, n, m):
        # write code here
        if n <= 0 or m <= 0:
            return -1
        last = 0
        i = 2
        while i <= n:
            last = (last + m) % i
            i += 1
        return last
```

### 不用加减乘除做加法
写一个函数，求两个整数之和，要求在函数体内不得使用+、-、 * 、/四则运算符号。

思路：用二进制和位运算
1. 先不考虑进位，让 num1 和 num2 的二进制每一位相加，0+0=0, 1+1=0, 0+1=1, 1+0=1, 相当于是二进制的异或操作，得到 sum
2. 记下进位的位置，只有 1+1 才会产生进位，相当于是按位与，并将得到的结果左移一位，得到 carry
3. 让 sum 和 carry 继续重复前两步操作，直到没有产生进位为止，也就是 carry = 0

按照上述思路写下如下代码：
```python
def Add(self, num1, num2):
    # write code here
    while num2:
        sum = num1 ^ num2
        carry = (num1 & num2) << 1
        num1 = sum
        num2 = carry
    return num1
```

在 C++ 中，按照上述思路没有问题，上述代码当输入都是正整数时没有问题，但当输入的 num 包含负数时，会出现死循环，问题就出在 `sum = num1 ^ num2` 上。

实际上，在进行负数的按位加法时，有可能发生在最高位还要向前进一位的情形，正常来说，这种进位因为超出了一个int可以表示的最大位数，应该舍去才能得到正确的结果。因此，对于Java，c，c++这样写是正确的。而对于Python，却有点不同。
在早期版本中如Python2.7中，整数的有int和long两个类型。int类型是一个固定位数的数；long则是一个理论上可以存储无限大数的数据类型。当数大到可能溢出时，为了避免溢出，python会把int转化为long。而Python3.x之后整数只有一个可以放任意大数的int了。可是无论哪种，都是采用了特殊的方法实现了不会溢出的大整数。 所以会使程序无限的算下去，这也是Python效率低的一个原因。

已经知道了右移过程中大整数的自动转化，导致变不成0，那么只需要在移动的过程中加一下判断就行了，把carry的值和 0xffffffff 做一下比较就可以了，代码如下

```python
def Add(self, num1, num2):
    # write code here
    while num2:
        sum = num1 ^ num2
        carry = 0xffffffff & (num1 & num2) << 1
        carry = -(~(carry - 1) & 0xffffffff) if carry > 0x7fffffff else carry # 看不懂？？？
        num1 = sum
        num2 = carry
    return num1
```

0x7fffffff,是 32-bit int的最大值

#### 二叉树的下一个结点
给定一个二叉树和其中的一个结点，请找出中序遍历顺序的下一个结点并且返回。注意，树中的结点不仅包含左右子结点，同时包含指向父结点的指针。

分情况考虑：
1. 当该节点有右子树，那它下一个节点是其右子树的最左边的节点，就从该节点的右孩子出发，一直往左走找到叶子节点
2. 当该节点没有右子树，且是它父节点的左孩子，那么下一个节点就是其父节点
3. 当该节点没有右子树，且是它父节点的右孩子，那么就一直沿着其父节点往上找，直到它位于某一个节点的左子树上，这个就是它的下一个节点（对于 2,3 可以合并为同一种情况）

按照中序遍历（左根右）的规则，当一个节点没有右子树时，要么就是全部遍历完毕，要么是某个节点的左子树全部遍历完毕，下一个节点就是子树的根节点

```python
def GetNext(self, pNode):
    if not pNode:
        return None
    if pNode.right:
        q = pNode.right
        while q.left:
            q = q.left
        return q
    else:
        while pNode.next:
            if pNode.next.left == pNode:
                return pNode.next
            pNode = pNode.next
    return None
```

### 机器人的运动范围
地上有一个m行和n列的方格。一个机器人从坐标0,0的格子开始移动，每一次只能向左，右，上，下四个方向移动一格，但是不能进入行坐标和列坐标的数位之和大于k的格子。 例如，当k为18时，机器人能够进入方格（35,37），因为3+5+3+7 = 18。但是，它不能进入方格（35,38），因为3+5+3+8 = 19。请问该机器人能够达到多少个格子？

思路： 回溯，设置一个 check 函数来检查 [i,j] 这个格子是否可以到达，也就是其行坐标和列坐标的数位之和是否大于 threshold。 初始化一个全局变量 self.cnt 来记录能够到达的格子数。 当某个格子能够到达时，就去看他上下左右的格子是否可以到达，注意已经访问过的节点需要记录下来。

```python
# -*- coding:utf-8 -*-
class Solution:
    def __init__(self):
        self.cnt = 0
    def movingCount(self, threshold, rows, cols):
        # write code here
        if threshold < 0 or (not rows and not cols):
            return 0
        visited = [[False for _ in range(cols)] for _ in range(rows)]
        
        def dfs(i, j):
            if i < 0 or i >= rows or j < 0 or j >= cols or visited[i][j] == True or not self.check(i, j, threshold):
                return 
            self.cnt += 1
            visited[i][j] = True
            dfs(i+1, j)
            dfs(i-1, j)
            dfs(i, j+1)
            dfs(i, j-1)
                
        dfs(0, 0)
        return self.cnt
            
    def check(self, i, j, threshold):
        sum = 0
        carry = 10
        while i:
            sum = sum + i % 10
            i = i // 10
        while j:
            sum = sum + j % 10
            j = j // 10
        return True if sum <= threshold else False
```

#### 二叉搜索树与双向链表
输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。

思路： 对于 BST，其中序遍历的结果是有序数组，转为排序的双向链表后，某个节点的 left 指向左子树中最大的节点，right 指向右子树中最小的节点。 遍历到某个节点时，它的左边已经排好序了，并且处于链表中的最后一个节点就是该节点的 left，然后再去转换该节点的右子树，其转换规则与左子树一样，因此递归转换即可。

设置两个指针 pHead 和 pEnd 分别指向转换后的双向链表的表头和表尾，首先找到链表的第一个节点，也就是 BST 最左边的节点，此时 pHead 和 pEnd 都还是 None，因此把 pHead 和 pEnd 都指向第一个节点，当遍历到下一个节点时，就需要调整指针的指向，链表中最后一个节点 pEnd 的下一个节点应该是当前节点，当左子树转化完成后，就对右子树进行相同的转换。 整个过程就相当于**中序遍历**，只是中间改成了指针的调整

```python
# -*- coding:utf-8 -*-
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
class Solution:
    def __init__(self):
        self.pHead = None
        self.pEnd = None
    def Convert(self, pRootOfTree):
        if not pRootOfTree:
            return None
        self.Convert(pRootOfTree.left) # 中序遍历，一直往左走找到链表的第一个节点
        if not self.pHead: # 只在找到第一个节点时调用一次
            self.pHead = pRootOfTree
            self.pEnd = pRootOfTree
        else: # 调整指针
            self.pEnd.right = pRootOfTree
            pRootOfTree.left = self.pEnd
            self.pEnd = pRootOfTree
        self.Convert(pRootOfTree.right) # 中序遍历
        return self.pHead
```

### 数组中的逆序对
在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组,求出这个数组中的逆序对的总数P。并将P对1000000007取模的结果输出。 即输出P%1000000007

思路： 如果固定一个数字，让它与后面所有的数字作比较，时间复杂度为 O(n^2)，我们可以考虑只比较相邻的两个数字。

可以把问题分解，先将数组中所有的数字拆分为长度为 1 的子数组，再将相邻的两个子数组进行比较，统计出逆序对的个数，同时对两个子数组按照从小到大的顺序进行排序和合并。

1. 用两个指针 i 和 j 分别指向两个子数组的第一个数字，并比较指向数字的大小。如 left=[5,7] 和 right=[4,6]
2. 若第一个子数组中的数字（left[i]=5）大于第二个子数组中的数字（right[j]=6），那么第一个子数组中的包括 i 和 i 之后的所有数字都会大于 right[j] 这个数字，并构成逆序对的个数为 len(left)-i 个，并将 j+1；若小于或等于，则不构成逆序对。
3. 开辟一个辅助数组 tmp，每次把比较中较小的数字添加到 tmp 中，确保其是从小到大排序的。

以上思想类似于归并排序： 先将数组拆分为长度为 1 的子数组，两两合并子数组并统计出相邻两个子数组之间逆序对的个数，合并过程中需要对两个子数组进行排序。

```python
class Solution:
    def __init__(self):
        self.cnt = 0

    def InversePairs(self, data):
        if len(data) <= 1:
            return 0
        self.InversePairsSort(data)
        return self.cnt % 1000000007

    def InversePairsSort(self, data):
        if len(data) <= 1:
            return data
        mid = len(data) // 2
        left = self.InversePairsSort(data[:mid])
        right = self.InversePairsSort(data[mid:])

        i, j = 0, 0
        tmp = []
        while i < len(left) and j < len(right):
            if left[i] <= right[j]:
                tmp.append(left[i])
                i += 1
            else:
                tmp.append(right[j])
                j += 1
                self.cnt = self.cnt + len(left) - i
        tmp += left[i:]
        tmp += right[j:]
        return tmp
```

### 正则表达式匹配
请实现一个函数用来匹配包括'.'和'*'的正则表达式。模式中的字符'.'表示任意一个字符，而'*'表示它前面的字符可以出现任意次（包含0次）。 在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但是与"aa.a"和"ab\*a"均不匹配

思路： 主要是包含 * 的情况比较复杂，需要全面考虑。

对于模式 `ba*ab` 的非确定有限状态机，状态 1：b， 状态 2： `a*`， 状态 3：a， 状态 4：b，当匹配进入状态 2 且字符串的字符是 'a' 时，我们有两种选择：
1. 在模式上后移两个字符进入状态 3 ，因为 `x*` 可以匹配 0 个字符，相当于被忽略，字符串保持不动
2. 选择回到状态 2， 也就是模式保持不变，而字符串向后移动一格字符

因此分为以下几种情况：
- 当第二个字符不是 `*` 时：
1. 若字符串的第一个字符与模式的第一个字符匹配，则字符串和模式都向后移动一个字符，匹配后面的部分
2. 若字符串的第一个字符与模式的第一个字符不匹配， return False

- 当第二个字符是 `*` 时：
若字符串的第一个字符与模式的第一个字符不匹配，则模式向后移动两个字符，字符串不动
若字符串的第一个字符与模式的第一个字符匹配，则有以下三种匹配情况：
1. 模式向后移动两个字符，`x*` 被忽略
2. 模式向后移动两个字符，字符串向后移动一个字符，匹配一次
3. 字符串向后移动一格字符，模式不变，继续向后匹配， `*` 匹配多次

```python
# -*- coding:utf-8 -*-
class Solution:
    # s, pattern都是字符串
    def match(self, s, pattern):
        # write code here
        if s == pattern: # 包含了两者都为空的情况
            return True
        if not pattern: # 也就是 s 非空，pattern 为空
            return False
        if len(pattern) > 1 and pattern[1] == '*':
            if s and (s[0] == pattern[0] or pattern[0] == '.'): # 注意必须先判断是否还有 s，有可能出现 s 为空，但 pattern 还有的情况，比如 x*，仍然可以匹配成功
                return self.match(s, pattern[2:]) or self.match(s[1:], pattern[2:]) or self.match(s[1:], pattern)
            else:
                return self.match(s, pattern[2:])
        else:
            if s and (s[0] == pattern[0] or pattern[0] == '.'):
                return self.match(s[1:], pattern[1:])
            else:
                return False
```

#### 表示数值的字符串
请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，字符串"+100","5e2","-123","3.1416"和"-1E-16"都表示数值。 但是"12e","1a3.14","1.2.3","+-5"和"12e+4.3"都不是。

表示数值的字符串形式： A[.[B]][e|EC] 或 .B[e|EC]， 其中 A、B、C 是数值。
- A 为数值的整数部分，A部分不是必须的，但如果一个数没有整数部分，那么其小数部分不能为空
- B 紧跟在小数点后面为数值的小数部分
- C 紧跟在 'e' 或 'E' 后面为数值的指数部分

其中 A 和 C 可能以 '+' 或 '-' 开头的 0-9 的数位串，B 也是 0-9 的数位串，但前面不能有正负号。

比如字符串 '123.45e+6', '123' 是整数部分 A，'45' 是小数部分 B，'+6' 是指数部分 C。

判断流程：
1. 设置三个变量 has_exp, has_dot, has_sign 分别记录是否出现过 e/E, 小数点, 正负号，然后依次遍历字符串
2. 遍历到 e 或 E，则 e 后面要有数字（可以有符号的），并 has_exp=True ， e 或 E 只能出现一次
3. 遍历到小数点'.'，则前面可以没有数字，但后面必须有数字（无符号），并 has_dot=True， 小数点只能出现一次，且小数点不能在 e 的后面出现
4. 遍历到正负号'+' 或 '-'，后面要接数字，且要么出现在开头，要么接在 e 或 E 的后面，has_sign=True，注意特殊情况如 '-.123' 或 '+.123' 是合法的，所以符号后面可以接小数点

```python
# -*- coding:utf-8 -*-
class Solution:
    # s字符串
    def isNumeric(self, s):
        # write code here
        if not s:
            return False
        has_dot, has_exp, has_sign = False, False, False
        for i in range(len(s)):
            if s[i] == 'e' or s[i] == 'E':
                if has_exp or i == len(s) - 1 or s[i+1] not in '0123456789+-':
                    return False
                has_exp = True
            elif s[i] == '.':
                if has_dot or has_exp or i == len(s) - 1 or s[i+1] not in '0123456789':
                    return False
                has_dot = True
            elif s[i] == '+' or s[i] == '-':
                if i == len(s) - 1 or s[i+1] not in '0123456789.':
                    return False
                if i != 0 and s[i-1] not in 'eE':
                    return False
                has_sign = True
            elif s[i] not in '0123456789':
                return False
        return True
```

### 序列化二叉树
请实现两个函数，分别用来序列化和反序列化二叉树

**二叉树的序列化**：把一棵二叉树按照某种遍历方式的结果以某种格式保存为字符串，从而使得内存中建立起来的二叉树可以持久保存。序列化可以基于先序、中序、后序、层序的二叉树遍历方式来进行修改，序列化的结果是一个字符串，序列化时通过 某种符号表示空节点（#），以 ！ 表示一个结点值的结束（value!）。

**二叉树的反序列化**：根据某种遍历顺序得到的序列化字符串结果str，重构二叉树

思路： 我们知道通过二叉树前序遍历和中序遍历的结果可以构造一颗二叉树，但这要求二叉树中不能有值相同的节点。如果二叉树的序列化是从根节点开始的，那么相应的反序列化就可以从根节点开始，因此可以根据前序遍历来进行二叉树的序列化，在遇到左右孩子为空的情况时，可以用特殊字符 '#' 来表示。

```python
# -*- coding:utf-8 -*-
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
class Solution:
    def __init__(self):
        self.serial = []
    def Serialize(self, root):
        # write code here
        if not root:
            self.serial.append('#')
        else:
            self.serial.append(str(root.val))
            self.Serialize(root.left)
            self.Serialize(root.right)
        return ' '.join(self.serial)

    def Deserialize(self, s):
        # write code here
        serial = s.split()
        def dePre():
            val = serial.pop(0)
            if val == "#":
                return None
            node = TreeNode(int(val))
            node.left = dePre()
            node.right = dePre()
            return node
        return dePre()
```

#### 滑动窗口的最大值
给定一个数组和滑动窗口的大小，找出所有滑动窗口里数值的最大值。例如，如果输入数组{2,3,4,2,6,2,5,1}及滑动窗口的大小3，那么一共存在6个滑动窗口，他们的最大值分别为{4,4,6,6,6,5}； 针对数组{2,3,4,2,6,2,5,1}的滑动窗口有以下6个： {[2,3,4],2,6,2,5,1}， {2,[3,4,2],6,2,5,1}， {2,3,[4,2,6],2,5,1}， {2,3,4,[2,6,2],5,1}， {2,3,4,2,[6,2,5],1}， {2,3,4,2,6,[2,5,1]}。

思路一： 直接遍历每个滑动窗口的最大值，若数组长度为 n，滑动窗口大小为 k，则时间复杂度为 O(n)，相同位置的数字被遍历了多次。
```python
def maxInWindows(self, num, size):
    if size > len(num) or size <= 0:
        return []
    res = []
    max_i = -float("inf")
    max_num = -float("inf")
    for i in range(len(num)):
        if num[i] > max_num
    return res
```

思路二： 用一个数组 tmp 来存放滑动窗口的最大值，和接下来可能成为最大值的次大值（因为之前的最大值可能会滑出窗口），为了方便比较数字是否已经滑出窗口，tmp 中存放的是数值所在位置的下标

```python
def maxInWindows(self, num, size):
    # write code here
    if size > len(num) or size <= 0:
        return []
    if not num:
        return []
    if size == 1:
        return num
    tmp = [0]
    res = []
    for i in range(1, len(num)):
        if i - tmp[0] >= size: # 首先判断当前的最大值是否已经滑出窗口
            tmp.pop(0)
        while tmp and num[i] >= num[tmp[-1]]: # 将第 i 个元素与 tmp 中的值比较，比 nums[i] 小的都弹出，因为他们不可能成为后面窗口的最大值
            tmp.pop()
        tmp.append(i)
        if i >=  size-1:
            res.append(num[tmp[0]])
    return res      
    
```
