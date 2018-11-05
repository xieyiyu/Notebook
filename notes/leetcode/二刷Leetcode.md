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