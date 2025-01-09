# Assignment #B: Dec Mock Exam大雪前一天

Updated 1649 GMT+8 Dec 5, 2024

2024 fall, Complied by <mark>吴道宁 元培学院</mark>



**说明：**

1）⽉考： AC2 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E22548: 机智的股民老张

http://cs101.openjudge.cn/practice/22548/

思路：start为当前最小的，end为当前最小的之后的最大的，每次end更新后计算新的end-start并与之前的ans比较取其中较大的那个



代码：

```python
a=list(map(int,input().split()))
n=len(a)
ans=0
start=a[0]
end=a[0]
temp=0
for i in range(1,n):
    if a[i]>end:
        end=a[i]
        temp=end-start
        ans=max(ans,temp)
    if a[i]<start:
        start=a[i]
        end=a[i]
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241206101218181](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241206101218181.png)



### M28701: 炸鸡排

greedy, http://cs101.openjudge.cn/practice/28701/

思路：这个题考试的时候一下子就想到了。理想情况下为锅里每个位置都炸sum(t)/k时间（记为平均时间avg），但如果需要时间最长的鸡排需要的时间长于这个平均时间，那这个情况就无法实现。现在最好的选择就是把这个鸡排放在一个位置一直炸，然后剩下的位置再算avg（(sum(t)-t[0])/(k-1)）（其中t已经按从大到小排序），然后把次大的t和avg比较，以此类推。如果一个t比此时的avg小了，那就结束循环。答案就是最终的avg



代码：

```python
n,k=map(int,input().split())
t=list(map(int,input().split()))
t.sort(reverse=True)
total=sum(t)
for i in range(k):
    avg=total/(k-i)
    total-=t[i]
    if t[i]<=avg:
        break
print(f'{avg:.3f}')
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241206101546732](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241206101546732.png)



### M20744: 土豪购物

dp, http://cs101.openjudge.cn/practice/20744/

思路：考试的时候因为是第二个题，还没有数据大小，所以就暴力方法写的，结果超时了。后面想到要用dp，但可以放回一个比较难处理。题解里弄两个dp数组，一个不放回，一个可以放回一个还是很巧妙的



代码：

```python
w=list(map(int,input().split(',')))
n=len(w)
dp1=[0]*n
dp2=[0]*n
dp1[0]=w[0]
dp2[0]=w[0]
for i in range(1,n):
    dp1[i]=max(dp1[i-1]+w[i],w[i])
    dp2[i]=max(dp1[i-1],dp2[i-1]+w[i],w[i])
print(max(dp2))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241206104422357](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241206104422357.png)



### T25561: 2022决战双十一

brute force, dfs, http://cs101.openjudge.cn/practice/25561/

思路：暴力枚举每种组合



代码：

```python
n,m=map(int,input().split())
prices=[input().split() for _ in range(n)]
coupons=[input().split() for _ in range(m)]
ans=float('inf')
item=0
total=0
store=[0]*m
def dfs(item,total,store):
    global ans
    if item==n:
        total_coupon=0
        for i in range(m):
            store_coupon=0
            for coupon in coupons[i]:
                a,b=map(int,coupon.split('-'))
                if store[i]>=a:
                    store_coupon=max(store_coupon,b)
            total_coupon+=store_coupon
        ans=min(ans,total-(total//300)*50-total_coupon)
        return
    for price in prices[item]:
        a,b=map(int,price.split(':'))
        store[a-1]+=b
        dfs(item+1,total+b,store)
        store[a-1]-=b
dfs(item,total,store)
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241206174252638](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241206174252638.png)



### T20741: 两座孤岛最短距离

dfs, bfs, http://cs101.openjudge.cn/practice/20741/

思路：dfs+bfs 代码长了之后总在一些细节的地方出错，还是得多练



代码：

```python
from collections import deque

def dfs(x,y,l,q):
    l[x][y]=2
    q.append((x,y))
    for dx,dy in direction:
       nx=x+dx
       ny=y+dy
       if 0<=nx<=n-1 and 0<=ny<=n-1 and l[nx][ny]==1:
           dfs(nx,ny,l,q)

def bfs(l,q):
    ans=0
    while q:
        for _ in range(len(q)):
            x,y=q.popleft()
            for dx,dy in direction:
               nx=x+dx
               ny=y+dy
               if 0<=nx<=n-1 and 0<=ny<=n-1:
                   if l[nx][ny]==1:
                       return ans
                   elif l[nx][ny]==0:
                       l[nx][ny]=2
                       q.append((nx,ny))
        ans+=1
    return ans

n=int(input())
l=[list(map(int,input())) for _ in range(n)]
q=deque()
direction=[(1,0),(-1,0),(0,1),(0,-1)]
def solve():
    for i in range(n):
        for j in range(n):
            if l[i][j]==1:
                dfs(i,j,l,q)
                return bfs(l,q)
print(solve())
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241206112921481](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241206112921481.png)



### T28776: 国王游戏

greedy, http://cs101.openjudge.cn/practice/28776

思路：按照左右手数的乘积从小到大排序即可



代码：

```python
n=int(input())
a,b=map(int,input().split())
l=[]
for _ in range(n):
    l.append(list(map(int,input().split())))
l.sort(key=lambda x:(x[0]*x[1]))
product=a
ans=0
for i in range(n):
    ans=max(ans,product//l[i][1])
    product*=l[i][0]
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241206103136566](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241206103136566.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

月考在土豪购物上卡了一个多小时，搜索的两个题都没来得及写。感觉就是最好先在纸上写一下，想想有没有好的方法，想明白之后再开始写代码，要不然好不容易写出来了还容易超时。之前以为学的还可以了，所以上周没怎么练题，考完月考发现水平还是不行，还得多做点题。特别是搜索这种代码比较长的还是容易在一些细节的地方出错。



