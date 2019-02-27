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

```python

```

