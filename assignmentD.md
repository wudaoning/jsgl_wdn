# Assignment #D: 十全十美 

Updated 1254 GMT+8 Dec 17, 2024

2024 fall, Complied by <mark>吴道宁 元培学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 02692: 假币问题

brute force, http://cs101.openjudge.cn/practice/02692

思路：



代码：

```python
n=int(input())
for i in range(n):
    s=[[],[],[]]
    for j in range(3):
        s[j]=input().split()
    for l in 'ABCDEFGHIJKL':
        if all((l in j[0] and j[2]=='up') or (l in j[1] and j[2]=='down') or (l not in j[0]+j[1] and j[2]=='even') for j in s):
            print(f'{l} is the counterfeit coin and it is heavy.')
            break
        if all((l in j[0] and j[2]=='down') or (l in j[1] and j[2]=='up') or (l not in j[0]+j[1] and j[2]=='even') for j in s):
            print(f'{l} is the counterfeit coin and it is light.')
            break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241217140328833](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241217140328833.png)



### 01088: 滑雪

dp, dfs similar, http://cs101.openjudge.cn/practice/01088

思路：



代码：

```python
r,c=map(int,input().split())
region=[list(map(int,input().split())) for _ in range(r)]
directions=[(0,1),(0,-1),(1,0),(-1,0)]
dp=[[0]*c for _ in range(r)]
def dfs(x,y):
    global dp
    if dp[x][y]>0:
        return dp[x][y]
    for dx,dy in directions:
        nx=x+dx
        ny=y+dy
        if 0<=nx<=r-1 and 0<=ny<=c-1:
            if region[x][y]>region[nx][ny]:
                dp[x][y]=max(dp[x][y],dfs(nx,ny)+1)
    return dp[x][y]
ans=0
for i in range(r):
    for j in range(c):
        ans=max(ans,dfs(i,j))
print(ans+1)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241217173728513](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241217173728513.png)



### 25572: 螃蟹采蘑菇

bfs, dfs, http://cs101.openjudge.cn/practice/25572/

思路：



代码：

```python
from collections import deque
n=int(input())
maze=[list(map(int,input().split())) for _ in range(n)]
crab=[]
for i in range(n):
    for j in range(n):
        if maze[i][j]==5:
            crab.append((i,j))
if crab[0][0]==crab[1][0]:
    cd=(0,1)
else:
    cd=(1,0)
start=crab[0]
directions=[(0,1),(0,-1),(1,0),(-1,0)]
def bfs(start,cd):
    q=deque()
    q.append(start)
    inq=set()
    inq.add(start)
    while q:
        for _ in range(len(q)):
            x,y=q.popleft()
            if maze[x][y]==9 or maze[x+cd[0]][y+cd[1]]==9:
                return 'yes'
            for dx,dy in directions:
                nx=x+dx
                ny=y+dy
                if 0<=nx<=n-1 and 0<=ny<=n-1 and 0<=nx+cd[0]<=n-1 and 0<=ny+cd[1]<=n-1 and (nx,ny) not in inq and maze[nx][ny]!=1 and maze[nx+cd[0]][ny+cd[1]]!=1:
                    q.append((nx,ny))
                    inq.add((nx,ny))
    return 'no'
print(bfs(start,cd))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241217140722443](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241217140722443.png)



### 27373: 最大整数

dp, http://cs101.openjudge.cn/practice/27373/

思路：这题的排序部分和12559最大最小整数一样，用一个冒泡排序就可以了，后面就是一个0-1背包，使用滚动数组方法，因为int('')会出现错误，所以在dp里面的每个元素前面都加一个0，输出的时候再去掉



代码：

```python
m=int(input())
n=int(input())
l=list(input().split())
for i in range(n-1):
    for j in range(n-i-1):
        if l[j+1]+l[j]>l[j]+l[j+1]:
            l[j],l[j+1]=l[j+1],l[j]
w=[len(l[i]) for i in range(n)]
dp=['0']*(m+1)
for i in range(n):
    for j in range(m,w[i]-1,-1):
        dp[j]='0'+str(max(int(dp[j]),int(dp[j-w[i]]+l[i])))
print(dp[-1][1:])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241217170658852](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241217170658852.png)



### 02811: 熄灯问题

brute force, http://cs101.openjudge.cn/practice/02811

思路：



代码：

```python
from itertools import product
from copy import deepcopy
change={0:1,1:0}
m0=[[0,0,0,0,0,0,0,0]]
for _ in range(5):
    m0.append([0]+[int(x) for x in input().split()]+[0])
m0.append([0,0,0,0,0,0,0,0])
for t in product(range(2),repeat=6):
    m=deepcopy(m0)
    answer=[list(t)]
    for i in range(1,6):
        for j in range(1,7):
            if answer[i-1][j-1]:
                m[i][j]=change[m[i][j]]
                m[i-1][j]=change[m[i-1][j]]
                m[i+1][j]=change[m[i+1][j]]
                m[i][j-1]=change[m[i][j-1]]
                m[i][j+1]=change[m[i][j+1]]
        answer.append(m[i][1:7])
    if m[5][1:7]==[0,0,0,0,0,0]:
        for a in answer[:-1]:
            print(' '.join(map(str,a)))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241217140812404](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241217140812404.png)



### 08210: 河中跳房子

binary search, greedy, http://cs101.openjudge.cn/practice/08210/

思路：类似aggressive cows



代码：

```python
l,n,m=map(int,input().split())
rock=[0]+[int(input()) for _ in range(n)]+[l]
def can_reach(d):
    count=0
    cur=rock[0]
    for i in range(1,n+2):
        if rock[i]-cur<d:
            count+=1
        else:
            cur=rock[i]
    return count<=m

def binary_search():
    low=0
    high=l
    while low<=high:
        mid=(low+high)//2
        if can_reach(mid):
            low=mid+1
        else:
            high=mid-1
    return high
print(binary_search())
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241217181220344](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241217181220344.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

现在在复习之前做的题目和学习的内容，cheat sheet也在做。



