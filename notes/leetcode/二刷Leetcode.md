# 二刷 Leetcode
## 提高效率！！！

<!-- GFM-TOC -->
* [2. Add Two Numbers](#add-two-numbers)
* [3. Longest Substring Without Repeating Characters](#longest-substring-without-repeating-characters)
* [** 4. Median of Two Sorted Arrays](#median-of-two-sorted-arrays)
* [Longest Palindromic Substring](#longest-palindromic-substring)
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

通过枚举每个回文子串的中心，然后往左右两边扩展，来得到最长回文子串。  
可以改进的地方是：如果有相同字母连在一起的情况，则先找到这一串连在一起的字母，再向两边扩展。

### ZigZag Conversion
[Leetcode : 6. ZigZag Conversion(Medium)](https://leetcode.com/problems/zigzag-conversion/description/)

找规律型题，画出图来，然后看每一行到下一个字符的步长，注意第一行和最后一行的步长是相同的，而中间的行会出现两种不同的步长。