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

