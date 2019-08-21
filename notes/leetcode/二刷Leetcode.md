# 二刷 Leetcode
## 提高效率！！！

<!-- GFM-TOC -->
* [2. Add Two Numbers](#add-two-numbers)
* [3. Longest Substring Without Repeating Characters](#longest-substring-without-repeating-characters)
* [** 较难 4. Median of Two Sorted Arrays](#median-of-two-sorted-arrays)
* [5. Longest Palindromic Substring](#longest-palindromic-substring)
* [6. ZigZag Conversion](#zigZag-conversion)
* [9. Palindrome Number](#palindrome-number)
* [12. 13. Integer and Roman](#integer-to-roman)
* [17. Letter Combinations of a Phone Number](#letter-combinations-of-a-phone-number)
* [19. Remove Nth Node From End of List](#remove-nth-node-from-end-of-list)
* [22. Generate Parentheses](#generate-parentheses)
* [29. Divide Two Integers](#divide-two-integers)
* [31. Next Permutation](#next-permutation)
* [33. Search in Rotated Sorted Array](#search-in-rotated-sorted-array)
* [34. Find First and Last Position of Element in Sorted Array](#find-first-and-last-position-of-element-in-sorted-array)
* [38. Count and Say](#count-and-say)
* [** 大数乘法 43. Multiply Strings](#multiply-strings)
* [49. Group Anagrams](#group-anagrams)
* [50. Pow(x, n)](#powx-n)
* [51. N-Queens](#n-queens)
* [53. Maximum Subarray](#maximum-subarray)
* [54. Spiral Matrix](#spiral-matrix)
* [55. Jump Game](#jump-game)
* [60. Permutation Sequence](#permutation-sequence)
* [注意优化 61. Rotate List](#rotate-ist)
* [71. Simplify Path](#simplify-path)
* [** 73. Set Matrix Zeroes](#set-matrix-zeroes)
* [74. Search a 2D Matrix](#search-a-2d-matrix)
* [75. Sort Colors](#sort-colors)
* [** 79. Word Search](#word-search)
* [81. Search in Rotated Sorted Array II](#search-in-rotated-sorted-array-ii)
* [82. Remove Duplicates from Sorted List II](#remove-duplicates-from-sorted-list-ii)
* [88. Merge Sorted Array](#merge-sorted-array)
* [89. Gray Code](#gray-code)
* [91. Decode Ways](#decode-ways)
* [** 92. Reverse Linked List II](#reverse-linked-list-ii)
* [** 记住 95. Unique Binary Search Trees II](#unique-binary-search-trees-ii)
* [96. Unique Binary Search Trees](#unique-binary-search-trees)
* [98. Validate Binary Search Tree](#validate-binary-search-tree)
* [100. Same Tree](#same-tree)
* [101. Symmetric Tree](#symmetric-tree)
* [105. Construct Binary Tree from Preorder and Inorder Traversal](#construct-binary-tree-from-preorder-and-inorder-traversal)
* [110. Balanced Binary Tree](#balanced-binary-tree)
* [112. Path Sum](#path-sum)
* [114. Flatten Binary Tree to Linked List](#flatten-binary-tree-to-linked-list)
* [116. Populating Next Right Pointers in Each Node](#populating-next-right-pointers-in-each-node)
* [** 117. Populating Next Right Pointers in Each Node II](#populating-next-right-pointers-in-each-node-ii)
* [123. Best Time to Buy and Sell Stock III](#best-time-to-buy-and-sell-stock-iii)
* [127. Word Ladder](#word-ladder)
* [130. Surrounded Regions](#surrounded-regions)
* [** 没做，图的深拷贝 133. Clone Graph](#clone-graph)
* [136. Single Number](#single-number)
* [** 没做，位操作，较难 137. Single Number II](#single-number-ii)
* [** 没做，链表深拷贝 138. Copy List with Random Pointer](#copy-list-with-random-pointer)
* [139. Word Break](#word-break)
* [147. Insertion Sort List](#insertion-sort-list)
* [148. Sort List](#sort-list)
* [150. Evaluate Reverse Polish Notation](#evaluate-reverse-polish-notation)
* [152. Maximum Product Subarray](#maximum-product-subarray)
* [153 Find Minimum in Rotated Sorted Array](#find-minimum-in-rotated-sorted-array)
* [154. Find Minimum in Rotated Sorted Array II](#find-minimum-in-rotated-sorted-array-ii)
* [160. Intersection of Two Linked Lists](#intersection-of-two-linked-lists)
* [162. Find Peak Element](#find-peak-element)
* [168. Excel Sheet Column Title](#excel-sheet-column-title)
* [171. Excel Sheet Column Number](#excel-sheet-column-number)
* [174. Dungeon Game](#dungeon-game)
* [179. Largest Number](#largest-number)
* [** 位运算可解 187. Repeated DNA Sequences](#repeated-dna-sequences)
* [189. Rotate Array](#rotate-array)
* [190. Reverse Bits](#reverse-bits)
* [191. Number of 1 Bits](#number-of-1-bits)
* [200. Number of Islands](#number-of-islands)
* [201. Bitwise AND of Numbers Range](#bitwise-and-of-numbers-range)
* [** 没做，素数计算 204. Count Primes](#count-primes)
* [205. Isomorphic Strings](#isomorphic-strings)
* [209. Minimum Size Subarray Sum](#minimum-size-subarray-sum)
* [215. Kth Largest Element in an Array](#kth-largest-element-in-an-array)
* [219. Contains Duplicate II](#contains-duplicate-ii)
* [221. Maximal Square](#maximal-square)
* [222. Count Complete Tree Nodes](#count-complete-tree-nodes)
* [** 队列实现栈 225. Implement Stack using Queues](#implement-stack-using-queues)
* [** 栈实现队列 232. Implement Queue using Stacks](#implement-queue-using-stacks)
* [223. Rectangle Area](#rectangle-area)
* [229. Majority Element II](#majority-element-ii)
* [235. Lowest Common Ancestor of a Binary Search Tree](#lowest-common-ancestor-of-a-binary-search-tree)
* [236. Lowest Common Ancestor of a Binary Tree](#lowest-common-ancestor-of-a-binary-tree)
* [237. Delete Node in a Linked List](#delete-node-in-a-linked-list)
* [279. Perfect Squares](#perfect-squares)
* [287. Find the Duplicate Number](#find-the-duplicate-number)
* [300. Longest Increasing Subsequence](#longest-increasing-subsequence)
* [** 完全背包 322. Coin Change](coin-change)
<!-- GFM-TOC -->

133, 138 关于深拷贝， 137 位运算暂时搁置
187,190,191,199,200,201,204

### Add Two Numbers
[Leetcode : 2. Add Two Numbers(Medium)](https://leetcode.com/problems/add-two-numbers/description/)

old： 遍历一遍两个链表，得到存储的数字，再将两数字相加，创建新的链表。

improve: 直接一次遍历，在得到两个节点的值时，就开始计算两数之和，用 carry 表示两个节点的和，若 >= 10，则表示要进位。

```python
def addTwoNumbers(self, l1, l2):
    dummy = ListNode(0)
    cur = dummy
    carry = 0
    while l1 or l2 or carry:
        if l1:
            carry += l1.val
            l1 = l1.next
        if l2:
            carry += l2.val
            l2 = l2.next
        carry, n = divmod(carry, 10)
        cur.next = ListNode(n)
        cur = cur.next
    return dummy.next
```

### Longest Substring Without Repeating Characters
[Leetcode : 3. Longest Substring Without Repeating Characters(Medium)](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

可以用字典来存储某个字符，在之前的子串中，最后一次出现的位置。

### 两个有序数组的中位数 Median of Two Sorted Arrays
[Leetcode : 4. Median of Two Sorted Arrays (Hard)](https://leetcode.com/problems/median-of-two-sorted-arrays/description/)

要求时间复杂度为 O(log(m+n))，显然是二分查找
暂且放弃

### Longest Palindromic Substring
[Leetcode : 5. Longest Palindromic Substring (Medium)](https://leetcode.com/problems/longest-palindromic-substring/description/)

通过枚举每个回文子串的中心，然后往左右两边扩展，来得到最长回文子串。用 left 和 right 表示边界。  
可以改进的地方是：如果有相同字母连在一起的情况，则先找到这一串连在一起的字母，再向两边扩展。

### ZigZag Conversion
[Leetcode : 6. ZigZag Conversion (Medium)](https://leetcode.com/problems/zigzag-conversion/description/)

找规律型题，画出图来，然后看每一行到下一个字符的步长，注意第一行和最后一行的步长是相同的，而中间的行会出现两种不同的步长。

### Palindrome Number
[Leetcode : 9. Palindrome Number (Easy)](https://leetcode.com/problems/palindrome-number/description/)

不允许将 int 转为 str，因此可以用除法和取模来判断。  
加快速度：只判断一半的数字即可，同时要注意字符长度为奇数和偶数的不同情况。并且可以直接排除掉能够整除 10 的数字。

### Integer to Roman
[Leetcode : 12. Integer to Roman (Medium)](https://leetcode.com/problems/integer-to-roman/description/)

枚举数字，再用除法和取模计算即可。

### Roman to Integer
[Leetcode : 13. Roman to Integer (Easy)](https://leetcode.com/problems/roman-to-integer/description/)

利用字典存储罗马字符对应的数值，遍历一遍字符串，直接相加对应的数值，当遇到某个数比前一个数更大的情况时，需要将 sum 减去两倍的前一个数。

### Letter Combinations of a Phone Number
[Leetcode : 17. Letter Combinations of a Phone Number(Medium)](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/)

一般组合问题，用回溯法，套路都基本类似

### ### Remove Nth Node From End of List
[Leetcode : 19. Remove Nth Node From End of List (Medium)](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)
快慢指针法： fast 先走 n 步，然后 slow 与 fast 同步走，当 fast 走到底时， slow.next 就是要删除的节点。

### Generate Parentheses
[Leetcode : 22. Generate Parentheses(Medium)](https://leetcode.com/problems/generate-parentheses/description/)

组合问题：回溯法。  
注意 dfs 函数的输入，是左括号和右括号的数量，并且当左括号剩余数量大于有括号剩余数量时，是不可能生成的。

### Divide Two Integers
[Leetcode : 29. Divide Two Integers (Medium)](https://leetcode.com/problems/divide-two-integers/description/)

利用位操作来加快速度，左移一位相当于将某个数 * 2， 当被除数比除数小时，则需要重置除数为 divisor

### Next Permutation
[Leetcode : 31. Next Permutation (Medium)](https://leetcode.com/problems/next-permutation/description/)

记住该题的解法：分三步走  
1. 从后往前，找到第一对前一个数比后一个数小的， nums[i] < nums[i+1]
2. 从后往前，找到第一个比 nums[i] 更大的数 nums[j]， 交换两个数的位置
3. 对 i 之后的数进行升序排序

### Search in Rotated Sorted Array
[Leetcode : 33. Search in Rotated Sorted Array (Medium)](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)

要求时间复杂度为 O(logn)，必是二分查找。有三种情况，先要知道左右哪个部分是有序的，才能知道 target 会落在哪。  
利用 nums[mid] 与 左右两边 进行比较来判断哪一个部分是有序的，再利用有序的那部分判断 target 是否会在有序的这边，从而移动 left 和 right。

### Find First and Last Position of Element in Sorted Array
[Leetcode : 34. Find First and Last Position of Element in Sorted Array (Medium)](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/)

两次二分查找，第一次找到第一个相等的元素下标，再将边界设为 left，len-1 进行第二次二分查找，找到最后一个相等的元素。 若第一次就没找到，就返回 [-1, -1]

### Count and Say
[Leetcode : 38. Count and Say (Easy)](https://leetcode.com/problems/count-and-say/description/)

设计一个函数，输入一个字符串，得到规则的下一个字符串。然后主函数循环遍历即可。  
遍历字符串，相同字符则 cnt+1, 不同字符则将其 计数和该字符 加到 res 中，并重置比较字符和 cnt。

### Multiply Strings
[Leetcode : 43. Multiply Strings (Medium)](https://leetcode.com/problems/multiply-strings/description/)

字符串相乘，实际上是大数相乘。 **记住该方法**  
1. 将两个字符串反转
2. 按位进行相乘，存储到一个数组中，最后相乘的数，位数最多会是 len(num1) + len(num2) - 1
3. 对数组中的数，对 10 取模即该位的数，除 10 即为进位的数，最后将相乘后得到的字符串前面的 0  去掉

```python
def multiply(self, num1, num2):
    num1 = num1[::-1]
    num2 = num2[::-1]
    arr = [0 for i in range(len(num1)+len(num2))]
    for i in range(len(num1)):
        for j in range(len(num2)):
            arr[i+j] += int(num1[i]) * int(num2[j])
    res = ""
    for i in range(len(arr)):
        n = arr[i] % 10
        carry = arr[i] // 10
        if i < len(arr)-1:
            arr[i+1] += carry
        res += str(n)
    res = res[::-1]
    return '0' if res == '0'*(len(num1)+len(num2)) else res.lstrip('0')
```

### Group Anagrams
[Leetcode : 49. Group Anagrams (Medium)](https://leetcode.com/problems/group-anagrams/description/)

将字典作为结果存储格式，最后返回字典的 values，再将其转为 list。  
用字典存储每个 word 排序后的结果， anagrams 排序后会是一样的 key。

```python
def groupAnagrams(self, strs):
    res = {}
    for word in strs:
        key = ''.join(sorted(word))
        if key in res:
            res[key].append(word)
        else:
            res[key] = [word]
    return list(res.values())
```

### Pow(x, n)
[Leetcode : 50. Pow(x, n) (Medium)](https://leetcode.com/problems/powx-n/description/)

直接 o(n) 解法超时，需要将幂不断除2，将时间复杂度降到 o(logn)。注意要分奇偶情况。

### N-Queens
[Leetcode : 51. N-Queens(Hard)](https://leetcode.com/problems/n-queens/description/)

N 皇后问题：使用一个一维数组 board[i] = j 来存储第 i 行的第 j 列是否可以放置棋子，这样就不需要判断棋子是否会在同一行。然后构建一个 check(i, j) 函数来判断第 i 行的第 j 列是否能够放置，需要与前 n-1 行数据作比较，比较棋子是否会在同一列或者同一斜线上。

### Maximum Subarray
[Leetcode : 53. Maximum Subarray (Easy)](https://leetcode.com/problems/maximum-subarray/description/)

动态规划，用 dp[i] 存储以 nums[i] 结尾的子数组的最大和， 则 dp[i] = max(dp[i-1]+nums[i], nums[i])，由于只用到 dp[i-1], 可以直接降维，简化为 dp；  
用 max_sum 存储全局的子数组的最大和，则 max_sum = max(max_sum, dp)

### Spiral Matrix
[Leetcode : 54. Spiral Matrix(Medium)](https://leetcode.com/problems/spiral-matrix/description/)

设置四个方向，依次输出，但需要注意终止条件，输出数组大小等于原矩阵大小即停止，否则可能会输出重复的数字。

### Jump Game
[Leetcode : 55. Jump Game(Medium)](https://leetcode.com/problems/jump-game/description/)

每次只往前面走一步，用 step 来记录剩余还能走的最大步数，当 step==0 时，则不能继续往前，return False

### Permutation Sequence
[Leetcode : 60. Permutation Sequence (Medium)](https://leetcode.com/problems/permutation-sequence/description/)

数学上的技巧性比较大，主要是排列组合问题。 以某一个数字开头的组合有 (n-1)! 种，根据数字的大小，可以一位一位来判断下一个数是什么，比如 n=4，k=9 时，必定是以 2 开头的组合 2+[1,3,4] 然后再找下一位数字是什么，注意每次选定一个数后就在原数组中将其删除，当 nums 中没有数字时，则找到第 k 个排列的数字。

```python
def getPermutation(self, n, k):
    res = ''
    nums = [i for i in range(1, n+1)]
    k = k - 1
    while nums:
        n -= 1
        index, k = divmod(k, math.factorial(n))
        res += str(nums[index])
        nums.pop(index)
    return res
```

### Rotate List
[Leetcode : 61. Rotate List (Medium)](https://leetcode.com/problems/rotate-list/description/)

自己做出来了，但最后翻转的时候用快慢指针法进行改进，fast 先走 k 步，然后 fast 和 slow 同步走，当 fast 走到最后时， slow.next 就是翻转后的头部，此时将 fast.next = head, head = slow.next, slow.next = None

### Simplify Path
[Leetcode : 71. Simplify Path (Medium)](https://leetcode.com/problems/simplify-path/description/)

利用堆栈实现，注意出现 '...' ，将其当做普通字符，因此需要判断的情况有三种：  
1. char == '.' or not char  不管，继续
2. char == '..'，若此时 stack 非空，则出栈
3. 其他字符： 进栈  
注意最后的输出格式。

### Set Matrix Zeroes
[Leetcode : 73. Set Matrix Zeroes (Medium)](https://leetcode.com/problems/set-matrix-zeroes/description/)

要求空间复杂度为 O(1)，可以将需要置为 0 的行号和列号记录在第 0 行和第 1 列，并记下第 0 列的原始数据是否本来就含有 0。

### Search a 2D Matrix
[Leetcode : 74. Search a 2D Matrix (Medium)](https://leetcode.com/problems/search-a-2d-matrix/description/)

使用分治法，比较右上角的数字与 target 的值，将原矩阵不断缩小。  
由于 matrix 是按行递增也按列递增的, 若 target>右上角，则肯定在下面的行中， row+1；  
若 targte<右上角，则肯定在左边的列中， col-1。

### Sort Colors
[Leetcode : 75. Sort Colors (Medium)](https://leetcode.com/problems/sort-colors/description/)

要求时间复杂度为 O(1)，因此可以用双指针，p0 指向 0 要存储的位置，p2 指向 2 要存储的位置，遍历一次数组，遇到 0 就将其与 p0 位置交换，遇到 2 就将其与 p2位置交换，遇到 1 则跳过。需要注意的是，交换 p2 后不需要 i+1，因此 i 位置可能会变为 1。

### Word Search
[Leetcode : 79. Word Search (Medium)](https://leetcode.com/problems/word-search/description/)

回溯，先在 board 中找到 word 的第一个字母，再根据该位置从“上下左右”四个方向去 DFS 后面的字母。  
用二维数组 visit 来记录 board[i][j] 是否被访问过，由于是递归，因此一次递归完成后，该节点应再标记为未访问。

### Search in Rotated Sorted Array II
[Leetcode : 81. Search in Rotated Sorted Array II (Medium)](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/description/)

二分查找，拿 nums[mid] 与 num[left] 相比来判断左右哪边是有序的，再拿 target 与有序的一边的两端元素相比，来判断 target 到底在哪边。  
需要注意的是：该题相比 33 有重复元素的存在，因此只需要添加一条 if nums[mid] == nums[left] : left += 1

### Remove Duplicates from Sorted List II
[Leetcode : 82. Remove Duplicates from Sorted List II (Medium)](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/description/)

用一个标记 is_repeated 记录是否出现过重复的节点，如果遇到重复节点，就先 pass 这些节点，直到 cur.val != cur.next.val 为止。

### Merge Sorted Array
[Leetcode : 88. Merge Sorted Array (Easy)](https://leetcode.com/problems/merge-sorted-array/description/)

归并两个有序数组，相当于是归并排序的归并这一步。  
应该从后往前来计算，用 cur 记录下当前位置，通过判断 nums1[i] 和 nums2[j] 哪个更大来看 cur 应该放哪个数字。当 j = -1 时，nums2 中的数去全部插进去了。 注意最后可能会 j >= 0，需要把 nums2 剩下的数查到 num1 的前面。 

### Gray Code
[Leetcode : 89. Gray Code (Medium)](https://leetcode.com/problems/gray-code/description/)

记住：格雷码：两个相邻的码的二进制只有一位是不同的，就是将 i 与 右移一位的 i 进行异或

### Decode Ways
[Leetcode : 91. Decode Ways (Medium)](https://leetcode.com/problems/decode-ways/description/)

动态规划，用 dp[i] 表示前 i 个字符能够解码的方法数，此处的 1<=i<=len(s)。  
有三种情况，s[i-2:i] == '10' or '20'， 11<=int(s[i-2:i])<=26，其他  
注意其他不能以 0 开头，比如含有 90 不能解码成功
注意边界，以 0 开头的字符串不能解码成功


### Reverse Linked List
[Leetcode : 92. Reverse Linked List II (Medium)](https://leetcode.com/problems/reverse-linked-list-ii/description/)

将链表分成三段，找到每段的起点和终点，只需要反转中间这一段

```python
def reverseBetween(self, head, m, n):
    if not head or not head.next or m == n:
        return head
    dummy = ListNode(0)
    dummy.next = head
    p1 = dummy
    for _ in range(m-1):
        p1 = p1.next # p1 记录下m的前一个节点，也就是第一部分的终点
    
    pre = None
    cur = p1.next
    p2 = cur # 反转后第二段的终点
    for _ in range(n-m+1): # 开始反转，到第 n 个节点需要经过 n-m 次
        tmp = cur.next
        cur.next = pre
        pre = cur
        cur = tmp
    p2.next = cur # cur 是第三段的起点
    p1.next = pre # pre 是第二段的起点
    return dummy.next
```

### Restore IP Addresses
[Leetcode : 93. Restore IP Addresses(Medium)](https://leetcode.com/problems/restore-ip-addresses/description/)

回溯，先判断边界，注意回溯停止的条件有两个 if not s and len(ip) == 4

```python
def restoreIpAddresses(self, s):
    if len(s) > 12:
        return []
    res = []
    def dfs(s, ip):
        if not s and len(ip) == 4:
            res.append('.'.join(ip))
            return 
        for i in range(len(s)):
            if i >= 3:
                break
            number = int(s[:i+1])
            if number <= 255 and str(number) == s[:i+1]: # 需要注意此处，为了避免 01 这种情况发生
                dfs(s[i+1:], ip+[s[:i+1]])
    dfs(s, [])
    return res
```

### Unique Binary Search Trees II
[Leetcode : 95. Unique Binary Search Trees II (Medium)](https://leetcode.com/problems/unique-binary-search-trees-ii/description/)

对于以 i 为根节点的 BST，1...i-1 构成左子树，i+1...n 构成右子树。  
把左子树的元素和右子树的元素递归出一个数组，从两个数组中取节点拼接成树。

** 背下来！！！ **
```python
def generateTrees(self, n):
    if not n:
        return []
    def dfs(begin, end):
        if begin > end:
            return [None]
        res = []
        for i in range(begin, end+1):
            left = dfs(begin, i-1)
            right = dfs(i+1, end)
            for l in left:
                for r in right:
                    root = TreeNode(i)
                    root.left = l
                    root.right = r
                    res.append(root)
        return res
    return dfs(1, n)
```

### Unique Binary Search Trees
[Leetcode : 96. Unique Binary Search Trees (Medium)](https://leetcode.com/problems/unique-binary-search-trees/description/)

dp[i] 表示长度为 i 的序列能够组成的 BST 数。  
F(j, i) 表示以 j 为根节点的，长度为 i 的序列能够组成的 BST 数，则该树的左子树有 j-1 个节点，右子树有 i-j 个节点。1<=j<=i  
dp[i] = F(1, i) + F(2, i) + ... + F(j, i) + ... + F(i, i)  
F(j, i) = dp[j-1] * dp[i-j]  
则有 dp[i] = dp[0] * dp[i-1] + dp[1] * dp[i-2] + ... + dp[i-1] * dp[0]

```python
def numTrees(self, n):
    dp = [0 for i in range(n+1)]
    dp[0] = dp[1] = 1
    for i in range(2, n+1):
        for j in range(1, i+1):
            dp[i] += dp[j-1] * dp[i-j]
    return dp[-1]
```

### Validate Binary Search Tree
[Leetcode : 98. Validate Binary Search Tree (Medium)](https://leetcode.com/problems/validate-binary-search-tree/description/)

利用 BST 中序遍历的结果是有序数组来验证是否为 BST，当前访问的节点值 <= 前一个节点值时，return False

### Same Tree
[Leetcode : 100. Same Tree (Easy)](https://leetcode.com/problems/same-tree/description/)

简单的递归，注意 return p.val == q.val and self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)

### Symmetric Tree
[Leetcode : 101. Symmetric Tree (Easy)](https://leetcode.com/problems/symmetric-tree/description/)

判断 left.left 与 right.right， left.right 与 right.left 是否是对称树。  
构造一个函数 helper 来判断 left 和 right 是否对称。

### Construct Binary Tree from Preorder and Inorder Traversal
[Leetcode : 105. Construct Binary Tree from Preorder and Inorder Traversal (Medium)](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)

前序遍历的第一个元素是根节点，找到根节点在中序遍历的位置 i，则 i 左边的是左子树， i 右边的是右子树，再找到左子树和右子树的前序遍历，递归构造即可

### Balanced Binary Tree
[Leetcode : 110. Balanced Binary Tree (Easy)](https://leetcode.com/problems/balanced-binary-tree/description/)

需要使用到 maxDepth 函数，求树的最大高度，当左子树与右子树的高度差大于 1 时，return False

### Path Sum
[Leetcode : 112. Path Sum (Easy)](https://leetcode.com/problems/path-sum/description/)

递归，只有当 sum == 0 且节点为叶子节点时，才 return True

若要找到所有符合条件的解，用回溯法
```python
def pathSum(self, root, sum):
    def dfs(root, sum, path):
        if not root:
            return 
        sum -= root.val
        if sum == 0 and not root.left and not root.right:
            path = path+[root.val] # 别忘记把最后一个节点添加到 path 里
            res.append(path)
        dfs(root.left, sum, path+[root.val])
        dfs(root.right, sum, path+[root.val])
        
    res = []
    dfs(root, sum, [])
    return res
```

### Flatten Binary Tree to Linked List
[Leetcode : 114. Flatten Binary Tree to Linked List (Medium)](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/description/)

相当于按照前序遍历组织二叉树，因此可以先得到前序遍历的结果，再构造二叉树

### Populating Next Right Pointers in Each Node
[Leetcode : 116. Populating Next Right Pointers in Each Node(Medium)](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/description/)

本题中的二叉树是完全二叉树，因此对于 root，有左孩子的话必定有右孩子，此时将 root.left.next = root.right。  
对于右孩子，当有 root.next 是， root.right.next = root.next.left，否则是右边的节点 next 为 None

### Populating Next Right Pointers in Each Node II
[Leetcode : 117. Populating Next Right Pointers in Each Node II (Medium)](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/description/)

相对于上一题，二叉树不是完全二叉树。  
需要考虑的情况很多，在有 root 的条件下：
1. root 有左孩子，也有右孩子，直接指向 root.left.next = root.right
2. root 只有左孩子，则需要根据下一个 root.next 的孩子来得到 root.left 的指向
3. root 只有右孩子，则需要根据下一个 root.next 的孩子来得到 root.right 的指向  

构造一个函数 helper(node) 来判断 root.next 的孩子情况，从而得到 root 的孩子需要指向哪个节点：
1. node 为空，则 root 没有 next，那么指向 None
2. node 有左孩子，则指向 node.left
3. node 有右孩子，但没有左孩子，则指向 node.right
4. node 既没有左孩子也没有右孩子，则需要根据下一个 node.next 来判断应该指向哪个节点，因此递归 self.helper(node.next)

```python
def connect(self, root):
    if root:
        if root.left:
            if root.right:
                root.left.next = root.right
            else:
                root.left.next = self.helper(root.next)
        if root.right:
            root.right.next = self.helper(root.next)
        self.connect(root.right)
        self.connect(root.left)
           
def helper(self, node):
    if not node:
        return None
    if node.left:
        return node.left
    elif node.right:
        return node.right
    return self.helper(node.next)
```

### Best Time to Buy and Sell Stock III
[Leetcode : 123. Best Time to Buy and Sell Stock III (Hard)](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/description/)

最多可以进行两次交易，若将数组分为两个部分，分别计算各自的最大利润，会超时。  
考虑设置两个数组， p1[i] 存储前 i 天的最大利润， p2[i] 天存储 i 天之后的最大利润。  
p1 计算方法与之前的相同， p2 需要从后往前算，保存的应该当前的最大值 pmax。

### Word Ladder
[Leetcode : 127. Word Ladder (Medium)](https://leetcode.com/problems/word-ladder/description/)

1. 用队列 queue 存储能够成功变换的单词及当前变化的次数 queue = [[word, length]]，alphas 存储单词的所有不同字符。
2. 当有 queue 时，先进先出，遍历这个单词的每个字符，将其替换为 alphas 中的每个字符，判断得到的新单词是否在 wordList 中，且新单词不能和旧单词一样。
3. 注意已经找到的单词需要从 wordList 中删除，成功找到的话就 length + 1
4. 注意用 set 比 list 更快, 先将 wordList 变为 set

### Surrounded Regions
[Leetcode : 130. Surrounded Regions (Medium)](https://leetcode.com/problems/surrounded-regions/description/)

1. 搜索边缘的元素，第一行和最后一个，第一列和最后一咧，若为 O，则将其置换成其他的字母如 D
2. 然后搜索该元素的上下左右位置，当超出范围或元素 != 'O' 时，则返回
3. 再遍历一遍，board 中还存在的 O 是被包围的，将其置换为 X，再将所有的 D 变为 O

### Clone Graph
[Leetocde : 133. Clone Graph (Medium)](https://leetcode.com/problems/clone-graph/description/)

### Gas Station
[Leetcode : 134. Gas Station (Medium)](https://leetcode.com/problems/gas-station/description/) 

1. 当 sum(gas) < sum(cost) 时，肯定不能跑完全程；当 sum(gas) >= sum(cost) 时，必然存在一个点，从该点出发能够跑完全程
2. 用 rest 记录剩余的油量，用 index 记录出发点
3. 当 rest < 0 时，说明从 index 出发不能跑完，index 处的油量肯定是 >= index+1 到 i 处的油量的，那么在 index 到 i 这一段都不能作为起点，因此重置 index = i + 1， res = 0

### Single Number
[Leetocde : 136. Single Number (Easy)](https://leetcode.com/problems/single-number/description/)

要求时间复杂度 O(n), 空间复杂度 O(1)  
用位运算实现，由于异或操作的顺序不影响结果，考虑将数组中的所有数字异或。  
x^0=x, x^x=0，例如 [4,1,2,1,2], 则 4^1^2^1^2 = 4^(1^1^2^2) = 4^0 = 4

```python
def singleNumber(self, nums):
    res = nums[0]
    for i in range(1, len(nums)):
        res = res ^ nums[i]
    return res
```

### Single Number II
[Leetocde : 137. Single Number II (Medium)](https://leetcode.com/problems/single-number-ii/description/)

### Copy List with Random Pointer
[Leetcode : 138. Copy List with Random Pointer (Medium)](https://leetcode.com/problems/copy-list-with-random-pointer/description/)

### Word Break
[Leetcode : 139. Word Break (Medium)](https://leetcode.com/problems/word-break/description/)

动态规划，dp[i] 表示到第 i 个字母时能够被正确分割，对于 leetcode， dp[0], dp[4], dp[8] 为 True  
遍历 s 的每个字符，再遍历每一个单词，若 s[i-len(word):i] == word and dp[i-len(word)] == True，得当前的 dp[i] 也可以被正确分割

### Insertion Sort List
[Leetcode : 147. Insertion Sort List (Medium)](https://leetcode.com/problems/insertion-sort-list/description/)

链表的插入排序，注意链表不能和数组一样从后往前遍历，因此需要从前往后寻找待排序的节点应该插入的正确位置。  
用 pre 记录前一个节点，cur 记录当前节点，则待排序节点为 cur.next

```python
def insertionSortList(self, head):
    if not head or not head.next:
        return head
    dummy = ListNode(0)
    dummy.next = head
    cur = head
    while cur.next:
        if cur.next.val >= cur.val: # 由于前面已经有序，当待排序节点值比前一个大时则不需要排序
            cur = cur.next
        else:
            pre = dummy
            tmp = cur.next
            while pre.next.val <= tmp.val: # 找到待排序节点 tmp 需要插入的正确位置，也就是 pre.next
                pre = pre.next
            cur.next = cur.next.next
            tmp.next = pre.next
            pre.next = tmp
    return dummy.next
```

### Sort List
[Leetcode : 148. Sort List (Medium)](https://leetcode.com/problems/sort-list/description/)

要求时间 O(nlogn) 空间 O(1)，链表的归并排序，用快慢指针法来找到中点

```python
def sortList(self, head):
    if not head or not head.next:
        return head
    slow = fast = head
    while fast.next and fast.next.next: # 注意此处，与环形链表的条件不一样
        slow = slow.next
        fast = fast.next.next
    right = self.sortList(slow.next)
    slow.next = None
    left = self.sortList(head)
    return self.merge(left, right)

def merge(self, left, right):
    dummy = ListNode(0)
    cur = dummy
    while left and right:
        if left.val < right.val:
            cur.next = left
            left = left.next
        else:
            cur.next = right
            right = right.next
        cur = cur.next
    if left:
        cur.next = left
    if right:
        cur.next = right
    return dummy.next
```

### Evaluate Reverse Polish Notation
[Leetcode : 150. Evaluate Reverse Polish Notation (Medium)](https://leetcode.com/problems/evaluate-reverse-polish-notation/description/)

实现逆波兰式的四则运算，用 stack 即可。判断是否为数字时，由于有负数，可以用 if char.lstrip('-').isdigit()

### Maximum Product Subarray
[Leetcode : 152. Maximum Product Subarray (Medium)](https://leetcode.com/problems/maximum-product-subarray/description/)

1. dp[i] 记录以下标为 i 的数字结尾的子数组的最大积，则有 dp[i] = max(dp[i-1] * nums[i], nums[i])，由于只用到 dp[i-1], 可以优化到空间复杂度 O(1)
2. 需要注意的是，由于是求积，最大值可能是 负数 * 负数 的情况，因此需要记录下前 i-1 的最小值，因此最大值在 [maxp * nums[i], minp * nums[i], nums[i]] 中产生
3. res 记录全局的最大值 res = max(res, maxp)

### Find Minimum in Rotated Sorted Array
[Leetcode : 153. Find Minimum in Rotated Sorted Array (Medium)](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)

二分查找，找到左右两边的条件即可，注意 right = mid

### Find Minimum in Rotated Sorted Array II
[Leetcode : 154. Find Minimum in Rotated Sorted Array II (Hard)](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/description/)

判断 nums[mid] 与 nums[right] 的大小，有三种情况：
1. nums[mid] < nums[right], min 可能是 nums[mid] 也可能是左半部分，因此 right = mid
2. nums[mid] = numd[right], 无法判断，可能在左边也可能右边，因此 right -= 1
3. 其他，在有半部分，因此 left = mid + 1

### Intersection of Two Linked Lists
[Leetcode : 160. Intersection of Two Linked Lists (Easy)](https://leetcode.com/problems/intersection-of-two-linked-lists/description/)

直观思路是计算出两个链表的长度，得到差值 step，让较长的链表先走 step 不，然后两个链表一起走，相遇的点就是两个链表的交点。若某个链表已经走到底还没有相遇，则没有交点。时间复杂度 O(max(n,m))  
  
改进算法：若 A,B 有交点，设公共部分长度为 c，则 A 长度为 a+c， B 长度为 b+c， 则有 a+c+b = b+c+a。 当 A 走到底时让 A 从 headB 出发，当 B 走到底时让 B 从 headA 出发，若到最后两者都没有相遇的话，A 和 B 都为 None，退出循环。

### Find Peak Element
[Leetcode : 162. Find Peak Element (Medium)](https://leetcode.com/problems/find-peak-element/description/)

二分查找，当 nums[mid] < nums[mid+1], 峰值在右半部分，left = mid + 1；反之，峰值可能是 nums[mid] 也可能在左半部分，因此 right = mid

### Compare Version Numbers
[Leetcode : 165. Compare Version Numbers (Medium)](https://leetcode.com/problems/compare-version-numbers/description/)

注意二者的长度不同，遍历时选择长度更长的，当 i 超过某个 arr 的长度时，就把他的后面的数字置为 0，再继续比较

```python
def compareVersion(self, version1, version2):
    if version1 == version2:
        return 0
    v1, v2 = version1.split('.'), version2.split('.')
    for i in range(max(len(v1), len(v2))):
        num1 = int(v1[i]) if i < len(v1) else 0
        num2 = int(v2[i]) if i < len(v2) else 0
        if num1 > num2:
            return 1
        elif num1 < num2:
            return -1
    return 0
```

### Excel Sheet Column Title
[Leetcode : 168. Excel Sheet Column Title(Easy)](https://leetcode.com/problems/excel-sheet-column-title/description/)

十进制转二十六进制

```python
def convertToTitle(self, n):
    res = ''
    while n:
        res = chr((n-1)%26 + 65) + res # 由于没有 0，需要 n-1
        n = (n-1) // 26
    return res
```

### Excel Sheet Column Number
[Leetcode : 171. Excel Sheet Column Number (Easy)](https://leetcode.com/problems/excel-sheet-column-number/description/)

二十六进制转十进制

```python
def titleToNumber(self, s):
    sum = 0
    for char in s:
        sum = sum * 26 + ord(char) - 64
    return sum
```

### Dungeon Game
[Leetcode : 174. Dungeon Game (Hard)](https://leetcode.com/problems/dungeon-game/description/)

### Largest Number
[Leetcode : 179. Largest Number (Medium)](https://leetcode.com/problems/largest-number/description/)

```python
from functools import cmp_to_key
class Solution:
    def largestNumber(self, nums):
        nums = [str(n) for n in nums]
        nums.sort(key=cmp_to_key(lambda a, b: 1 if a+b<b+a else -1))
        return ''.join(nums) if nums[0] !='0' else '0'
```

### Repeated DNA Sequences
[Leetocde : 187. Repeated DNA Sequences (Medium)](https://leetcode.com/problems/repeated-dna-sequences/description/)

直接判断用 list 判断会超时，用 set 提高效率。
另外，可以用**位运算**做

### Rotate Array
[Leetcode : 189. Rotate Array(Easy)](https://leetcode.com/problems/rotate-array/description/)

若直接 nums[:] = nums[:len(nums)-k] + nums[len(nums)-k:], 在 OJ 中一定要 nums[:]，否则只是一个相同的叫 nums 的引用。  
要求时间复杂度为 O(1) 的话，可以通过三次反转实现，对于 [1,2,3,4,5,6,7], k=3  
[1,2,3,4] -> [4,3,2,1]; [5,6,7] -> [7,6,5]; [4,3,2,1,7,6,5] -> [5,6,7,1,2,3,4]

### Reverse Bits
[Leetcode : 190. Reverse Bits (Easy)](https://leetcode.com/problems/reverse-bits/description/)

```python
def reverseBits(self, n):
    res = 0
    for _ in range(32):
        res <<= 1
        if n & 1:
            res += 1
        n >>= 1
    return res
```

### Number of 1 Bits
[Leetcode : 191. Number of 1 Bits (Easy)](https://leetcode.com/problems/number-of-1-bits/description/)

与 1 进行 & 操作
```python
def hammingWeight(self, n):
    cnt = 0
    for i in range(32):
        if n & 1:
            cnt += 1
        n >>= 1
    return cnt
```

### Number of Islands
[Leetcode : 200. Number of Islands (Medium)](https://leetcode.com/problems/number-of-islands/description/)

矩阵搜索，每次遇到 1 的时候就开始往他的上下左右搜索，直到周围都是 0 为止，遍历过的 1 要变为 0；主函数每次遇到 1 都说明出现了一个新的 island

```python
def numIslands(self, grid):
    if not grid:
        return 0
    cnt = 0
    n = len(grid)
    m = len(grid[0])
    
    def dfs(i, j):
        if i >= n or i < 0 or j >= m or j < 0 or grid[i][j] == '0':
            return 
        grid[i][j] = '0'
        dfs(i-1, j)
        dfs(i+1, j)
        dfs(i, j-1)
        dfs(i, j+1)
                  
    for i in range(n):
        for j in range(m):
            if grid[i][j] == '1':
                dfs(i, j)
                cnt += 1
    return cnt
```

### Bitwise AND of Numbers Range
[Leetcode : 201. Bitwise AND of Numbers Range (Medium)](https://leetcode.com/problems/bitwise-and-of-numbers-range/description/)

直接遍历一遍按位 & 超时，无法通过

m-n 之间的所有数字按位与相当于是 m 和 n 左边的公共部分，后面肯定都是 0；先将 m 和 n 右移 cnt 位，直到两个数相等，再将 m 左移 cnt 位得到结果

```python
def rangeBitwiseAnd(self, m, n):
    cnt = 0
    while m != n:
        m >>= 1
        n >>= 1
        cnt += 1
    return m << cnt
```

### Count Primes
[Leetcode : 204. Count Primes (Easy)](https://leetcode.com/problems/count-primes/description/)

### Isomorphic Strings
[Leetcode : 205. Isomorphic Strings (Easy)](https://leetcode.com/problems/isomorphic-strings/description/)

字典记录 s[i] 为 key， t[i] 为 value，两种情况：  
1. 若 s[i] 在字典中， 若 t[i] != dic[s[i]] 不对应，则 return False
2. 若 s[i] 不在字典中，若 t[i] in dic.values()，说明已经有一个 key 对应了这个字符，不能有两个不同的 key 对应同一个字符，因此 return False；否则就把 s[i] 加到 dic 中

### Minimum Size Subarray Sum
[Leetcode : 209. Minimum Size Subarray Sum (Medium)](https://leetcode.com/problems/minimum-size-subarray-sum/description/)

双指针 left right 记录下子数组的起点和终点  
sum < s 时，right 移动； sum >= s 时， left 移动； 同时需要记录下最小的长度

```python
def minSubArrayLen(self, s, nums):
    if not nums or sum(nums) < s:
        return 0
    left = right = 0
    min_len = float('inf')
    sum_nums = 0
    while right < len(nums):
        while sum_nums < s and right < len(nums):
            sum_nums += nums[right]
            right += 1
        while sum_nums >= s:
            min_len = min(min_len, right-left) # 注意这个长度
            sum_nums -= nums[left]
            left += 1
    return min_len
```

### Kth Largest Element in an Array
[Leetcode : 215. Kth Largest Element in an Array (Medium)](https://leetcode.com/problems/kth-largest-element-in-an-array/description/)

二分查找 + 快速排序

```python
class Solution(object):
    def findKthLargest(self, nums, k):
        if k > len(nums) or k <= 0:
            return None
        left, right = 0, len(nums)-1
        while left <= right:
            mid = self.quick_sort(nums, left, right)
            if mid == len(nums) - k:
                return nums[mid]
            elif mid < len(nums) - k:
                left = mid + 1
            else:
                right = mid - 1
        
    def quick_sort(self, nums, left, right):
        key = nums[left]
        while left < right:
            while left < right and nums[right] >= key:
                right -= 1
            nums[left] = nums[right]
            while left < right and nums[left] <= key:
                left += 1
            nums[right] = nums[left]
        nums[left] = key
        return left
```

### Contains Duplicate II
[Leetcode : 219. Contains Duplicate II (Easy)](https://leetcode.com/problems/contains-duplicate-ii/description/)

用字典存储元素上一次出现的位置，当前元素在字典中的时候，比较两个小标的差是不是 <= k 

```python
def containsNearbyDuplicate(self, nums, k):
    dic = {}
    for i in range(len(nums)):
        if nums[i] in dic:
            if i - dic[nums[i]] <= k:
                return True
        dic[nums[i]] = i
    return False
```

### Maximal Square
[Leetcode : 221. Maximal Square (Medium)](https://leetcode.com/problems/maximal-square/description/)

用 dp[i][j] 存储以 [i, j] 为右下角的正方形的最大边长，则当 nums[i][j] == '0' 时，dp[i][j] = 0; nums[i][j] == '1' 时， dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1; 在这个过程中需记录下全局的最大边长。

```python
def maximalSquare(self, matrix):
    if not matrix:
        return 0
    n, m = len(matrix), len(matrix[0])
    dp = [[0 for j in range(m)] for i in range(n)]
    res = 0
    for i in range(n):
        dp[i][0] = int(matrix[i][0])
        res = max(res, dp[i][0])
    for j in range(m):
        dp[0][j] = int(matrix[0][j])
        res = max(res, dp[0][j])
    for i in range(1, n):
        for j in range(1, m):
            if matrix[i][j] == '1':
                dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1
                res = max(res, dp[i][j])
            else:
                dp[i][j] = 0
    return res*res
```

### Count Complete Tree Nodes
[Leetcode : 222. Count Complete Tree Nodes (Medium)](https://leetcode.com/problems/count-complete-tree-nodes/description/)

计算完全二叉树的节点数，不能直接遍历一遍。 利用左右子树的高度来计算，因为对于满二叉树的节点数为 2 ** height - 1

若左子树高等于右子树高，则左子树为满二叉树，节点数可以求出；右子树可能满也可能完全，则继续递归计算右子树
若左子树高大于右子树高，则右子树为满二叉树

**时间复杂度 O(logn * logn)**

```python
class Solution(object):
    def countNodes(self, root):
        if not root:
            return 0
        left_height = self.get_height(root.left)
        right_height = self.get_height(root.right)
        if left_height == right_height:
            return 2 ** left_height + self.countNodes(root.right)
        else:
            return 2 ** right_height + self.countNodes(root.left)
        
    def get_height(self, root):
        if not root:
            return 0
        return self.get_height(root.left) + 1 # 由于是完全二叉树，只需要返回左子树的树高
```

### Implement Stack using Queues
[Leetcode : 225. Implement Stack using Queues (Easy)](https://leetcode.com/problems/implement-stack-using-queues/description/)

### Implement Queue using Stacks
[Leetcode : 232. Implement Queue using Stacks (Easy)](https://leetcode.com/problems/implement-queue-using-stacks/description/)

### Rectangle Area
[Leetcode : 223. Rectangle Area (Medium)](https://leetcode.com/problems/rectangle-area/description/)

数学题，需要找到两个矩形的重叠部分，用右上角最小的减去左下角最大的，则可以得到重叠边长

```python
def computeArea(self, A, B, C, D, E, F, G, H):
    length = max(0, min(C, G)-max(A, E))
    width = max(0, min(D, H)-max(B,F))
    overlap = length * width
    return (C-A) * (D-B) + (G-E) * (H-F) - overlap
```

### Majority Element II
[Leetcode : 229. Majority Element II (Medium)](https://leetcode.com/problems/majority-element-ii/description/)

要求时间复杂度为 O(n) 空间 O(1)，用摩尔投票法，初始化两个候选者为 None，每次遍历只能进行一种操作，不然选不出来

```python
def majorityElement(self, nums):
    can1, can2 = None, None
    cnt1, cnt2 = 0, 0 
    for i in range(len(nums)):
        if nums[i] == can1:
            cnt1 += 1
        elif nums[i] == can2:
            cnt2 += 1
        elif cnt1 == 0:
            can1 = nums[i]
            cnt1 = 1
        elif cnt2 == 0:
            can2 = nums[i]
            cnt2 = 1
        else:
            cnt1 -= 1
            cnt2 -= 1
    res = [n for n in (can1, can2) if nums.count(n) > len(nums)//3] # 最后需要判断是否真的符合条件
    return res
```

### Lowest Common Ancestor of a Binary Search Tree
[Leetcode : 235. Lowest Common Ancestor of a Binary Search Tree (Easy)](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/)

看到二叉查找树 BST ，肯定要用到其左子树比它小，右子树比它大的特性。

```python
def lowestCommonAncestor(self, root, p, q):
    if root.val > p.val and root.val > q.val:
        return self.lowestCommonAncestor(root.left, p, q)
    elif root.val < p.val and root.val < q.val:
        return self.lowestCommonAncestor(root.right, p, q)
    else: # 介于两者之间，或者其他情况，必须要写在最后面
        return root
```

### Lowest Common Ancestor of a Binary Tree
[Leetcode : 236. Lowest Common Ancestor of a Binary Tree (Medium) ](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/)

找到 p 和 q 在左子树还是右子树

```python
def lowestCommonAncestor(self, root, p, q):
    if not root or root == p or root == q:
        return root
    left = self.lowestCommonAncestor(root.left, p, q)
    right = self.lowestCommonAncestor(root.right, p, q)
    if left and right:
        return root
    elif left:
        return left
    else:
        return right
```

### Delete Node in a Linked List
[Leetcode : 237. Delete Node in a Linked List (Easy)](#https://leetcode.com/problems/delete-node-in-a-linked-list/description/)

删除节点 node，注意在该题中值只给了一个节点 node，没有给整个链表，因此可以考虑用下一个节点来操作，把下一个节点的值赋给 node，再删除下一个节点，就相当于删除了 node 节点。

```python
def deleteNode(self, node):
    node.val = node.next.val
    node.next = node.next.next
```

### Product of Array Except Self
[Leetcode : 238. Product of Array Except Self (Medium)](https://leetcode.com/problems/product-of-array-except-self/description/)

理清相乘的过程，写下每次的数字，从左往右乘一遍，再从右往左乘一遍，第一个数是不乘的

```python
def productExceptSelf(self, nums):
    res = []
    tmp = 1
    for i in range(len(nums)):
        res.append(tmp)
        tmp = tmp * nums[i]
    tmp = 1
    for i in range(len(nums)-1, -1, -1):
        res[i] *= tmp
        tmp = tmp * nums[i]
    return res
```

### Perfect Squares
[Leetcode : 279. Perfect Squares (Medium)](https://leetcode.com/problems/perfect-squares/description/)

求最少的完全平方数组成，动态规划，用 dp[i] 存储以数字 i 的最少完全平方数组成。  
比如 13 = 1 * 1 + 12， 2 * 2 + 9， 3 * 3 + 4 , 那么dp[13] = min(dp[12]+1, dp[9]+1, dp[4]+1)

```python
def numSquares(self, n):
    dp = [float('inf')] * (n+1)
    dp[0] = 0
    for i in range(1, n+1):
        for j in range(1, int(math.sqrt(n)+1)):
            dp[i] = min(dp[i], dp[i-j*j]+1)
    return dp[-1]
```

### Find the Duplicate Number
[Leetcode : 287. Find the Duplicate Number (Medium)](https://leetcode.com/problems/find-the-duplicate-number/description/)

要求不能修改数组，时间 O(nlogn), 空间 O(1)，因此不能排序，不能用 dict 存储数字及计数。

二分查找，对于 nums，里面的数字是从 1 到 len(nums)-1，这个是有序的，因此为这里面的数字进行二分查找，然后遍历一遍数组，计算小于等于 mid 的个数，若 cnt > mid 大，则说明重复数字要么是 mid 要么比 mid 更小，也就是在 1-mid 之间。

```python
def findDuplicate(self, nums):
    left, right = 1, len(nums)-1
    while left < right:
        mid = left + (right-left) // 2
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

### Longest Increasing Subsequence
[Leetcode : 300. Longest Increasing Subsequence (Medium)](https://leetcode.com/problems/longest-increasing-subsequence/description/)

求最长递增子序列，用 dp[i] 存储到下标为 i 的数的最长递增子序列

```python
def lengthOfLIS(self, nums):
    if not nums:
        return 0
    dp = [0] * len(nums)
    for i in range(len(nums)):
        dp_max = 1
        for j in range(i):
            if nums[i] > nums[j]:
                dp_max = max(dp_max, dp[j] + 1)
        dp[i] = dp_max
    return max(dp)
```

### Coin Change
[Leetcode : 322. Coin Change (Medium)](https://leetcode.com/problems/coin-change/description/)

**完全背包，背包问题需要在复习一遍！！！**

```python
def coinChange(self, coins, amount):
    INF = float('inf')
    dp = [0] + [INF] * amount
    for i in range(len(coins)):
        for j in range(coins[i], amount+1):
            if dp[j-coins[i]] != INF:
                dp[j] = min(dp[j], dp[j-coins[i]]+1)
    return dp[amount] if dp[amount] != INF else -1
```

328 之后

### Min Cost Climbing Stairs
[Leetcode : 746. Min Cost Climbing Stairs (Easy)](https://leetcode.com/problems/min-cost-climbing-stairs/description/)

用 dp[i] 存储到第 i 层的时候的最小花费，则他可能从 i-1 或 i-2 层跳上来，但不用加上 cost[i] 的花费  
dp[i] = min(dp[i-1]+cost[i-1], dp[i-2]+cost[i-2])  

dp 的长度应该 cost 更长 1，因为需要跳到顶部，而不是 len(cost)-1 这层。

```python
def minCostClimbingStairs(self, cost):
    pre1 = pre2 = 0
    dp = 0
    for i in range(2, len(cost)+1):
        dp = min(pre1+cost[i-1], pre2+cost[i-2])
        pre2 = pre1
        pre1 = dp
    return dp
```
