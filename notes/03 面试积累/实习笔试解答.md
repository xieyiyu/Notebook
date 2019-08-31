## 20181207 字节跳动
1 验证密码，长度要求，大写字母 小写字母 数字 其他至少要三种，不能有长度超过2的重复子串
```python
def test_pwd(s):
    if len(s) > 20 or len(s) < 6:
        return False
    type = [0, 0, 0, 0]
    for i in range(len(s)):
        if s[i] in 'abcdefghijklmnopqrstuvwxyz':
            type[0] = 1
        elif s[i] in 'ABCDEFGHIJKLMNOPQRSTUVWXYZ':
            type[1] = 1
        elif s[i] in '0123456789':
            type[2] = 1
        else:
            type[3] = 1
    if sum(type) < 3:
        return False
    for i in range(len(s)-2):
        for j in range(i+2, len(s)):
            if s[i:j+1] in s[j+1:]:
                return False
    return True
```

2 leetcode55

3 捡金币，n * n的格子grid，-1表示障碍，该格不能走，0表示可以通过，1表示有一个金币，grid的值只有这三种，从左上到右下，只能向右或向下，到最后一格，然后再从右下到左上，只能向左或向上，求能够获得的最大金币数。第一次走过的格子，捡了金币后应该置为0，该格还可以继续走，(0，0)和(-1，-1)这两格不会是-1。  

思路：总体的最大值即为从左上到右下的最大值加上从右下到左上的最大值。
1. 用二维数组 dp[i][j] 来存储到达 (i,j) 格子时，能够捡到的最大金币数，从左上到右下只能向右或者向下走，因此 dp[i][j] = max(dp[i-1][j], dp[i][j-1]) + grid[i][j]
2. 设计函数 pick(grid), 得到从左上到右下能够捡到的最大金币数 dp1 = dp[-1][-1]
3. 根据 dp 数组回溯寻找走过的路径，并将走过的格子的金币数设为 0， 注意在边缘的时候，第 0 行只能从左边过来，第 0 列只能从右边过来。其余地方判断方法为：当 dp[i-1][j] >= dp[i][j-1] 时，说明是从上面过来的，则将上面一个 grid[i-1][j] = 0，反之将 grid[i][j-1] = 0
4. 根据 3 得到了一个新的 grid，需要获得从右下到左上的最大金币数，这相当于将 grid 左右翻转再上下翻转，得到从左上到右下的最大金币数。因此将 grid 先左右翻转再上下翻转，再运行一遍 pick(grid)，得到 dp2 = dp[-1][-1]
5. 最终得到的金币最大值为 dp1 + dp2

```python
def pick_gold(grid):
    if not grid:
        return 0
    N = len(grid)
    dp = pick(grid)
    dp1 = dp[-1][-1] # 得到左上到右下的最大金币数
    # 回溯寻找走过的路径，并将走过的格子金币数置 0, 得到新的 grid
    grid[0][0], grid[-1][-1] = 0, 0
    i = j = N-1
    while i!=0 or j!=0:
        if i == 0: # 边缘，第0行的时候，只能从左边来
            grid[0][j-1] = 0
            j -= 1
        if j == 0: # 边缘，第0列的时候，只能从右边来
            grid[i-1][0] = 0
            i -= 1
        elif dp[i-1][j] >= dp[i][j-1]: # 从上面来
            grid[i-1][j] = 0
            i -= 1
        else: # 从左边来
            grid[i][j-1] = 0
            j -= 1
    # 将 grid 左右翻转再上下翻转
    for i in range(N):
        for j in range(N//2):
            grid[i][j], grid[i][N-j-1] = grid[i][N-j-1], grid[i][j]
    for i in range(N//2):
        for j in range(N):
            grid[i][j], grid[N-i-1][j] = grid[N-i-1][j], grid[i][j]
    dp = pick(grid)
    dp2 = dp[-1][-1] # 得到右下到左上的最大金币数
    return dp1 + dp2

def pick(grid):
    N = len(grid)
    dp = [[0 for _ in range(N)] for _ in range(N)]
    # 填充边界
    for i in range(N):
        if grid[i][0] == -1:
            break
        dp[i][0] = dp[i-1][0] + grid[i][0]
    for j in range(N):
        if grid[0][j] == -1:
            break
        dp[0][j] = dp[0][j-1] + grid[0][j]
    for i in range(1, N):
        for j in range(1, N):
            if grid[i][j] != -1:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1]) + grid[i][j]
    return dp
```

### 20190309 腾讯提前批
1. 1-n 种面值的硬币，无穷个，商品价格为 m，求组成 m 的最小硬币数

思路： 注意此处是 1,2,3,...,n 种面值，因此可以直接贪心解决。 如果是特定几种面值，则是完全背包问题。

```python
def function(n, m):
    res = 0
    flag = n
    while m:
        if m >= flag:
            m -= flag
            res += 1
        else:
            flag = m
    return res
```

2. 有一个序列是 i * (-1)^i, nums = [-1, 2, -3, 4, -5, 6 ...]，给定区间 n，m，求出该区间的和， n 从 1 开始。

思路： 找出规律，分 n,m 分别是奇数和偶数，共四种情况考虑，直接计算出和。

```python
# def function(n, m):
#     if n > m:
#         return 0
#     if n % 2 != 0:
#         return function(n+1, m) - n
#     if (m-n+1) % 2 != 0:
#         return function(n, m-1) + m
#     return -(m-n+1) //2
def function(n, m):
    if n > m:
        return 0
    if n == m and n % 2 != 0:
        return -n
    if n == m and n % 2 == 0:
        return n
    if n % 2 != 0 and m % 2 == 0:
        return (m-n+1)//2
    if n % 2 != 0 and m % 2 != 0:
        return (m-n+1)//2 - m
    if n % 2 == 0 and m % 2 == 0:
        return -((m-n+1)//2) + m
    if n % 2 == 0 and m % 2 != 0:
        return -((m-n+1)//2)
```

4. n个数字组成的数组 nums，有 1-m 个数字，找到 nums 中包含 1-m 所有数字的最小子数组的长度。 nums 由 1-m 和 0 组成，如果没有这样的数组，返回 -1。

思路： 设置 dp 存储每个数字在当前区域内出现的次数， left，right 分别表示区域的左右边界，cnt 记录当前区域内不重复的数字的个数。 只需要考虑 > 0 的数字，0 可以直接略过。

- 当 cnt < m 时，区间需要向右扩张，right + 1
- 当 cnt = m 时，说明此时区间已经包含 1-m 的所有数字，可以开始收缩，left + 1

注意最后 left 和 right 指向的是区间的边界 + 1，长度是 right-left+1

```python
import sys

def function(n, m, nums):
    res = n + 1
    cnt = 0
    dp = [0] * m
    left = right = 0
    while right < len(nums):
        while cnt < m and right < len(nums):
            if nums[right] > 0:
                if dp[nums[right]-1] == 0:
                    cnt += 1
                dp[nums[right]-1] += 1
            right += 1
        while cnt >= m and left <= right:
            if nums[left] > 0:
                dp[nums[left]-1] -= 1
                if dp[nums[left]-1] == 0:
                    cnt -= 1
            left += 1
        res = min(res, right-left+1)
    return -1 if res == n + 1 else res

if __name__ == "__main__":
    line1 = sys.stdin.readline().strip()
    a = list(map(int, line1.split()))
    n = int(a[0])
    m = int(a[1])

    line2 = sys.stdin.readline().strip()
    b = list(map(int, line2.split()))
    nums = [int(b[i]) for i in range(len(b))]
```