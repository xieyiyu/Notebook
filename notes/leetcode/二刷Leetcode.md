# 二刷 Leetcode
## 提高效率！！！

<!-- GFM-TOC -->
* [2. Add Two Numbers](#add-two-numbers)
* [3. Longest Substring Without Repeating Characters](#longest-substring-without-repeating-characters)
* [** 4. Median of Two Sorted Arrays](#median-of-two-sorted-arrays)
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
* [38. Count and Say](#count-and-say)
* [** 43. Multiply Strings](#multiply-strings)
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
<!-- GFM-TOC -->

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
        if carry >= 10:
            cur.next = ListNode(carry-10)
            carry = 1
        else:
            cur.next = ListNode(carry)
            carry = 0
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
[Leetocde : 73. Set Matrix Zeroes (Medium)](https://leetcode.com/problems/set-matrix-zeroes/description/)

要求空间复杂度为 O(1)，可以将需要置为 0 的行号和列号记录在第 0 行和第 1 列，并记下第 0 列的原始数据是否本来就含有 0。

### Search a 2D Matrix
[Leetocde : 74. Search a 2D Matrix (Medium)](https://leetcode.com/problems/search-a-2d-matrix/description/)

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
[Leetcdoe : 112. Path Sum (Easy)](https://leetcode.com/problems/path-sum/description/)

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