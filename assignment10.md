# Assignment #10: dp & bfs

Updated 2 GMT+8 Nov 25, 2024

2024 fall, Complied by <mark>吴道宁 元培学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### LuoguP1255 数楼梯

dp, bfs, https://www.luogu.com.cn/problem/P1255

思路：和flowers那个题k=2情况一样，但这个题直接用组合数算就能AC



代码：

```python
import math
n=int(input())
a=n//2
ans=0
for i in range(a+1):
    j=n-2*i
    ans+=math.comb(i+j,i)
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241126084037952](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241126084037952.png)



### 27528: 跳台阶

dp, http://cs101.openjudge.cn/practice/27528/

耗时：<5min



代码：

```python
n=int(input())
dp=[0]*(n+1)
dp[0]=1
for i in range(1,n+1):
    for j in range(1,i+1):
        dp[i]+=dp[i-j]
print(dp[-1])
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241126084850842](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241126084850842.png)



### 474D. Flowers

dp, https://codeforces.com/problemset/problem/474/D

思路：一开始对每个数量的花用组合数算吃的方式结果超时了，后来改成dp就可以了



代码：

```python
m=10**9+7
t,k=map(int,input().split())
al=[]
bl=[]
for _ in range(t):
    a,b=map(int,input().split())
    al.append(a)
    bl.append(b)
max_bl=max(bl)
l=[0]*(max_bl+1)
l[0]=1
for i in range(1,max_bl+1):
    if i>=k:
        l[i]=(l[i-k]+l[i-1])%m
    else:
        l[i]=1
suml=[0]*(max_bl+1)
for i in range(1,max_bl+1):
    suml[i]=(suml[i-1]+l[i])%m
for i in range(t):
    print((suml[bl[i]]-suml[al[i]-1]+m)%m)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241126082709786](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241126082709786.png)



### LeetCode5.最长回文子串

dp, two pointers, string, https://leetcode.cn/problems/longest-palindromic-substring/

思路：以一个位置或两个位置为中心向两边扩展（分回文子串长度为奇数和偶数两种情况）



代码：

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        x=1
        ans=s[0]
        n=len(s)
        for i in range(1,n-1):
            j=0
            while True:
                if i-j>=1 and i+j<=n-2 and s[i-j-1]==s[i+j+1]:
                    j+=1
                else:
                    break
            if 2*j+1>x:
                x=2*j+1
                ans=s[i-j:i+j+1]
        for i in range(0,n-1):
            if s[i]==s[i+1]:
                j=0
                while True:
                    if i-j>=1 and i+1+j<=n-2 and s[i-j-1]==s[i+j+2]:
                        j+=1
                    else:
                        break
                if 2*j+2>x:
                    x=2*j+2
                    ans=s[i-j:i+j+2]
        return ans
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241126091106329](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241126091106329.png)





### 12029: 水淹七军

bfs, dfs, http://cs101.openjudge.cn/practice/12029/

思路：淹过的点高度改成水深



代码：

```python
import sys
from collections import deque
input=sys.stdin.read

dx=[0,0,1,-1]
dy=[1,-1,0,0]
                  
data=input().split()
result=[]
k=int(data[0])
idx=1
for _ in range(k):
    m,n=map(int,data[idx:idx+2])
    idx+=2
    maph=[]
    for i in range(m):
        maph.append(list(map(int,data[idx:idx+n])))
        idx+=n
    ans=[[0]*n for _ in range(m)]
    I,J=map(int,data[idx:idx+2])
    I-=1
    J-=1
    idx+=2
    p=int(data[idx])
    idx+=1
    for _ in range(p):
        x,y=map(int,data[idx:idx+2])
        x-=1
        y-=1
        idx+=2
        if maph[x][y]>maph[I][J]:
            q=deque()
            q.append((x,y))
            while q:
                for _ in range(len(q)):
                    cx,cy=q.popleft()
                    for i in range(4):
                        nx=cx+dx[i]
                        ny=cy+dy[i]
                        if 0<=nx<=m-1 and 0<=ny<=n-1:
                            if maph[nx][ny]<maph[x][y]:
                                maph[nx][ny]=maph[x][y]
                                q.append((nx,ny))
                                ans[nx][ny]=1
    if ans[I][J]==1:
            result.append('Yes')
    else:
        result.append('No')
sys.stdout.write('\n'.join(result)+'\n')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241126163457310](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241126163457310.png)



### 02802: 小游戏

bfs, http://cs101.openjudge.cn/practice/02802/

思路：



代码：

```python
from collections import deque
dx=[0,0,1,-1]
dy=[1,-1,0,0]
board_i=1
while True:
    w,h=map(int,input().split())
    if w==0:
        break
    board=[' '*(w+2)]
    for _ in range(h):
        board.append(' '+str(input())+' ')
    board.append(' '*(w+2))
    print(f'Board #{board_i}:')
    pair_i=1
    while True:
        x1,y1,x2,y2=map(int,input().split())
        if x1==0:
            break
        q=deque()
        inq=set()
        q.append((x1,y1,-1,0))
        ans=[]
        while q:
            x,y,direction,seg=q.popleft()
            for i in range(4):
                nx=x+dx[i]
                ny=y+dy[i]
                if 0<=nx<=w+1 and 0<=ny<=h+1 and (nx,ny,i) not in inq:
                    if i!=direction:
                        nseg=seg+1
                    else:
                        nseg=seg
                    if (nx,ny)==(x2,y2):
                        ans.append(nseg)
                        continue
                    if board[ny][nx]==' ':
                        inq.add((nx,ny,i))
                        q.append((nx,ny,i,nseg))
        if len(ans)==0:
            print(f'Pair {pair_i}: impossible.')
        else:
            print(f'Pair {pair_i}: {min(ans)} segments.')
        pair_i+=1
    print()
    board_i+=1
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241126172002965](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241126172002965.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

每日选做基本都做完了，印象比较深的是接雨水，学会了双指针和单调栈两种方法。没事的时候会看看算法图解，现在基本看完了，对递归和栈的关系、字典（散列表）、快速排序、bfs有了更直观的理解，也学到了dijkstra算法。这次作业水淹七军一直RE，花了很长时间才AC，其他的题感觉还可以。
