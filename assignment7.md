# Assignment #7: Nov Mock Exam立冬

Updated 1646 GMT+8 Nov 7, 2024

2024 fall, Complied by <mark>吴道宁 元培学院</mark>



**说明：**

1）⽉考： AC3。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E07618: 病人排队

sorttings, http://cs101.openjudge.cn/practice/07618/

耗时：<10min



代码：

```python
n=int(input())
l1=[]
l2=[]
for _ in range(n):
    idp,b=input().split()
    age=int(b)
    if age>=60:
        l1.append([age,idp])
    else:
        l2.append(idp)
l1.sort(key=lambda x:x[0],reverse=True)
for l in l1:
    print(l[1])
for l in l2:
    print(l)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241107192259558](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241107192259558.png)



### E23555: 节省存储的矩阵乘法

implementation, matrices, http://cs101.openjudge.cn/practice/23555/

耗时：10min



代码：

```python
n,m1,m2=map(int,input().split())
l1=[]
for _ in range(m1):
    l1.append(list(map(int,input().split())))
l2=[]
for _ in range(m2):
    l2.append(list(map(int,input().split())))
l3=[[0]*n for _ in range(n)]
for a in l1:
    for b in l2:
        if b[0]==a[1]:
            l3[a[0]][b[1]]+=a[2]*b[2]
for i in range(n):
    for j in range(n):
        if l3[i][j]!=0:
            c=[i,j,l3[i][j]]
            print(*c)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241107192358917](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241107192358917.png)



### M18182: 打怪兽 

implementation/sortings/data structures, http://cs101.openjudge.cn/practice/18182/

耗时：30min（中间出了些小问题查了挺长时间才查出来）



代码：

```python
nc=int(input())
for _ in range(nc):
    n,m,b=map(int,input().split())
    l=[]
    for i in range(n):
        l.append(list(map(int,input().split())))
    l.sort(key=lambda x:x[0])
    t=l[0][0]
    lt=[]
    r=0
    for s in l:
        if s[0]==t:
            lt.append(s[1])
            r+=1
        else:
            lt.sort(reverse=True)
            xt=0
            if len(lt)<=m:
                xt=sum(lt)
            else:
                for j in range(m):
                    xt+=lt[j]
            if xt>=b:
                print(t)
                break
            else:
                b-=xt
                t=s[0]
                lt=[s[1]]
                r+=1
    if r==n:
        lt.sort(reverse=True)
        xt=0
        if len(lt)<=m:
            xt=sum(lt)
        else:
            for j in range(m):
                xt+=lt[j]
        if xt>=b:
            print(t)
        else:
            print('alive')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241107192503672](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241107192503672.png)



### M28780: 零钱兑换3

dp, http://cs101.openjudge.cn/practice/28780/

耗时：很长时间



代码：

```python
n,m=map(int,input().split())
l=list(map(int,input().split()))
dp=[float('inf')]*(m+max(l))
for i in l:
    dp[i-1]=1
for j in range(m):
    if dp[j]!=float('inf'):
        for i in l:
            dp[j+i]=min(dp[j+i],dp[j]+1)
if dp[m-1]==float('inf'):
    print('-1')
else:
    print(dp[m-1])
```

代码（TLE，其实感觉和ac的代码差不多）：

```python
n,m=map(int,input().split())
l=list(map(int,input().split()))
dp=[-1]*m
for i in l:
    dp[i-1]=1
for j in range(m):
    for i in l:
        if j+1>i and dp[j-i]!=-1:
            if dp[j]==-1:
                dp[j]=dp[j-i]+1
            else:
                dp[j]=min(dp[j],dp[j-i]+1)
print(dp[m-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241107200218082](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241107200218082.png)



### T12757: 阿尔法星人翻译官

implementation, http://cs101.openjudge.cn/practice/12757

耗时：10min，考试后做的，字典偷懒复制了一下



代码：

```python
dic={"zero":0, "one":1, "two":2, "three":3, "four":4, "five":5, "six":6, "seven":7, "eight":8, "nine":9, "ten":10, "eleven":11, "twelve":12, "thirteen":13, "fourteen":14, "fifteen":15, "sixteen":16, "seventeen":17, "eighteen":18, "nineteen":19, "twenty":20, "thirty":30, "forty":40, "fifty":50, "sixty":60, "seventy":70, "eighty":80, "ninety":90, "hundred":100, "thousand":1000, "million":1000000}
l=list(input().split())
sign=1
if l[0]=='negative':
    sign=-1
    del l[0]
ans=0
x=0
for i in l:
    if i in ["thousand","million"]:
        ans+=x*dic[i]
        x=0
    elif i=="hundred":
        x*=100
    else:
        x+=dic[i]
ans+=x
ans*=sign
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241107192048507](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241107192048507.png)



### T16528: 充实的寒假生活

greedy/dp, cs10117 Final Exam, http://cs101.openjudge.cn/practice/16528/

耗时：20min



代码：

```python
n=int(input())
l=[-1]*61
for _ in range(n):
    a,b=map(int,input().split())
    l[b]=max(l[b],a)
dp=[0]*61
if l[0]==0:
    dp[0]=1
for i in range(1,61):
    if l[i]==-1:
        dp[i]=max(dp[i],dp[i-1])
    else:
        dp[i]=max(dp[i],dp[i-1],dp[l[i]-1]+1)
print(dp[60])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241107191836738](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241107191836738.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

每日选做补了一部分，周末接着补。

这次月考每个题都有思路，但考的比较寄。打怪兽那个题查一个小的bug查了挺长时间才查出来，然后零钱兑换那个题用dp写的但是一直超时。因为我感觉写出来了但没ac比较亏，所以就一直在想办法改它，结果到最后都没过，浪费了很多时间。下次机考的时候不能再在一个题上卡很长时间了。



