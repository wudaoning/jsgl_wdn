# Assignment #5: Greedy穷举Implementation

Updated 1939 GMT+8 Oct 21, 2024

2024 fall, Complied by <mark>吴道宁 元培学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 04148: 生理周期

brute force, http://cs101.openjudge.cn/practice/04148

耗时：15min



代码：

```python
n=1
while True:
    p,e,i,d=map(int,input().split())
    if {p,e,i,d}=={-1}:
        break
    p%=23
    e%=28
    i%=33
    x=d+1
    while (x-p)%23!=0 or (x-e)%28!=0 or (x-i)%33!=0:
        x+=1
    x-=d
    print(f'Case {n}: the next triple peak occurs in {x} days.')
    n+=1
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241022134217347](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241022134217347.png)



### 18211: 军备竞赛

greedy, two pointers, http://cs101.openjudge.cn/practice/18211

耗时：10min



代码：

```python
p=int(input())
l=list(map(int,input().split()))
n=len(l)
l.sort()
i=0
j=n-1
x=0
while i<j:
    if l[i]<=p:
        p-=l[i]
        i+=1
        x+=1
        continue
    if l[i]>p and x>=1:
        p+=l[j]
        j-=1
        x-=1
        continue
    break
if i==j and l[i]<=p:
    x+=1
print(x)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241022134053602](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241022134053602.png)



### 21554: 排队做实验

greedy, http://cs101.openjudge.cn/practice/21554

耗时：<10min



代码：

```python
n=int(input())
l=list(map(int,input().split()))
l2=[]
for i in range(n):
    l2.append([i+1,l[i]])
l2.sort(key=lambda x: x[1])
l3=[j[0] for j in l2]
print(*l3)
sumt=0
for i in range(n):
    sumt+=(n-1-i)*l2[i][1]
print(f'{sumt/n:.2f}')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241022140509602](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241022140509602.png)



### 01008: Maya Calendar

implementation, http://cs101.openjudge.cn/practice/01008/

耗时：较长。有一些细节出了问题（比如一开始复制月份的名称时把最后一个复制漏了），导致第四次交才AC



代码：

```python
n=int(input())
l1=['pop','no','zip','zotz','tzec','xul','yoxkin','mol','chen','yax','zac','ceh','mac','kankin','muan','pax','koyab','cumhu','uayet']
l2=['imix','ik','akbal','kan','chicchan','cimi','manik','lamat','muluk','ok','chuen','eb','ben','ix','mem','cib','caban','eznab','canac','ahau']
print(n)
for _ in range(n):
    d,m,y=input().split()
    d=int(d[:-1])
    y=int(y)
    n=365*y+l1.index(m)*20+d+1
    if (n%260)%13==0:
        d2=13
    else:
        d2=(n%260)%13
    print(str(d2)+' '+l2[(n%260)%20-1]+' '+str((n-1)//260))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241022133752343](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241022133752343.png)



### 545C. Woodcutters

dp, greedy, 1500, https://codeforces.com/problemset/problem/545/C

思路：让树尽量往左倒，不能往左倒就尽量往右倒

耗时：10min



代码：

```python
n=int(input())
l=[]
for _ in range(n):
    l.append(list(map(int,input().split())))
if n==1:
    print(1)
else:
    ans=2
    for i in range(1,n-1):
        if l[i][0]-l[i-1][0]>l[i][1]:
            ans+=1
        elif l[i+1][0]-l[i][0]>l[i][1]:
            ans+=1
            l[i][0]+=l[i][1]
    print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### 01328: Radar Installation

greedy, http://cs101.openjudge.cn/practice/01328/

思路：对于每个岛算出能探测到它的雷达的位置范围，剩下的同进程检测

耗时：15min



代码：

```python
r=1
while True:
    n,d=map(int,input().split())
    if n==0 and d==0:
        break
    l=[]
    for _ in range(n):
        x,y=map(int,input().split())
        if y<=d:
            l.append([x-(d*d-y*y)**0.5,x+(d*d-y*y)**0.5])
    if len(l)<n:
        ans=-1
    else:
        l.sort(key=lambda x: x[0])
        d=l[0][1]
        ans=1
        for i in range(1,n):
            if l[i][0]<=d:
                if l[i][1]<d:
                    d=l[i][1]
            else:
                d=l[i][1]
                ans+=1
    print(f'Case {r}: {ans}')
    r+=1
    input()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241022133314204](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241022133314204.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

完成了每日选做。

进一步练习贪心的题目，学习了用贪心解决五类区间问题。

在处理日期类问题时经常因为一些细节处理不当WA或者RE（比如n正好是一年天数m的k倍时应该是第k-1年的最后一天，所以应该用(n-1)//m而不是n//m），争取以后一次性AC

