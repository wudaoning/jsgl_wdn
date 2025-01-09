# Assignment #C: 五味杂陈 

Updated 1148 GMT+8 Dec 10, 2024

2024 fall, Complied by <mark>吴道宁 元培学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 1115. 取石子游戏

dfs, https://www.acwing.com/problem/content/description/1117/

思路：若a//b>=2，先手可以选择取(a//b)个b，也可以选择取(a//b-1)个b，此时后手只能取1个b，这两种情况下相当于二人互换处境，因此先手总能选择自己能赢的处境



代码：

```python
while True:
    a,b=map(int,input().split())
    if a==0:
        break
    i=1
    a,b=max(a,b),min(a,b)
    while a//b<2 and a!=b:
        a,b=b,a-b
        i+=1
    if i%2==1:
        print('win')
    else:
        print('lose')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241210164005591](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241210164005591.png)



### 25570: 洋葱

Matrices, http://cs101.openjudge.cn/practice/25570

思路：



代码：

```python
n=int(input())
m=[list(map(int,input().split())) for _ in range(n)]
ans=0
layer=n//2
for i in range(layer):
    suml=0
    for j in range(i,n-i):
        suml+=m[i][j]
        suml+=m[n-1-i][j]
    for j in range(i+1,n-i-1):
        suml+=m[j][i]
        suml+=m[j][n-1-i]
    ans=max(ans,suml)
if n%2==0:
    print(ans)
else:
    print(max(ans,m[n//2][n//2]))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241210122950921](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241210122950921.png)



### 1526C1. Potions(Easy Version)

greedy, dp, data structures, brute force, *1500, https://codeforces.com/problemset/problem/1526/C1

思路：



代码：

```python
import heapq
n=int(input())
a=list(map(int,input().split()))
health=0
consumed=[]
for ai in a:
    health+=ai
    heapq.heappush(consumed,ai)
    if health<0:
        health-=consumed[0]
        heapq.heappop(consumed)
print(len(consumed))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241210170800000](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241210170800000.png)



### 22067: 快速堆猪

辅助栈，http://cs101.openjudge.cn/practice/22067/

思路：



代码：

```python
pig=[]
pigmin=[]
while True:
    try:
        s=input().split()
        if s[0]=='pop':
            if pig:
                pig.pop()
                if pigmin:
                    pigmin.pop()
        elif s[0]=='min':
            if pigmin:
                print(pigmin[-1])
        else:
            new_pig=int(s[1])
            pig.append(new_pig)
            if not pigmin:
                pigmin.append(new_pig)
            else:
                pig_min=pigmin[-1]
                pigmin.append(min(pig_min,new_pig))
    except EOFError:
        break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241210123116099](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241210123116099.png)



### 20106: 走山路

Dijkstra, http://cs101.openjudge.cn/practice/20106/

思路：



代码：

```python
import heapq
directions=[(0,1),(0,-1),(1,0),(-1,0)]
def dijkstra(s1,s2,t1,t2):
    pq=[(0,s1,s2)]
    visited=set()
    distances=[[float('inf')]*n for _ in range(m)]
    distances[s1][s2]=0
    while pq:
        distance,x,y=heapq.heappop(pq)
        if x==t1 and y==t2:
            return distance
        if (x,y) in visited:
            continue
        visited.add((x,y))
        for dx,dy in directions:
            nx=x+dx
            ny=y+dy
            if 0<=nx<=m-1 and 0<=ny<=n-1 and matrix[nx][ny]!='#' and (nx,ny) not in visited:
                new_distance=distance+abs(int(matrix[nx][ny])-int(matrix[x][y]))
                if new_distance<distances[nx][ny]:
                    distances[nx][ny]=new_distance
                    heapq.heappush(pq,(new_distance,nx,ny))
    return 'NO'
m,n,p=map(int,input().split())
matrix=[list(input().split()) for _ in range(m)]
for _ in range(p):
    s1,s2,t1,t2=map(int,input().split())
    if matrix[s1][s2]=='#' or matrix[t1][t2]=='#':
        print('NO')
    else:
        print(dijkstra(s1,s2,t1,t2))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241210152358988](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241210152358988.png)



### 04129: 变换的迷宫

bfs, http://cs101.openjudge.cn/practice/04129/

思路：



代码：

```python
from collections import deque
directions=[(0,1),(0,-1),(1,0),(-1,0)]
def bfs(x,y):
    inq=set()
    inq.add((0,x,y))
    q=deque()
    q.append((0,x,y))
    while q:
        t,x,y=q.popleft()
        if maze[x][y]=='E':
            return t
        for dx,dy in directions:
            nx=x+dx
            ny=y+dy
            nt=(t+1)%k
            if 0<=nx<=r-1 and 0<=ny<=c-1 and (nt,nx,ny) not in inq and (maze[nx][ny]!='#' or nt==0):
                q.append((t+1,nx,ny))
                inq.add((nt,nx,ny))
    return 'Oop!'
                
T=int(input())
for _ in range(T):
    r,c,k=map(int,input().split())
    maze=[list(input()) for _ in range(r)]
    for i in range(r):
        for j in range(c):
            if maze[i][j]=='S':
                print(bfs(i,j))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241210173234822](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241210173234822.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

复习了一下dp的讲义，然后又练习了一些dp的题。做了22年和21年的机考题，都做的比较顺，23年的准备去机房做。最近搜索写的更顺了，不用参考之前的代码也能写出来了，一次性AC的也更多了。最近也做到了一些用堆的题。
