# Assignment #6: Recursion and DP

Updated 2201 GMT+8 Oct 29, 2024

2024 fall, Complied by <mark>吴道宁 元培学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### sy119: 汉诺塔

recursion, https://sunnywhy.com/sfbj/4/3/119  

思路：主要是学习了一下答案



代码：

```python
def move(n,s,t,m):
    global cnt;ans
    if n==1:
        cnt+=1
        ans.append(f'{s}->{t}')
    else:
        move(n-1,s,m,t)
        move(1,s,t,m)
        move(n-1,m,t,s)
n=int(input())
cnt=0
ans=[]
move(n,'A','C','B')
print(cnt)
print('\n'.join(ans))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241104182805481](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241104182805481.png)



### sy132: 全排列I

recursion, https://sunnywhy.com/sfbj/4/3/132

思路：主要是学习了一下答案



代码：

```python
l=[]
def function(s,n):
    if len(s)==n:
        l.append(s)
        return
    for i in range(1,n+1):
        if str(i) not in s:
            function(s+str(i),n)
n=int(input())
function('',n)
for j in l:
    print(' '.join(j))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241104201103898](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241104201103898.png)



### 02945: 拦截导弹 

dp, http://cs101.openjudge.cn/2024fallroutine/02945

耗时：较短



代码：

```python
k=int(input())
h=list(map(int,input().split()))
dp=[1]*k
for i in range(1,k):
    for j in range(i):
        if h[i]<=h[j]:
            dp[i]=max(dp[i],dp[j]+1)
print(max(dp))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241104204105795](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241104204105795.png)



### 23421: 小偷背包 

dp, http://cs101.openjudge.cn/practice/23421

耗时：较短



代码：

```python
n,b=map(int,input().split())
p=[0]+[int(i) for i in input().split()]
w=[0]+[int(i) for i in input().split()]
dp=[[0]*(b+1) for _ in range(n+1)]
for i in range(1,n+1):
    for j in range(1,b+1):
        if w[i]<=j:
            dp[i][j]=max(p[i]+dp[i-1][j-w[i]],dp[i-1][j])
        else:
            dp[i][j]=dp[i-1][j]
print(dp[-1][-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241104205755935](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241104205755935.png)



### 02754: 八皇后

dfs and similar, http://cs101.openjudge.cn/practice/02754

思路：在全排列代码的基础上加一个判断不在斜线上就可以了



代码：

```python
l=[]
def function(s,n):
    if len(s)==n:
        l.append(s)
        return
    for i in range(1,n+1):
        if str(i) not in s and all(len(s)-j!=abs(i-int(s[j])) for j in range(len(s))):
            function(s+str(i),n)
function('',8)
for k in range(int(input())):
    print(l[int(input())-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241104201941254](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241104201941254.png)



### 189A. Cut Ribbon 

brute force, dp 1300 https://codeforces.com/problemset/problem/189/A

耗时：较短



代码：

```python
n,a,b,c=map(int,input().split())
l=[a,b,c]
dp=[0]*(n+1)
for i in range(3):
    if n>=l[i]:
        dp[l[i]]=1
for i in range(1,n+1):
    for j in range(3):
        if i>=l[j] and dp[i-l[j]]>=1:
            dp[i]=max(dp[i],dp[i-l[j]]+1)
print(dp[-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241104212220597](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241104212220597.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

上周因为在准备期中，所以每日选做基本只做到了dp era之前。感觉之前在一些题目中已经用到dp的思想了，所以上手起来比较容易也感觉比较自然。递归的题主要是学习了一下答案，也看了群里分享的一些文章。之前我其实不怎么使用函数，这次作业学会了用函数实现递归以及什么是全局变量。这周准备补一下之前的每日选做。



