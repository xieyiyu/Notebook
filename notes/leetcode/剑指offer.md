<!-- GFM-TOC -->
* [字符串](#字符串)
* [替换空格](#替换空格)
* [从尾到头打印链表](#从尾到头打印链表)
* [重建二叉树](#重建二叉树)
* [** 用两个栈实现队列](#用两个栈实现队列)
* [** 旋转数组的最小数字](#旋转数组的最小数字)
* [矩形覆盖](#矩形覆盖)
* [** 二进制中1的个数](#二进制中1的个数)
* [数值的整数次方](#数值的整数次方)
* [在O(1)时间删除链表节点](#在O-1-时间删除链表节点)
* [调整数组顺序使奇数位于偶数前面](#调整数组顺序使奇数位于偶数前面)
* [链表中倒数第 k 个结点](#链表中倒数第-k-个结点)
* [树的子结构](#树的子结构)
<!-- GFM-TOC -->

### 字符串
#### 替换空格
请实现一个函数，将一个字符串中的每个空格替换成 "%20"。例如，当字符串为 We Are Happy,则经过替换之后的字符串为 We%20Are%20Happy。

- 问题1： 是在当前字符串上替换，还是可以开辟一个新的字符串做替换？
- 问题2： 在当前字符串上替换，怎么做才能更有效率？
从前往后替换的话，后面的字符要移动多次，效率低，时间复杂度为 O(n<sup>2</sup>); 而从后往前替换，先计算出需要增加多少空间，在从后往前移动，每个字符只需移动一次，时间复杂度为 O(n)。

思路： 用两个指针，p1 指向原始字符串的末尾，p2 指向替换后的字符串的末尾； 当 p1 指向空格时，就将其替换为 %20，同时 p1 向前移动一格，p2 向前移动三格。

```python

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
 
```python
class Solution:
    def minNumberInRotateArray(self, rotateArray):
        # write code here
        if not rotateArray:
            return 0
        left, right = 0, len(rotateArray)-1
        while right - left > 1:
            mid = left + (right-left)//2
            if rotateArray[mid] == rotateArray[left] and rotateArray == rotateArray[right]:
                for i in range(left+1, len(rotateArray)):
                    if rotateArray[i] < rotateArray[left]:
                        return rotateArray[i]
            elif rotateArray[mid] >= rotateArray[left]:
                left = mid
            else:
                right = mid
        return rotateArray[right]
```

### 变态跳台阶
一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

```python
class Solution:
    def jumpFloorII(self, number):
        # write code here
        if not number: return 0
        dp = [1]
        for i in range(1, number):
            f = sum(dp)
            dp.append(f)
        return sum(dp)
```

### 矩形覆盖
我们可以用2 * 1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2 * 1的小矩形无重叠地覆盖一个2 * n的大矩形，总共有多少种方法？

思路： 仍然是斐波拉切数列，最后一个小矩形竖着放，有 f(n-1) 种放法，横着放，则下面必须再横着放一个，则有 f (n-2) 种放法，f(n) = f(n-1) + f(n-2)

## 位运算
### 二进制中1的个数
输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。

思路： 从 n 的二进制的最右边与 1 进行按位与，正数可以得到正确结果，但负数右移时在最高位补的是 1，而与 1 按位与的话，会全部变成 1 而进入死循环。 因此可以将数字 1 左移，再和 n 进行按位与。

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

思路二： 将一个整数减去 1，再和原整数做按位与运算，会把该整数最右边一个 1 变成 0， 因此一个整数有多少个 1， 就可以进行多少次这样的运算，知道该整数变为 0.

1. 用一条语句判断一个整数是不是 2 的整数次方：
```python
if (n-1)&n == 0：
	return True
```

2. 输入两个整数 m 和 n，计算需要改变 m 的二进制表示的多少位才能得到 n：
先异或，再计算异或得到的二进制中的 1 的个数。


### 数值的整数次方
给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

注意考虑各种边界条件

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
        if not pRoot1 and pRoot2:
            return False
        if pRoot1.val != pRoot2.val:
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