# Assignment #9: dfs, bfs, & dp

Updated 2107 GMT+8 Nov 19, 2024

2024 fall, Complied by <mark>吴道宁 元培学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 18160: 最大连通域面积

dfs similar, http://cs101.openjudge.cn/practice/18160

思路：在lake counting的基础上改了一下



代码：

```python
t=int(input())
for _ in range(t):
    n,m=map(int,input().split())
    l=[list(input()) for _ in range(n)]
    direction=[(-1,-1),(-1,0),(-1,1),(0,-1),(0,1),(1,-1),(1,0),(1,1)]
    ans=0
    def dfs(x,y):
        count=0
        stack=[(x,y)]
        while stack:
            x,y=stack.pop()
            if l[x][y]=='.':
                continue
            count+=1
            l[x][y]='.'
            for dirx,diry in direction:
                dx=x+dirx
                dy=y+diry
                if dx>=0 and dx<=n-1 and dy>=0 and dy<=m-1 and l[dx][dy]=='W':
                    stack.append((dx,dy))
        return(count)
    for i in range(n):
        for j in range(m):
            if l[i][j]=='W':
                ans=max(ans,dfs(i,j))
    print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241119213832859](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241119213832859.png)



### 19930: 寻宝

bfs, http://cs101.openjudge.cn/practice/19930

思路：注意要单独判断起点是不是1（WA了好几次）



代码：

```python
from collections import deque
dx=[0,0,1,-1]
dy=[1,-1,0,0]

def bfs(x,y):
    if matrix[x][y]==1:
        return 0
    inq.add((x,y))
    q=deque()
    q.append((x,y))
    step=0
    while q:
        for _ in range(len(q)):
            front=q.popleft()
            for i in range(4):
                nx=front[0]+dx[i]
                ny=front[1]+dy[i]
                if matrix[nx][ny]==1:
                    return step+1
                if matrix[nx][ny]==0 and (nx,ny) not in inq:
                    inq.add((nx,ny))
                    q.append((nx,ny))
        step+=1
    return 'NO'

m,n=map(int,input().split())
matrix=[[-1]*(n+2)]+[[-1]+list(map(int,input().split()))+[-1] for _ in range(m)]+[[-1]*(n+2)]
inq=set()
print(bfs(1,1))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241120124719962](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241120124719962.png)



### 04123: 马走日

dfs, http://cs101.openjudge.cn/practice/04123

思路：dfs+回溯 把经过的点放到一个集合used里面，当集合元素数量达到m*n时ans+1



代码：

```python
direction=[(-2,-1),(-2,1),(-1,-2),(-1,2),(1,-2),(1,2),(2,-1),(2,1)]
ans=0
def dfs(x,y,n,m):
    global ans
    if len(used)==m*n:
        ans+=1
        return
    for dirx,diry in direction:
        dx=x+dirx
        dy=y+diry
        if dx>=0 and dx<=n-1 and dy>=0 and dy<=m-1 and (dx,dy) not in used:
            used.add((dx,dy))
            dfs(dx,dy,n,m)
            used.remove((dx,dy))
            
t=int(input())
for _ in range(t):
    ans=0
    n,m,x,y=map(int,input().split())
    used=set()
    used.add((x,y))
    dfs(x,y,n,m)
    print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241120145610024](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241120145610024.png)



### sy316: 矩阵最大权值路径

dfs, https://sunnywhy.com/sfbj/8/1/316

思路：dfs+回溯 l为每次的路径，若此次的权值之和count大于之前最大的num，则将ans更新为l，注意这里需要使用深拷贝



代码：

```python
import copy
direction=[(0,1),(0,-1),(1,0),(-1,0)]
n,m=map(int,input().split())
matrix=[list(map(int,input().split())) for _ in range(n)]
num=float('-inf')
ans=[]
count=matrix[0][0]
used=set()
used.add((0,0))
l=[[1,1]]
def dfs(x,y):
    global num,count,ans,l
    if x==n-1 and y==m-1:
        if count>num:
            num=count
            ans=copy.deepcopy(l)
        return
    for dirx,diry in direction:
        dx=x+dirx
        dy=y+diry
        if dx>=0 and dx<=n-1 and dy>=0 and dy<=m-1 and (dx,dy) not in used:
            used.add((dx,dy))
            count+=matrix[dx][dy]
            l.append([dx+1,dy+1])
            dfs(dx,dy)
            used.remove((dx,dy))
            count-=matrix[dx][dy]
            l.pop()
dfs(0,0)
for i in ans:
    print(*i)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241120155325490](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241120155325490.png)





### LeetCode62.不同路径

dp, https://leetcode.cn/problems/unique-paths/

耗时：较短



代码：

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp=[[1]*n for _ in range(m)]
        for i in range(1,m):
            for j in range(1,n):
                dp[i][j]=dp[i-1][j]+dp[i][j-1]
        return dp[-1][-1]
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241119211647053](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241119211647053.png)



### sy358: 受到祝福的平方

dfs, dp, https://sunnywhy.com/sfbj/8/3/539

思路：dfs，用了is_integer()函数，要是把小于等于a的完全平方数都算出来会超时



代码：

```python
from math import sqrt
a=int(input())
s=str(a)
def dfs(s):
    if sqrt(int(s)).is_integer() and sqrt(int(s))!=0:
        return True
    for i in range(1,len(s)):
        if sqrt(int(s[:i])).is_integer() and sqrt(int(s[:i]))!=0:
            if dfs(s[i:]):
                return True
    return False
if dfs(s):
    print('Yes')
else:
    print('No')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241120171134012](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241120171134012.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

每日选做中OJ的题目都做完了，学会了kadane算法、mergesort等。此外还做了些课件里面搜索的题目，大概掌握了dfs和bfs的模板写法。一般连通面积、路径数量、能否达到类的问题用dfs，路径类的需要进行回溯；最短路径用bfs。现在写dp的题目比较顺，但有时候会超时；搜索还不太熟练，经常不能一次性ac，还需要多练习。后续也准备做些leetcode上的题。



