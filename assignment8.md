# Assignment #8: 田忌赛马来了

Updated 1021 GMT+8 Nov 12, 2024

2024 fall, Complied by <mark>吴道宁 元培学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 12558: 岛屿周⻓

matices, http://cs101.openjudge.cn/practice/12558/ 

耗时：<10min



代码：

```python
n,m=map(int,input().split())
l=[[0]*(m+2)]
for _ in range(n):
    l.append([0]+list(map(int,input().split()))+[0])
l.append([0]*(m+2))
ans=0
for i in range(1,n+1):
    for j in range(1,m+1):
        if l[i][j]==1:
            ans+=4-l[i-1][j]-l[i+1][j]-l[i][j-1]-l[i][j+1]
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241113133609486](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241113133609486.png)



### LeetCode54.螺旋矩阵

matrice, https://leetcode.cn/problems/spiral-matrix/

与OJ这个题目一样的 18106: 螺旋矩阵，http://cs101.openjudge.cn/practice/18106

耗时：10min（做的OJ上的题）



代码：

```python
n=int(input())
l=[[0]*n for _ in range(n)]
direction=[[1,0],[0,1],[-1,0],[0,-1]]
d=0
x=0
y=0
l[0][0]=1
for i in range(2,n*n+1):
    if x+direction[d][1]>=n or y+direction[d][0]>=n:
        d=(d+1)%4
    else:
        if l[x+direction[d][1]][y+direction[d][0]]!=0:
            d=(d+1)%4
    x+=direction[d][1]
    y+=direction[d][0]
    l[x][y]=i
for j in range(n):
    print(*l[j])
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241113153643389](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241113153643389.png)



### 04133:垃圾炸弹

matrices, http://cs101.openjudge.cn/practice/04133/

耗时：做的早记不清了，主要就是上课讲的range里面用min和max



代码：

```python
d=int(input())
n=int(input())
board=[[0]*1025 for _ in range(1025)]
for _ in range(n):
    x,y,k=map(int,input().split())
    for i in range(max(0,x-d),min(1025,x+d+1)):
        for j in range(max(0,y-d),min(1025,y+d+1)):
            board[i][j]+=k
maxk=max(max(l) for l in board)
num=sum(l.count(maxk) for l in board)
print(num,maxk)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241113120213466](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241113120213466.png)



### LeetCode376.摆动序列

greedy, dp, https://leetcode.cn/problems/wiggle-subsequence/

与OJ这个题目一样的，26976:摆动序列, http://cs101.openjudge.cn/routine/26976/

耗时：10min（做的OJ上的题）



代码：

```python
n=int(input())
nums=list(map(int,input().split()))
def sgn(x):
    if x==0:
        return 0
    elif x>0:
        return 1
    else:
        return -1
delta=[sgn(nums[i+1]-nums[i]) for i in range(n-1)]
ans=1
sign=0
for i in range(n-1):
    if delta[i]*sign<0 or (sign==0 and delta[i]!=0):
        ans+=1
        sign=delta[i]
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241113155434808](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241113155434808.png)



### CF455A: Boredom

dp, 1500, https://codeforces.com/contest/455/problem/A

耗时：较短



代码：

```python
n=int(input())
a=list(map(int,input().split()))
dp=[0]*(max(a)+1)
count=[0]*(max(a)+1)
for ai in a:
    count[ai]+=1
dp[1]=count[1]
for i in range(2,max(a)+1):
    dp[i]=max(dp[i-1],dp[i-2]+i*count[i])
print(dp[-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241113120459770](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241113120459770.png)



### 02287: Tian Ji -- The Horse Racing

greedy, dfs http://cs101.openjudge.cn/practice/02287

耗时：较长，双指针是比较好想到的，两个马速度一样的情形不太好处理，题解里面的比较顺序解决了这个问题



代码：

```python
while True:
    n=int(input())
    if n==0:
        break
    tian=list(map(int,input().split()))
    king=list(map(int,input().split()))
    tian.sort()
    king.sort()
    it=0
    jt=n-1
    ik=0
    jk=n-1
    ans=0
    while it<=jt:
        if tian[it]>king[ik]:
            ans+=1
            it+=1
            ik+=1
        elif tian[jt]>king[jk]:
            ans+=1
            jt-=1
            jk-=1
        else:
            if tian[it]<king[jk]:
                ans-=1
            it+=1
            jk-=1
    print(ans*200)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241113164424731](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241113164424731.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

补了一些每日选做，主要是继续练习递归和dp。看了算法图解中递归的部分，



