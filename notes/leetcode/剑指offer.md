<!-- GFM-TOC -->
* [二维数组中的查找](#二维数组中的查找)
* [** 替换空格](#替换空格)
* [从尾到头打印链表](#从尾到头打印链表)
* [重建二叉树](#重建二叉树)
* [** 用两个栈实现队列](#用两个栈实现队列)
* [** 旋转数组的最小数字](#旋转数组的最小数字)
* [** 变态跳台阶](#变态跳台阶)
* [矩形覆盖](#矩形覆盖)
* [** 二进制中1的个数](#二进制中1的个数)
* [数值的整数次方](#数值的整数次方)
* [在O(1)时间删除链表节点](#在O-1-时间删除链表节点)
* [** 调整数组顺序使奇数位于偶数前面](#调整数组顺序使奇数位于偶数前面)
* [链表中倒数第 k 个结点](#链表中倒数第-k-个结点)
* [合并两个排序的链表](#合并两个排序的链表)
* [** 树的子结构](#树的子结构)
* [二叉树镜像](#二叉树镜像)
* [顺时针打印矩阵](#顺时针打印矩阵)
* [包含min函数的栈](#包含min函数的栈)
* [** 栈的压入、弹出序列](#栈的压入-弹出序列)
* [** 二叉搜索树的后序遍历序列](#二叉搜索树的后序遍历序列)
* [二叉树中和为某一值的路径](#二叉树中和为某一值的路径)
* [** 复杂链表的复制](#复杂链表的复制)
* [** Medium. 二叉搜索树与双向链表](#二叉搜索树与双向链表)
* [字符串的排列](#字符串的排列)
* [数组中出现次数超过一半的数字](#数组中出现次数超过一半的数字)
* [** 最小的K个数](#最小的K个数)
* [** 连续子数组的最大和](#连续子数组的最大和)
* [** Hard. 233. 整数中1出现的次数](#整数中1出现的次数)
* [** Medium. 179. 把数组排成最小的数](#把数组排成最小的数)
* [** 丑数](#丑数)
* [** 数组中的逆序对](#数组中的逆序对)
* [** 数字在排序数组中出现的次数](#数字在排序数组中出现的次数)
* [平衡二叉树](#平衡二叉树)
* [** 数组中只出现一次的数字](#数组中只出现一次的数字)
* [和为S的连续正数序列](#和为S的连续正数序列)
* [和为S的两个数字](#和为S的两个数字)
* [左旋转字符串](#左旋转字符串)
* [翻转单词顺序列](#翻转单词顺序列)
* [扑克牌顺子](#扑克牌顺子)
* [** 圆圈中最后剩下的数](#圆圈中最后剩下的数)
* [求1+2+3+...+n](#求1+2+3+...+n)
* [**python中负数位移问题看不懂** 不用加减乘除做加法](#不用加减乘除做加法)
* [把字符串转换成整数](#把字符串转换成整数)
* [数组中重复的数字](#数组中重复的数字)
* [构建乘积数组](#构建乘积数组)
* [** Hard. 10. 正则表达式匹配](#正则表达式匹配)
* [表示数值的字符串](#表示数值的字符串)
* [字符流中第一个不重复的字符](#字符流中第一个不重复的字符)
* [链表中环的入口结点](#链表中环的入口结点)
* [** 删除链表中重复的结点](#删除链表中重复的结点)
* [** 二叉树的下一个结点](#二叉树的下一个结点)
* [** 序列化二叉树](#序列化二叉树)
* [二叉搜索树的第k个结点](#二叉搜索树的第k个结点)
* [**如何用堆求解？** 数据流中的中位数](#数据流中的中位数)
* [** 滑动窗口的最大值](#滑动窗口的最大值)
* [** 矩阵中的路径](#矩阵中的路径)
* [机器人的运动范围](#机器人的运动范围)
<!-- GFM-TOC -->

【总结】
Easy 会做：
1. 二维数组中的查找: target 与右上角数字对比来缩小范围，时间 O(n+m)，空间 O(1)
2. 重建二叉树：根据前序和中序构建，找到前序中根节点的位置将数组分为左右两部分，再递归，递归深度 O(logn)
3. 斐波那契数列： f(n) = f(n-1) + f(n-2)，f(0) = 0, f(1) = 1, f(2) = 1 注意初始值
4. 跳台阶： f(n) = f(n-1) + f(n-2)，f(1) = 1, f(2) = 2，与斐波拉切数列的初始值不同
5. 链表中倒数第k个结点： 快慢指针法，fast 先走 k 步，然后 fast 和 slow 同步走， 时间 O(n), 空间 O(1)
6. 反转链表： 设置 pre = None，从 cur = head 以此反转， 时间 O(n), 空间 O(1)
7. 二叉树的镜像： left 和 right 互换，再递归互换 left.left 和 right.right， 以及 left.right 和 right.left
8. 顺时针打印矩阵： 设置四个方向依次打印，注意每次打印都要判断 res 的长度是否已经超过矩阵大小
9. 从上往下打印二叉树： 层次遍历，cur 记录当前层的节点，tmp 记录下一层节点
10. 二叉树中和为某一值的路径： 回溯，注意递归结束的条件
11. 字符串的排列： 回溯，注意递归结束的条件，注意字符串拼接方法
12. 数组中出现次数超过一半的数字： 摩尔投票法，同加异减规则，当 cnt = 0 时，就重置要计数的数字并将 cnt = 1, 一次遍历完成，时间 O(n)，空间 O(1)，需要注意的是最后一定要检查得到的数字是否符合条件
13. 两个链表的第一个公共结点： 画图，当 p1 走到尾时就从 p2 的头部开始走，p2 走到尾时就从 p1 的头部开始走，时间 O(n+m)
14. 二叉树的深度： 递归，返回左右子树较大的深度 + 1
15. 平衡二叉树： 递归，左右子树的深度差 <= 1
16. 对称的二叉树： 递归，考虑清楚几种情况
17. 按之字形顺序打印二叉树： 层次遍历分奇数行和偶数行打印
18. 把二叉树打印成多行： 层次遍历
19. 二叉搜索树的第k个结点： 中序遍历

Medium 有思路，还需要再加深一遍：
1. 从尾到头打印链表： 自己是直接按顺序追加到 res 中，再 return res[::-1]，剑指 offer 是利用栈的后进先出特性来解决，用 stack 存储链表从头到尾的顺序，遍历完整个链表后，再将 stack 中的元素 pop 到 res 中

2. 用两个栈实现队列： 用 stack1 实现进队列，直接 append 元素到 stack1 中； stack2 实现出队列，首先要判断 stack2 中的是否有元素，stack2 为空，则把 stack1 中的元素全部压入 stack2 中，stack2 非空，则直接弹出 stack2 中的最后一个元素（栈顶）

3. 旋转数组的最小数字： 分情况考虑，因为从左边算过来后面肯定是有有一部分有序的，因此要拿 mid 和 left 进行比较，当 nums[mid] <= nums[left] 时，最小数字在左边， right = mid； 注意考虑特殊情况，数组没有旋转的情况，nums[mid] == nums[left] == nums[right] 的情况

4. 变态跳台阶： 用 dp[i] 存储到第 i 阶时的跳法，dp[i+1] = sum(dp)

5. 矩形覆盖： f(n) = f(n-1) + f(n-2)

6. 二进制中1的个数

7. 数值的整数次方
8. 调整数组顺序使奇数位于偶数前面
9. 合并两个排序的链表
10. 包含min函数的栈
11. 栈的压入、弹出序列
12. 二叉搜索树的后序遍历序列
13. 连续子数组的最大和
14. 第一个只出现一次的字符位置
15. 左旋转字符串
16. 翻转单词顺序列
17. 把字符串转换成整数
18. 数组中重复的数字
19. 字符流中第一个不重复的字符
20. 链表中环的入口结点
21. 删除链表中重复的结点
22. 数据流中的中位数
23. 矩阵中的路径

Hard 不太会：
1. 替换空格
2. 树的子结构
3. 复杂链表的复制
4. 最小的K个数(最大堆解法)
5. 丑数
6. 数字在排序数组中出现的次数
7. 和为S的连续正数序列
8. 和为S的两个数字
9. 扑克牌顺子
10. 孩子们的游戏(圆圈中最后剩下的数)
11. 求1+2+3+...+n
12. 不用加减乘除做加法
13. 构建乘积数组
14. 二叉树的下一个结点
15. 机器人的运动范围

Very hard 完全不会：
1. 二叉搜索树与双向链表
2. 整数中1出现的次数
3. 把数组排成最小的数
4. 数组中的逆序对
5. 正则表达式匹配
6. 表示数值的字符串
7. 序列化二叉树
8. 滑动窗口的最大值

#### 二维数组中的查找
在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

```python
# -*- coding:utf-8 -*-
class Solution:
    # array 二维列表
    def Find(self, target, array):
        # write code here
        if not array:
            return False
        i = 0
        j = len(array[0]) - 1
        while i <= len(array)-1 and j >= 0:
            if target == array[i][j]:
                return True
            elif target > array[i][j]:
                i += 1
            else:
                j -= 1
        return False
```

### 字符串
#### 替换空格
请实现一个函数，将一个字符串中的每个空格替换成 "%20"。例如，当字符串为 We Are Happy,则经过替换之后的字符串为 We%20Are%20Happy。

- 问题1： 是在当前字符串上替换，还是可以开辟一个新的字符串做替换？
- 问题2： 在当前字符串上替换，怎么做才能更有效率？
从前往后替换的话，后面的字符要移动多次，效率低，时间复杂度为 O(n<sup>2</sup>); 而从后往前替换，先计算出需要增加多少空间，再从后往前移动，每个字符只需移动一次，时间复杂度为 O(n)。

从后往前遍历是为了在改变 p2 所指的

思路： 用两个指针，p1 指向原始字符串的末尾，p2 指向替换后的字符串的末尾； 当 p1 指向空格时，就将其替换为 %20，同时 p1 向前移动一格，p2 向前移动三格。

1. 计算原字符串长度，并统计空格数量
2. 新字符串长度 = 原字符串长度 + 空格数量 * 2
3. 在新字符串数组上，从后往前编辑，通过两个指针移动并复制

```python
# -*- coding:utf-8 -*-
class Solution:
    # s 源字符串
    def replaceSpace(self, s):
        # write code here
        s = list(s)
        p1 = len(s) - 1
        cnt = 0
        for c in s:
            if c == " ":
                cnt += 1
        s = s + [None] * (cnt*2)
        p2 = len(s) - 1
        while p1 >= 0:
            if s[p1] == " ":
                s[p2] = '0'
                s[p2-1] = '2'
                s[p2-2] = '%'
                p2 -= 3
            else:
                s[p2] = s[p1]
                p2 -= 1
            p1 -= 1
        return ''.join(s)
```

### 链表
链表时一种动态数据结构，创建链表时不需要知道链表长度，当插入一个结点时，只需要为新结点分配内存。链表中没有闲置的内存，空间效率高。

#### 从尾到头打印链表
也就是要求后进先出，使用栈来实现。

```python
def printListFromTailToHead(self, listNode):
    # write code here
    stack = []
    while listNode:
        stack.append(listNode.val)
        listNode = listNode.next
    res = []
    while stack:
        res.append(stack.pop())
    return res
```

### 树
#### 重建二叉树
通过前序遍历和中序遍历构建二叉树

```python
class Solution:
    # 返回构造的TreeNode根节点
    def reConstructBinaryTree(self, pre, tin):
        # write code here
        if not pre or not tin:
            return 
        root = TreeNode(pre[0])
        i = tin.index(pre[0])
        root.left = self.reConstructBinaryTree(pre[1:i+1], tin[:i])
        root.right = self.reConstructBinaryTree(pre[i+1:],tin[i+1:])
        return root
```

### 栈和队列

#### 用两个栈实现队列
用两个栈来实现一个队列，完成队列的 Push 和 Pop 操作。 队列中的元素为 int 类型。

栈是先进后出，队列是先进先出，因此添加元素用 stack1，删除元素需要先将 stack1 中的元素全部压入 stack2，再 stack2 从栈顶开始删除。 删除的时候先删除的是队头，也就是栈底。

删除时需要先考虑 stack2 是否为空

注意 stack2 为空时，需要把 stack1 压入 stack2， stack2 不为空时，可以直接弹出元素。

```python
class Solution:
    def __init__(self):
        self.stack1 = []
        self.stack2 = []
    
    def push(self, node):
        self.stack1.append(node)
        
    def pop(self):
        # return xx
        if not self.stack2:
            while self.stack1:
                self.stack2.append(self.stack1.pop())
        return self.stack2.pop()
```

#### 用两个队列实现栈
进栈： 元素插入 queue1
出栈： 假设 queue1 = [a, b, c]，现在要出栈 c(先进后出)，但是队列是先进先出，只能从队列的头部进行删除，因此把 a 和 b 从 queue1 中删除并压入 queue2，则 queue1 = [c], queue2 = [a, b], 当 queue1 只剩一个元素时，出栈， queue1 为空。
若要继续出栈 b， 则再将 a 从 queue2 中删除并压入 queue1，然后 queue2 出栈。
为了减少判断，在出栈前，可以将 queue1 和 queue2 进行交换，则每次 queue1 和 queue2 的逻辑操作相同，但要注意出栈的会变成 queue2。

出栈的时间复杂度 O(n<sup>2</sup>)

```python
class Solution:
	def __init__(self):
		self.queue1 = []
		self.queue2 = []

	def push(self, node):
		self.queue1.append(node)

	def pop(self):
		if not self.queue1:
			return None
		while len(self.queue1) > 1:
			self.queue2.append(self.queue1.pop())
		self.queue1, self.queue2 = self.queue2, self.queue1 # 为了下一次更好的交换
		return self.queue2.pop()
```

### 查找和排序
#### 旋转数组的最小数字
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个非减排序的数组的一个旋转，输出旋转数组的最小元素。 

思路： 旋转后的数组可以看成两个排序的子数组，且前面的子数组的元素都大于等于后面的，最小的元素刚好是两个子数组的分界。
用两个指针 left 和 right 分别指向左右，有三种情况：
1. nums[mid] >= nums[left], 左边有序，由于左边子数组的元素都会大于等于右边的，也就是最小元素在右边子数组中，有可能是 mid，所以 left = mid
2. nums[mid] <= nums[left]， right = mid
3. 考虑特殊情况，当出现很多相同元素，即 nums[mid] == nums[left] == nums[right] 时，只能顺序查找，找到 nums[mid] < nums[left] 即是最小元素

循环终止时，left 指向最大元素，right 指向最小元素，两者的 index 相差 1 
 
旋转后，第一个元素肯定是大于或等于最后一个元素的，如果出现第一个元素小于最后一个元素，说明数组没有旋转，第一个元素就是最小的数字。

```python
# -*- coding:utf-8 -*-
class Solution:
    def minNumberInRotateArray(self, rotateArray):
        if not rotateArray:
            return 0
        if rotateArray[0] < rotateArray[-1]:
            return rotateArray[0] # 
        left = 0
        right = len(rotateArray) - 1
        while left < right - 1:
            mid = left + (right-left) // 2
            if rotateArray[mid] == rotateArray[left] and rotateArray[mid] == rotateArray[right]:
                for i in range(left+1, right+1):
                    if rotateArray[i] < rotateArray[mid]:
                        return rotateArray[i]
            elif rotateArray[mid] >= rotateArray[left]:
                left = mid
            else:
                right = mid
        return rotateArray[right]
```

### 变态跳台阶
一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

f(n) = 1 + f(n-1) + f(n-2) + ... + f(2) + f(1)

由数学归纳法可得 f(n) = 2 ** (n-1)

```python
class Solution:
    def jumpFloorII(self, number):
        # write code here
        if not number: return 0
        dp = [1,1]
        for i in range(2, number+1):
            dp.append(sum(dp))
        return dp[-1]
```

### 矩形覆盖
我们可以用2 * 1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2 * 1的小矩形无重叠地覆盖一个2 * n的大矩形，总共有多少种方法？

思路： 仍然是斐波拉切数列，最后一个小矩形竖着放，有 f(n-1) 种放法，横着放，则下面必须再横着放一个，则有 f (n-2) 种放法，f(n) = f(n-1) + f(n-2)

## 位运算
### 二进制中1的个数
输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。

如果没有负数，可以如下解法，将该整数和 1 相与，得到的结果是 1，则最后一位是 1，然后再将这个整数右移一位直到整数变为 0：
```python
def NumberOf1(self, n):
    cnt = 0
    while n:
        if n & 1:
            cnt += 1
        n >>= 1
    return cnt
```

思路： 从 n 的二进制的最右边与 1 进行按位与，正数可以得到正确结果，但负数右移时在最高位补的是 1，而与 1 按位与的话，会全部变成 1 而进入死循环。 因此可以将数字 1 左移，再和 n 进行按位与。

注意： Python2 的 int 类型有 32 位和 64 位的区分，在 Python3 中，当长度超过 32 位或 64 位之后，Python3 会自动将其转为长整型，为 long 类型，长整型理论上没有长度限制，因此必须要加上循环 32 次的限制，不然 flag 左移 32 次之后并不会变成 0。

在 java 和 c 中会指明是 int 类型，但 python 类型模糊，因此需要注意自己加上限制条件。

```python
class Solution:
    def NumberOf1(self, n):
        # write code here
        cnt = 0
        flag = 1
        for i in range(32):
            if n & flag:
                cnt += 1
            flag <<= 1
        return cnt
```

更优的思路： 将一个整数减去 1，相当于把这个整数最右边的一个 1 变成 0，这个 1 后面的 0 都变成 1，而前面的不变。再和原整数做按位与运算，原整数就会少了一个 1，因此一个整数有多少个 1， 就可以进行多少次这样的运算，直到该整数变为 0.

比如二进制 1100，减去 1 后，变为 1011，两者相与得到 1000； 1000 减去 1 为 0111，两者相与得到 0000，整数变为 0 ，总共进行了两次这样的操作，因为原整数有两个 1。

如果只是 while n，在 n < 0 时会死循环，不会变成 0，python要使用n & 0xffffffff得到一个数的补码

```python
def NumberOf1(self, n):
    cnt = 0
    while n:
        n = (n-1) & n & 0xffffffff # 负数在进行位运算的时候记得和 Oxffffffff 相与
        cnt += 1
    return cnt
```

参考： https://blog.csdn.net/u010005281/article/details/79851154
https://www.cnblogs.com/shengguorui/p/10907382.html

1. 用一条语句判断一个整数是不是 2 的整数次方：
```python
if (n-1)&n == 0：
	return True
```

2. 输入两个整数 m 和 n，计算需要改变 m 的二进制表示的多少位才能得到 n：
先异或，再计算异或得到的二进制中的 1 的个数。


### 数值的整数次方
给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

思路一： 注意考虑各种边界条件，0、1、正、负的情况，这样算时间复杂度为 O(n)

```python
class Solution:
    def Power(self, base, exponent):
        # write code here
        if base == 0:
            return 0
        if exponent == 0 or base == 1:
            return 1
        res = 1
        for i in range(abs(exponent)):
            res = base * res
        return res if exponent > 0 else 1/res
```

优化，使用快速幂算法：
https://blog.csdn.net/hkdgjqr/article/details/5381028

思路二：全面又高效的解法，将时间复杂度降低到 O(logn)
当幂 n 为偶数时， a^n = a^(n/2)^2
当幂 n 为奇数时， a^n = a^((n-1)/2)^2 * a

因此可以递归计算，将幂不断除 2

```python
# -*- coding:utf-8 -*-
class Solution:
    def Power(self, base, exponent):
        # write code here
        if exponent == 0:
            return 1
        if exponent == 1:
            return base
        if exponent == -1:
            return 1/base 
        res = self.Power(base, exponent>>1) # 用右移运算符代替除 2，效率高
        res *= res
        if exponent & 1 == 1: # 用位运算代替取模(exponent%2) 来判断是奇数还是偶数，效率高
            res *= base
        return res
```

### 在O(1)时间删除链表节点
需要考虑多方面：是否头部和尾部(必须顺序查找)，只有一个节点，节点是否存在于该链表中

### 调整数组顺序使奇数位于偶数前面
输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

思路一： 开辟新数组，用空间换时间，时间复杂度 O(n)，空间复杂度 O(n)
```python
def reOrderArray(self, array):
        # write code here
        odd = [i for i in array if i%2==1]
        even = [i for i in array if i%2==0]
        return odd + even
```

思路二： 类似于排序，需要采用稳定排序的思路  

使用冒泡排序的思想，i 从前往后遍历， j 从后往前遍历，当遇到**前偶后奇**的情况，就交换
```python
def reOrderArray(self, array):
        # write code here
        for i in range(len(array)):
            for j in range(len(array)-1, i, -1):
                if array[j-1] % 2 == 0 and array[j] % 2 == 1:
                    array[j], array[j-1] = array[j-1], array[j]
        return array
```

如果题目不要求保证数字的相对位置不变，只要把奇数排在前面，偶数排在后面呢？

只需要设置两个指针，i 指向第一个元素， j 指向最后一个元素，i 向前移动直到指向偶数，j 向后移动直到指向奇数； 当 i 指向偶数，j 指向奇数，就两者交换，时间复杂度为 O(n)

```python
def reOrderArray(self, array):
    i, j = 0, len(array)-1
    while i < j:
        while i < j and array[i] % 2 == 1:
            i += 1
        while i < j and array[j] % 2 == 0:
            j -= 1
        if i < j:
            array[i], array[j] = array[j], array[i]
    return array
```

如果把题目改为将数组中的数按负数和非负数分为两部分，或者分为能被3整除和不能被3整除两部分，要这样具有扩展性的话，只需要把 reOrderArray 中的 while i < j and array[i] % 2 == 1 的后面这部分用一个单独的函数来判断数字是否符合要求，因此判断框架为：

```python
def reOrderArray(array):
    i, j = 0, len(array)-1
    while i < j:
        while i < j and function(array[i]):
            i += 1
        while i < j and function(array[j]):
            j -= 1
        if i < j:
            array[i], array[j] = array[j], array[i]
    return array

def function(x):
    if 判断条件:
        return True
    else:
        return False
```

### 链表中倒数第 k 个结点
输入一个链表，输出该链表中倒数第k个结点。

思路： 倒数第 k 个结点，也就是第 n-k+1 个结点，n 为链表长度，若要在 O(n) 时间解决，则用快慢指针法，fast 先走 k 步，然后 fast 和 slow 同步走，当 fast 走到最后时， slow 指向的就是倒数第 k 个结点。

要注意 k 比链表长度更大的情况，此时 fast 已经走到最后，但是 k != 0，直接返回； 还有链表为空的情况，fast 就没有 next，因此在最开始就需要考虑链表是否为空的情况。
```python
class Solution:
    def FindKthToTail(self, head, k):
        # write code here
        if not head:
            return None
        fast = slow = head
        while k:
            fast = fast.next
            k -= 1
            if not fast and k != 0:
                return None
        while fast:
            fast = fast.next
            slow = slow.next
        return slow
```

### 合并两个排序的链表
输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。

```python
def Merge(self, pHead1, pHead2):
    if not pHead1 and not pHead2:
        return None
    dummy = ListNode(0)
    p = dummy
    while pHead1 and pHead2:
        if pHead1.val <= pHead2.val:
            p.next = pHead1
            pHead1 = pHead1.next
        else:
            p.next = pHead2
            pHead2 = pHead2.next
        p = p.next
    if not pHead1:
        p.next = pHead2
    if not pHead2:
        p.next = pHead1
    return dummy.next
```

### 树的子结构
输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）

思路： 首先需要在 A 中找到一个与 B 的根节点的值相同的结点，再从 A 的该节点与 B 进行比较，判断 B 是否是其子结构，此时可以构造一个函数 isSubtree 来判断 B 是否是 A 的子结构。 如果没找到，则继续往 A 的左子树和右子树找。

注意： 找到第一个相同值的结点后，不能直接 return isSubtree 的结果，因为可能只有根节点相同，左子树和右子树并不相同，则会返回 False，因此可以用一个变量 res 记录下这次的结果，如果是 False，则继续往 A 的左子树找，如果再是 False，再往 A 的右子树找。

```python
class Solution:
    def HasSubtree(self, pRoot1, pRoot2):
        # write code here
        if not pRoot1 or not pRoot2:
            return False
        res = False
        if pRoot1.val == pRoot2.val:
            res = self.isSubtree(pRoot1, pRoot2)
        if not res:
            res = self.HasSubtree(pRoot1.left, pRoot2)
        if not res:
            res = self.HasSubtree(pRoot1.right,pRoot2)
        return res
            
    def isSubtree(self, pRoot1, pRoot2):
        if not pRoot2:
            return True
        if not pRoot1 and pRoot2: # A没有B还有
            return False
        if pRoot1.val != pRoot2.val: # 值不同
            return False
        return self.isSubtree(pRoot1.left, pRoot2.left) and self.isSubtree(pRoot1.right, pRoot2.right)
```
### 二叉树镜像
操作给定的二叉树，将其变换为源二叉树的镜像。

思路： 递归交换结点的左右子树即可。

```python
class Solution:
    # 返回镜像树的根节点
    def Mirror(self, root):
        # write code here
        if not root:
            return root
        root.left, root.right = root.right, root.left
        self.Mirror(root.left)
        self.Mirror(root.right)
        return root
```

### 顺时针打印矩阵
输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，如果输入如下4 X 4矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.

思路： 设置四个方向进行打印，向右，向下，向左，向上，但是必须要注意循环结束的终止条件。 首先第一层需要满足 left <= right and up <= down，其次需要分析每一次打印元素的前提条件，res 的长度必须小于矩阵的大小的时候，才打印。 

若没有 if len(res) < size 这个条件，就可能会出现重复打印的情况。比如只有一列的矩阵，[[1],[2],[3],[4],[5]]
1. 首先 go right， res = [1]
2. 然后 go down ，res = [1,2,3,4,5]
3. 不会 go left，因此此时 left = 0, right = -1
4. 此时 up = 1，down = 3，会继续 go up，res = [1,2,3,4,5,4,3,2], 最后循环终止。 

这道题最重要的是： 确定循环终止条件， 确定打印的终止条件。

```python
class Solution:
    # matrix类型为二维列表，需要返回列表
    def printMatrix(self, matrix):
        # write code here
        if not matrix:
            return []
        left = 0
        right = len(matrix[0])-1
        up = 0
        down = len(matrix)-1
        size = len(matrix) * len(matrix[0]) 
        res = []
        while left <= right and up <= down:
            # go right
            for j in range(left, right+1):
                if len(res) < size:
                    res.append(matrix[up][j])
            up += 1
            # go down
            for i in range(up, down+1):
                if len(res) < size:
                    res.append(matrix[i][right])
            right -= 1
            # go left
            for j in range(right, left-1, -1):
                if len(res) <  size:
                    res.append(matrix[down][j])
            down -= 1
            # go up
            for i in range(down, up-1, -1):
                if len(res) < size:
                    res.append(matrix[i][left])
            left += 1
        return res
```

### 包含min函数的栈
定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。

思路： 要求时间复杂度为 O(1), 因此需要一次得到最小值，因此要考虑用空间换时间。

不能在元素入栈的时候就对元素进行排序，这样的话就无法保证出栈的是最后入栈的那个元素。

考虑使用一个辅助栈 min_stack，用来存储当前的最小值，每次都把当前的最小值压入 min_stack 中。 当 stack 需要出栈时，辅助栈中也需要同步出栈，这样就能保证若出栈的是最小值，那么辅助栈中就不能再保存最小值，然后就到了次小值。

重点： 用辅助栈保存当前最小值，并使两个栈大小相同，可以同步出栈

```python
class Solution:
    def __init__(self):
        self.stack = []
        self.min_stack = []
    def push(self, node):
        self.stack.append(node)
        if not self.min_stack or node <= self.min_stack[-1]:
            self.min_stack.append(node)
        else:
            self.min_stack.append(self.min_stack[-1])
    def pop(self):
        self.min_stack.pop()
        self.stack.pop()
    def top(self):
        return self.stack[-1]
    def min(self):
        return self.min_stack[-1]
```

### 栈的压入、弹出序列
输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）

思路： 用一个辅助栈，把输入的第一个序列的元素依次压入栈，再按照第二个序列的顺序依次出栈。 

```python
class Solution:
    def IsPopOrder(self, pushV, popV):
        # write code here
        stack = []
        i = 0
        while i < len(pushV):
            stack.append(pushV[i])
            while popV and stack and popV[0] == stack[-1]: # 注意这里必须先判断 popV 和 stack 是否为空，否则会出现溢出
                stack.pop()
                popV.pop(0)
            i += 1
        return True if not stack else False
```

### 二叉搜索树的后序遍历序列
输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则输出Yes,否则输出No。假设输入的数组的任意两个数字都互不相同。

思路： 对于 BST，后序遍历的最后一个数字是根节点，BST 左子树的所有节点都比根节点小，右子树的所有节点都比根节点大，因此对前面的元素与根节点大小比较，可以把该序列分成左、右子树两部分。然后再递归判断左右子树的结构是否符合。当有元素违背 BST 的规则时，则返回 False

该题由于测试用例为 [] 时，需要返回 False，如果为空情况返回 True 的话，直接调用 helper 函数即可。

要注意左右子树可能为空的情况，如果去找 i 这个点，记得 left 和 right 为空的情况。
不能通过前一个数比 sequence[-1] 小，后一个数比 sequence[-1] 更大来判断 i 的位置，因为有可能最开始的数很大，因此当遇到第一个比 sequence[-1] 更大的数时就将数组分成左右两个部分。

```python
class Solution:
    def VerifySquenceOfBST(self, sequence):
        # write code here
        if not sequence:
            return False
        return self.helper(sequence)
    
    def helper(self, sequence):
        if len(sequence) <= 2:
            return True
        left = []
        right = []
        i = 0
        while sequence[i] < sequence[-1]:
            left.append(sequence[i])
            i += 1
        right = sequence[i:-1]
        for j in range(len(right)):
            if right[j] < sequence[-1]:
                return False
        return self.helper(left) and self.helper(right)
```

### 二叉树中和为某一值的路径
输入一颗二叉树的跟节点和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。(注意: 在返回值的list中，数组长度大的数组靠前)

```python
def FindPath(self, root, expectNumber):
    # write code here
    res = []
    def dfs(root, n, arr):
        if not root:
            return 
        if not root.left and not root.right and n-root.val == 0:
            res.append(arr+[root.val])
        if root.left:
            dfs(root.left, n-root.val, arr+[root.val])
        if root.right:
            dfs(root.right, n-root.val, arr+[root.val])
    
    dfs(root, expectNumber, [])
    res = sorted(res, key = lambda x : len(x), reverse=True)
    return res
```

### 复杂链表的复制
输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针指向任意一个节点），返回结果为复制后复杂链表的head。（注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空）

思路1：如果先复制原始链表的每一个节点，并用指针链接起来；再设置每个节点的 random 指针。 原始链表需要经过 n 步找到他的 random，那么新链表也需要 n 步找到 random 指向的节点，那么最终的时间复杂度是 O(n<sup>2</sup>)。

思路2：用空间换时间，分为三步走，最终的时间复杂度 O(n), 空间复杂度为 O(n)
1. 在原始链表的每个节点后面都插入一个新的节点，新节点的值与原来的相同
2. 找到新节点的 random 指针指向的节点 
3. 将新链表从原始链表中拆出来

```python
# -*- coding:utf-8 -*-
# class RandomListNode:
#     def __init__(self, x):
#         self.label = x
#         self.next = None
#         self.random = None
class Solution:
    # 返回 RandomListNode
    def Clone(self, pHead):
        # write code here
        if not pHead:
            return None
        cur = pHead
        while cur:
            new_node = RandomListNode(cur.label)
            new_node.next = cur.next
            cur.next = new_node
            cur = cur.next.next
        
        cur = pHead
        while cur:
            if cur.random:
                cur.next.random = cur.random.next
            cur = cur.next.next
            
        new_head = pHead.next
        pold = pHead
        pnew = new_head
        while pnew.next:
            pold.next = pnew.next
            pnew.next = pnew.next.next
            pold = pold.next
            pnew = pnew.next
        pold.next = None
        pnew.next = None
        return new_head
```

### 二叉搜索树与双向链表
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

### 字符串的排列
输入一个字符串,按字典序打印出该字符串中字符的所有排列。例如输入字符串abc,则打印出由字符a,b,c所能排列出来的所有字符串abc,acb,bac,bca,cab和cba。

```python
class Solution:
    def Permutation(self, ss):
        # write code here
        if not ss:
            return []
        res = []
        size = len(ss)
        def dfs(ss, string):
            if len(string) > size:
                return
            if len(string)== size and string not in res:
                res.append(string)
                return 
            for i in range(len(ss)):
                dfs(ss[:i]+ss[i+1:], string+ss[i])
        dfs(ss, "")
        return res
```

### 数组中出现次数超过一半的数字
数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。例如输入一个长度为9的数组{1,2,3,2,2,2,5,4,2}。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。如果不存在则输出0。

思路： 摩尔投票法，同加异减的思想，注意最后需要判断选出来的数字是否符合条件

```python
class Solution:
    def MoreThanHalfNum_Solution(self, numbers):
        if not numbers:
            return 0
        cnt = 1
        num = numbers[0]
        for i in range(1, len(numbers)):
            if numbers[i] == num:
                cnt += 1
            else:
                cnt -= 1
            if cnt == 0:
                num = numbers[i]
                cnt = 1
        return num if numbers.count(num) > len(numbers)/2 else 0
```

### 最小的K个数
输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

思路： 最直观的做法就是先排序再给出前 k 个数，但时间复杂度为 O(nlogn)

1. 如果能够修改原数组，且不要求输出的这 k 个数有序，可以将时间复杂度降到 O(n)，利用快速排序的原理将数组分为两部分，使得比第 k 个数字小的都在左边，比第 k 个数字大的都在右边，这样找到数组的第 k 个数字，就找到了最小的 k 个数。

为什么时间复杂度是 O(n) ： 对于快速排序，一次快速排序 partition 的时间是 O(n)，总共要进行 logn 次排序，因此时间复杂度是 O(n)，而在此题中，类似于二分查找 k 的位置，并不需要递归到 logn 这层，可能几次就找到了 k 的位置，如果刚好每次二分进入一半的数组的话，那么时间复杂度为 O(n) + O(2/n) + O(4/n) + ... < O(2n)， 因此时间复杂度为 O(n)

```python
# -*- coding:utf-8 -*-
class Solution:
    def GetLeastNumbers_Solution(self, tinput, k):
        # write code here
        if k <= 0 or k > len(tinput):
            return []
        left, right = 0, len(tinput) - 1
        index = self.partition(tinput, left, right)
        while index != k-1:
            if index > k-1:
                index = self.partition(tinput, left, index-1)
            elif index < k-1:
                index = self.partition(tinput, index+1, right)
        return tinput[:k]
        
    def partition(self, tinput, left, right):
        key = tinput[left]
        while left < right:
            while left < right and tinput[right] >= key:
                right -= 1
            tinput[left] = tinput[right]
            while left < right and tinput[left] <= key:
                left += 1
            tinput[right] = tinput[left]
        tinput[left] = key
        return left
```

2. 适用于处理海量数据，时间复杂度为 O(nlogk) 的做法

思路： 创建一个大小为 k 的容器来存储最小的 k 个数，遍历数组
1. 若容器中的数字少于 k 个，则直接把读入的数字加入容器中
2. 若容器中的数字等于 k 个，则不能再插入数字，只能替换已有的数字，先找到容器中最大的数，然后与新数字进行比较，若待插入的数字比当前最大值小，则替换当前最大值；若待插入的数字比当前最大值还大，那么它不可能成为最小的 k 个数，舍弃。

我们可以用二叉树来实现这个容器，在 O(logk) 的时间里能完成一次操作，总共有 n 个数字，则时间复杂度为 O(nlogk)

由于每次都要去找容器中的最大值，我们可以用最大堆来实现，最大堆中根节点的值是最大的，那么找到每次找到容器中最大值的时间复杂度为 O(1)，同时需要 O(logk) 的时间来完成删除和插入新节点。如果要自己实现最大堆有些复杂，在允许使用标准库时，我们可以借助 python 中的 

```python
# -*- coding:utf-8 -*-
class Solution:
    def GetLeastNumbers_Solution(self, tinput, k):
        # write code here
        if k <= 0 or k > len(tinput):
            return []
        for i in range((k//2)-1, -1, -1):
            self.max_heapify(tinput, k, i)
        for i in range(k, len(tinput)):
            if tinput[i] < tinput[0]:
                tinput[0], tinput[i] = tinput[i], tinput[0]
                self.max_heapify(tinput, k, 0)
        return sorted(tinput[:k])
    
    def max_heapify(self, heap, k, root):
        left = 2*root + 1
        right = 2*root + 2
        largest = root
        if left < k and heap[largest] < heap[left]:
            largest = left
        if right < k and heap[largest] < heap[right]:
            largest = right
        if largest != root:
            heap[largest], heap[root] = heap[root], heap[largest]
            self.max_heapify(heap, k, largest)
```


### 连续子数组的最大和
例如:{6,-3,-2,7,-15,1,2,2},连续子向量的最大和为8(从第0个开始,到第3个为止)。给一个数组，返回它的最大连续子序列的和

思路： dp[i] 表示从第一个数到第 i 个数的最大子序列和，dp[i] = max(dp[i] + nums[i], nums[i])，max_sum 用来记录全局的最大子序列和

```python
def FindGreatestSumOfSubArray(self, array):
    dp = -float('inf')
    max_sum = dp
    for i in range(len(array)):
        dp = max(dp+array[i], array[i])
        max_sum = max(dp, max_sum)
    return max_sum
```

### 整数中1出现的次数
求出任意非负整数区间中1出现的次数（从1 到 n 中1出现的次数）。

思路： 直接的思路是求出 1-n 每个数字中 1 出现的次数，可以用除法和取模运算得到，有 n 个数字，平均每个数字有 logn 位，那么时间复杂度为 O(nlogn)，运算效率较低

考虑一个更有效的思路： 寻找 1 出现的规律。 

对于 1-n 的这些数，总的出现 1 的总次数 = 个位为 1 的次数 + 十位为 1 的次数 + 百位为 1 的次数 + ... + 最高位为 1 的次数

我们以一个 n 为一个五位数，百位为 1 的次数为例进行分析：
1. 若 n 的百位 >= 2, 如 31256，把 312 记为 a，56 记为 b，
那么 1-n 中百位为 1 的数有 (00-31)1(00-99)，也就有 `32*100` 个，即 `(a/10+1)*100`

2. 若 n 的百位 == 1, 如 31156，把 311 记为 a，56 记为 b，
那么 1-n 中百位为 1 的数有 (00-30)1(00-99) 和 311(00-56)，也就有 `31*100+57` 个，即 `a/10*100 + b + 1`

3. 若 n 的百位 == 0，如 31056，那百位为 1 的数有 (00-30)1(00-99) ，也就有 `31*100` 个，即 `a/10*100`

因此总的个数从个位为 1 开始，按照上述规则进行计算再相加

```python
# -*- coding:utf-8 -*-
class Solution:
    def NumberOf1Between1AndN_Solution(self, n):
        # write code here
        cnt = 0
        i = 1
        while i <= n:
            digit = n / i % 10 # 当前位数上的数字
            a = n / i
            b = n % i
            if digit == 0:
                cnt += (a / 10) * i
            elif digit == 1:
                cnt += (a / 10) * i + b + 1
            else:
                cnt += (a / 10 + 1) * i
            i = i * 10 # 进位
        return cnt
```

### 把数组排成最小的数
输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。例如输入数组{3，32，321}，则打印出这三个数字能排成的最小数字为321323。

如果求所有的排列时间复杂度 O(n!)

思路： leetcode 179，这道题需要我们找到一个排序规则，数组根据这个规则排序后能排成一个最小的数字。对于两个数 n 和 m，将两个数组合起来，我们需要比较的是 nm 和 mn 哪个更小，如果 nm < mn，那么 n 应该排在前面

```python
class Solution:
    def PrintMinNumber(self, numbers):
        # write code here
        numbers = [str(i) for i in numbers]
        numbers = sorted(numbers, self.cmp)
        return ''.join(numbers)
        
    def cmp(self, x, y):
        if x+y > y+x: # 注意 sorted 自定义比较函数，如果 x 要排在 y 前面就 return -1
            return 1
        if x+y < y+x:
            return -1
        return 0
```

### 丑数
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

### 第一个只出现一次的字符
在一个字符串(0<=字符串长度<=10000，全部由字母组成)中找到第一个只出现一次的字符,并返回它的位置, 如果没有则返回 -1（需要区分大小写）.

两次遍历

```python
def FirstNotRepeatingChar(self, s):
    # write code here
    dict = {}
    for c in s:
        if c not in dict:
            dict[c] = 1
        else:
            dict[c] += 1
    for i in range(len(s)):
        if dict[s[i]] == 1:
            return i
    return -1
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

### 数字在排序数组中出现的次数
统计一个数字在排序数组中出现的次数。

思路： 看到排序数组，就应该考虑是否可以用二分查找来解决，可以找到这个数字第一次出现的位置和最后一次出现的位置，last-start+1 就是数字出现的次数。

注意找不到时的特殊情况，可能是最左边也可能最右边，left 会比 right 更大 1，要是在左边就要判断找到的 data[left] 是否等于 k，要是在右边就要判断 left 是否越界。

```python
# -*- coding:utf-8 -*-
class Solution:
    def GetNumberOfK(self, data, k):
        # write code here
        left, right = 0, len(data)-1
        while left <= right:
            mid = left + (right-left)//2
            if data[mid] >= k:
                right = mid - 1
            else:
                left = mid + 1
        if left >= len(data) or data[left] != k:
            return 0
        start = left
        
        right = len(data)-1
        while left <= right:
            mid = left + (right-left)//2
            if data[mid] <= k:
                left = mid + 1
            else:
                right = mid - 1
        end = right
        return end-start+1
```

### 平衡二叉树
输入一棵二叉树，判断该二叉树是否是平衡二叉树。

```python
class Solution:
    def IsBalanced_Solution(self, pRoot):
        # write code here
        if not pRoot:
            return True
        if abs(self.maxHeight(pRoot.left) - self.maxHeight(pRoot.right)) > 1:
            return False
        return self.IsBalanced_Solution(pRoot.left) and self.IsBalanced_Solution(pRoot.right)
        
    def maxHeight(self, pRoot):
        if not pRoot:
            return 0
        return max(self.maxHeight(pRoot.left), self.maxHeight(pRoot.right)) + 1
```

### 数组中只出现一次的数字
一个整型数组里除了两个数字之外，其他的数字都出现了两次。请写程序找出这两个只出现一次的数字。

如果是只有一个数字出现一次，其余数字都出现两次的话，可以用异或来找到。
```python
def singleNumber(self, nums):
    res = 0
    for i in range(len(nums)):
        res = res ^ nums[i]
    return res
```

现在题中有两个数字只出现一次，可以考虑将原数组分成两个部分，每个部分里都含有一个只出现一次的数字。那么如何进行分组？

思路： 把所有数字进行异或，最终得到的结果是两个不同的单数字异或的结果，肯定是不为 0 的，那么结果的二进制中必定含有至少一个 1。 我们找到第一个为 1 的位置，对于 single1 该位置为 1， single2 该位置为 0，这样就可以把这两个数分到两个不同的数组中，其他数字也同样的根据这个位置是 0 还是 1 分到对应的组中，相同数字必定在同一个分组中。这样对两个数组分别进行异或，就可以得到这两个单数字。

```python
# -*- coding:utf-8 -*-
class Solution:
    # 返回[a,b] 其中ab是出现一次的两个数字
    def FindNumsAppearOnce(self, array):
        # write code here
        res = 0
        for i in range(len(array)):
            res = res ^ array[i]
        index = 0
        while res & 1 == 0:
            res >>= 1
            index += 1

        arr1 = []
        arr2 = []
        for i in range(len(array)):
            num = array[i] >> index
            if num & 1 == 1:
                arr1.append(array[i])
            else:
                arr2.append(array[i])

        res1, res2 = 0, 0
        for i in range(len(arr1)):
            res1 = res1 ^ arr1[i]
        for i in range(len(arr2)):
            res2 = res2 ^ arr2[i]
        return [res1, res2]
```

### 和为S的两个数字
输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。对应每个测试案例，输出两个数，小的先输出。

思路： 用两个指针分别指向左边和右边的数，由于是递增数组，当 array[left] + array[right] < tsum 时，说明需要更大的数字相加，就把 left + 1；当 array[left] + array[right] = tsum 时，找到这样两个数字，但由于可能有多组符合条件的，当发现乘积更小时就进行置换，注意不存在时返回空数组。

```python
def FindNumbersWithSum(self, array, tsum):
    num1, num2 = 0, 0
    cmp = float('inf')
    left, right = 0, len(array)-1
    while left < right:
        if array[left] + array[right] < tsum:
            left += 1
        elif array[left] + array[right] > tsum:
            right -= 1
        else:
            if array[left] * array[right] < cmp:
                num1 = array[left]
                num2 = array[right]
                cmp = num1 * num2
            left += 1
            right -= 1
    return [num1, num2] if cmp != float('inf') else []
```

### 和为S的连续正数序列
输出所有和为S的连续正数序列。序列内按照从小至大的顺序，序列间按照开始数字从小到大的顺序

思路： 延续上一题的思路，可以用两个指针 left 和 right 表示一个连续正数序列的起始数字和终止数字，我们从 letf = 1，right = 2 开始进行计算，当前连续正数序列的和为 cur_sum。
1. 当 cur_sum < tsum 时，说明需要增加数字，就让 right+1，不用每次都重复循环计算 cur_sum 的值，因为每次都只增加一个或者减少一个数字，只需要根据之前的 cur_sum 和增加或减少的数字来算即可
2. 当 cur_sum > tsum 时，说明需要减少数字，cur_sum 要减去之前 left 的值，再让 left-1
3. 当 cur_sum = tsum 时，找到符合条件的序列的左右边界，将其添加的结果数组中，并修改边界的值。

```python
def FindContinuousSequence(self, tsum):
    res = []
    left, right = 1, 2
    max_num = (tsum + 1) // 2
    cur_sum = left + right
    while left <= max_num:
        if cur_sum < tsum:
            right += 1
            cur_sum += right
        elif cur_sum > tsum:
            cur_sum -= left
            left += 1
        else:
            res.append([i for i in range(left, right+1)])
            right += 1
            cur_sum = cur_sum + right - left
            left += 1
    return res
```

### 翻转单词顺序列
牛客最近来了一个新员工Fish，每天早晨总是会拿着一本英文杂志，写些句子在本子上。同事Cat对Fish写的内容颇感兴趣，有一天他向Fish借来翻看，但却读不懂它的意思。例如，“student. a am I”。后来才意识到，这家伙原来把句子单词的顺序翻转了，正确的句子应该是“I am a student.”。Cat对一一的翻转这些单词顺序可不在行，你能帮助他么？

思路： 如果按照 c++ 或 java，就先翻转整个字符串，在按照空格分割字符串，翻转每个单词，用 python 就比较偷懒，需要注意的是几个特殊情况

```python
def ReverseSentence(self, s):
    if not s:
        return s
    slist = s.split()
    if not slist:
        return s # s = " ",返回 s
    return " ".join(slist[::-1])
```

### 左旋转字符串
汇编语言中有一种移位指令叫做循环左移（ROL），现在有个简单的任务，就是用字符串模拟这个指令的运算结果。对于一个给定的字符序列S，请你把其循环左移K位后的序列输出。例如，字符序列S=”abcXYZdef”,要求输出循环左移3位后的结果，即“XYZdefabc”。是不是很简单？OK，搞定它！

思路： 按照上提的思路，可以先把 s 分成左右两个部分，abc 和 XYZdef，分别翻转得到，s1 = cbafedZYX，再将 s1 整个进行翻转得到 s2 = XYZdefabc 

python 的切片功能可以快速解决。
```python
def LeftRotateString(self, s, n):
    if not s:
        return s
    size = len(s)
    n = n % size
    return s[n:]+s[:n]
```

### 扑克牌顺子
随机抽取扑克牌中的5张牌,判断是不是顺子,即这5张牌是不是连续的。其中A看成1,J看成11,Q看成12,K看成13,大小王可以看成任何需要的数字。

思路： 该题需要把扑克牌背景抽象成计算机语言，5 张扑克牌可以看做是一个含有 5 个数字的数组，对于大小王可以定义为 0，用他可以代替任何数字，因此该题需要判断 nums 是否是连续的。

可以先对 numbers 排序，再计算出 numbers 中 0 的个数，对于剩下的数字，如果无法连成顺子，计算需要用多少个 0 来补足，如果超过了 0 的数量，就无法连成顺子，返回 False

```python
# -*- coding:utf-8 -*-
class Solution:
    def IsContinuous(self, numbers):
        # write code here
        if not numbers:
            return False
        numbers.sort()
        zeros = numbers.count(0)
        gap = 0
        for i in range(zeros, len(numbers)-1): # 前面都是 0，因此直接从 0 之后的数字开始遍历
            if numbers[i] == numbers[i+1]:
                return False
            gap = gap + numbers[i+1] - numbers[i] - 1
            if gap > zeros:
                return False
        return True
```

### 圆圈中最后剩下的数
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

### 求1+2+3+...+n
求1+2+3+...+n，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

思路： 可以用加减法，因此重点在于如何终止循环。

利用逻辑运算符 and 和 or 的短路特性来实现递归终止，比如 a and b，如果 a 是 False，就返回 a，如果 a 是 True，就返回 b。 对于数值， 2 and 3 会返回 3， 2 or 3 会返回 2。

“or” 运算符表示“或”，有一个为真则全部为真；前半部分判断出来是真的，后半部分就不再进行运算了。
“and”运算符表示“与”，前一项为假则整个表达式为假，因此可以利用这个性质进行递归运算或者达到整洁代码的目的。


```python
 def Sum_Solution(self, n):
    return (n and n + self.Sum_Solution(n-1))
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

### 把字符串转换成整数
将一个字符串转换成一个整数(实现Integer.valueOf(string)的功能，但是string不符合数字要求时返回0)，要求不能使用字符串转换整数的库函数。 数值为0或者字符串不是一个合法的数值则返回0。

```python
# -*- coding:utf-8 -*-
class Solution:
    def StrToInt(self, s):
        # write code here
        if not s:
            return 0
        flag = 1
        s = s.strip()
        if s == '+' or s == '-':
            return 0
        if s[0] == '-':
            flag = -1
            s = s[1:]
        elif s[0] == '+':
            s = s[1:]
        for c in s:
            if c not in ['0','1','2','3','4','5','6','7','8','9']:
                return False
        return flag * int(s)
            
```

### 数组中重复的数字
在一个长度为n的数组里的所有数字都在0到n-1的范围内。 数组中某些数字是重复的，但不知道有几个数字是重复的。也不知道每个数字重复几次。请找出数组中任意一个重复的数字。 例如，如果输入长度为7的数组{2,3,1,0,2,5,3}，那么对应的输出是第一个重复的数字2。

思路一：利用哈希表，时间复杂度 O(n), 空间复杂度 O(n)
```python
class Solution:
    # 这里要特别注意~找到任意重复的一个值并赋值到duplication[0]
    # 函数返回True/False
    def duplicate(self, numbers, duplication):
        # write code here
        dict = {}
        for num in numbers:
            if num not in dict:
                dict[num] = 1
            else:
                duplication[0] = num
                return True
        return False
```

思路二： 由于数字都是 0 到 n-1 范围内的，若没有重复数字且排好序的话，数字与其下标是相等的，我们现在可以来重排这个数组。从 i = 0 开始，当 nums[i] = i 时，i + 1，不相等，则将 nums[i] 与第 nums[i] 的那个数字进行交换，然后再看 i = 0 这个位置上的数字是不是符合要求，当发现有两个数字到一个位置时，就找到了这个重复数字。时间复杂度为 O(n)，空间复杂度为 O(1)

```python
def duplicate(self, numbers, duplication):
    # write code here
    for i in range(len(numbers)):
        while numbers[i] != i:
            if numbers[numbers[i]] == numbers[i]:
                duplication[0] = numbers[i]
                return True
            numbers[numbers[i]], numbers[i] = numbers[i], numbers[numbers[i]] # 注意这个顺序不可以交换，自己写个 tmp 中间交换就明白了

    return False
```

### 构建乘积数组
给定一个数组A[0,1,...,n-1],请构建一个数组B[0,1,...,n-1],其中B中的元素B[i]=A[0]*A[1]*...*A[i-1]*A[i+1]*...*A[n-1]。不能使用除法。

思路： B[i] 是 A 数组中除了 A[i] 之外的所有数的乘积，也就是 i 左边元素的乘积 * i 右边元素的乘积，因此可以分为两部分计算。第一个 for 计算 i 左边的乘积，第二个 for 计算 i 右边的乘积。

```python
def multiply(self, A):
    # write code here
    if not A:
        return []
    B = [None] * len(A)
    B[0] = 1
    for i in range(1, len(B)):
        B[i] = B[i-1] * A[i-1]
    tmp = 1
    for i in range(len(B)-2, -1, -1):
        tmp *= A[i+1]
        B[i] *= tmp
    return B
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

### 表示数值的字符串
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

### 字符流中第一个不重复的字符
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

### 链表中环的入口结点
给一个链表，若其中包含环，请找出该链表的环的入口结点，否则，输出null。

```python
class Solution:
    def EntryNodeOfLoop(self, pHead):
        # write code here
        if not pHead:
            return None
        fast = slow = pHead
        flag = 0
        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
            if fast == slow:
                flag = 1
                break # 切记要 break！！！
        if not flag:
            return None
        
        slow = pHead # fast 不用重走，他已经在相遇的地方
        while fast != slow:
            fast = fast.next
            slow = slow.next
        return fast
```

### 删除链表中重复的结点
在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点不保留，返回链表头指针。 例如，链表1->2->3->3->4->4->5 处理后为 1->2->5

```python
class Solution:
    def deleteDuplication(self, pHead):
        # write code here
        if not pHead or not pHead.next:
            return pHead
        dummy = ListNode(0)
        dummy.next = pHead
        pre = dummy
        cur = pHead
        while cur and cur.next: # 注意这个条件
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

### 二叉树的下一个结点
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

### 二叉搜索树的第k个结点
给定一棵二叉搜索树，请找出其中的第k小的结点。例如， （5，3，7，2，4，6，8）    中，按结点数值大小顺序第三小结点的值为4。

```python
class Solution:
    # 返回对应节点TreeNode
    def KthNode(self, pRoot, k):
        # write code here
        if k <= 0:
            return None
        stack = []
        while pRoot or stack:
            while pRoot:
                stack.append(pRoot)
                pRoot = pRoot.left
            if stack:
                node = stack.pop()
                k -= 1
                if k == 0:
                    return node
                pRoot = node.right
        return None
```

### 数据流中的中位数
如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。我们使用Insert()方法读取数据流，使用GetMedian()方法获取当前读取数据的中位数。

思路一：

```python
# -*- coding:utf-8 -*-
class Solution:
    def __init__(self):
        self.nums = []
    def Insert(self, num):
        # write code here
        self.nums.append(num)
        self.nums.sort()
    def GetMedian(self, nums):
        # write code here
        l = len(self.nums)
        if l % 2 == 1:
            return self.nums[l//2]
        else:
            return (self.nums[l//2] + self.nums[(l-1)//2]) / 2.0 # 注意此处
```

思路二：如何利用最大堆和最小堆求解？

### 滑动窗口的最大值
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


### 矩阵中的路径
请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一个格子开始，每一步可以在矩阵中向左，向右，向上，向下移动一个格子。如果一条路径经过了矩阵中的某一个格子，则之后不能再次进入这个格子。 例如 a b c e s f c s a d e e 这样的3 X 4 矩阵中包含一条字符串"bcced"的路径，但是矩阵中不包含"abcb"路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入该格子。

思路： 该题为 leetcode79，但不同的是 matrix 是用一个一维数组表示二维数组，可以先将其转化为一个二维数组，这样能更加直观的解题。

1. 创建一个和 matrix 一样大小的二维数组 visited，用来记录被访问过的节点
2. 在 matrix 中按照顺序找到与 path 的第一个字母相同的位置，将这个位置的 visited 标记为 True，再从这个位置的上下左右去进行 DFS
3. 当某条路径走不通时，则进行回溯，并把该位置的 visited 重新标记为 False（因为别的路径可能会经过这个位置），去 matrix 中找下一个与 path 字母相同的位置。

```python
# -*- coding:utf-8 -*-
class Solution:
    def hasPath(self, matrix, rows, cols, path):
        # write code here
        visited = [[False for _ in range(cols)] for _ in range(rows)]
        
        m = [[0 for _ in range(cols)] for _ in range(rows)]
        index = 0
        for i in range(rows):
            for j in range(cols):
                m[i][j] = matrix[index]
                index += 1
        
        def dfs(i, j, k):
            if k == len(path):
                return True
            # 向上
            if i-1 >= 0 and not visited[i-1][j] and m[i-1][j] == path[k]:
                visited[i-1][j] = True
                if dfs(i-1, j, k+1):
                    return True
                visited[i-1][j] = False
            # 向下
            if i+1 < rows and not visited[i+1][j] and m[i+1][j] == path[k]:
                visited[i+1][j] = True
                if dfs(i+1, j, k+1):
                    return True
                visited[i+1][j] = False
            # 向左
            if j-1 >= 0 and not visited[i][j-1] and m[i][j-1] == path[k]:
                visited[i][j-1] = True
                if dfs(i, j-1, k+1):
                    return True
                visited[i][j-1] = False
            # 向右
            if j+1 < cols and not visited[i][j+1] and m[i][j+1] == path[k]:
                visited[i][j+1] = True
                if dfs(i, j+1, k+1):
                    return True
                visited[i][j+1] = False

        for i in range(rows):
            for j in range(cols):
                if m[i][j] == path[0]:
                    visited[i][j] = True
                    if dfs(i, j, 1):
                        return True
                    visited[i][j] = False
        return False
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