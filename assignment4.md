# Assignment #4: T-primes + 贪心

Updated 0337 GMT+8 Oct 15, 2024

2024 fall, Complied by 吴道宁 元培学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知9月19日导入选课名单后启用。**作业写好后，保留在自己手中，待9月20日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 34B. Sale

greedy, sorting, 900, https://codeforces.com/problemset/problem/34/B

耗时：5min



代码

```python
n,m=map(int,input().split())
l=list(map(int,input().split()))
l.sort()
x=0
for i in range(m):
    if l[i]>=0:
        break
    x=x+l[i]
print(-x)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241015082905339](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241015082905339.png)



### 160A. Twins

greedy, sortings, 900, https://codeforces.com/problemset/problem/160/A

耗时：5min



代码

```python
n=int(input())
l=list(map(int,input().split()))
l.sort(reverse=True)
s=sum(l)
a=0
for i in range(n):
    a=a+l[i]
    if a>(s/2):
        print(i+1)
        break
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241015083033909](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241015083033909.png)



### 1879B. Chips on the Board

constructive algorithms, greedy, 900, https://codeforces.com/problemset/problem/1879/B

耗时：<10min



代码

```python
t=int(input())
for i in range(t):
    n=int(input())
    a=list(map(int,input().split()))
    b=list(map(int,input().split()))
    amin=min(a)
    bmin=min(b)
    s1=n*amin+sum(b)
    s2=n*bmin+sum(a)
    print(min(s1,s2))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20241015084928276](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241015084928276.png)



### 158B. Taxi

*special problem, greedy, implementation, 1100, https://codeforces.com/problemset/problem/158/B

耗时：5min

思路：很像装箱子的那个题



代码

```python
import math
n=int(input())
s=list(map(int,input().split()))
x1=s.count(1)
x2=s.count(2)
x3=s.count(3)
x4=s.count(4)
if x2%2==0:
    x=x3+x4+(x2//2)
    if x1>x3:
        x+=math.ceil((x1-x3)/4)
else:
    x=x3+x4+(x2//2)+1
    if x1>x3+2:
        x+=math.ceil((x1-x3-2)/4)
print(x)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20241015085055468](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241015085055468.png)



### *230B. T-primes（选做）

binary search, implementation, math, number theory, 1300, http://codeforces.com/problemset/problem/230/B

耗时：10min（非常顺利，一遍就AC了）



代码

```python
import math
p=[0]*(10**6)
p[0]=1
for i in range(1,10**3):
    if p[i]==0:
        for j in range(2*i+1,10**6,i+1):
            p[j]=1
n=int(input())
l=list(map(int,input().split()))
for i in range(n):
    x=l[i]
    if math.sqrt(x)%1!=0:
        print('NO')
    else:
        y=int(math.sqrt(x))
        if p[y-1]==0:
            print('YES')
        else:
            print('NO')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20241015085256977](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241015085256977.png)



### *12559: 最大最小整数 （选做）

greedy, strings, sortings, http://cs101.openjudge.cn/practice/12559

思路1：把每个数都补到同样的位数（max_len*2）（比如123补到七位是1231231），按大小排序

耗时：较长，因为一开始没有用元素为数组的列表来排序，而是用index来查找原来列表中元素的位置，这样在两个数补位后完全相同时就会WA

代码

```python
n=int(input())
l=list(input().split())
max_len=max(len(l[i]) for i in range(n))
l1=[]
for i in range(n):
    x=0
    for j in range(max_len*2):
        x+=int(l[i][j%len(l[i])])*(10**(max_len*2-1-j))
    l1.append((l[i],x))
l1.sort(key=lambda x:x[1])
l2=l1[::-1]
for i in range(n):
    print(l2[i][0],end='')
print(' ',end='')
for i in range(n):
    print(l1[i][0],end='')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20241015133114871](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241015133114871.png)



思路2：冒泡排序

耗时：10min

代码

```python
n=int(input())
l=list(input().split())
for i in range(n-1):
    for j in range(n-i-1):
        if l[j+1]+l[j]>l[j]+l[j+1]:
            l[j],l[j+1]=l[j+1],l[j]
l2=l[::-1]
print(''.join(l)+' '+''.join(l2))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20241015135226688](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241015135226688.png)



## 2. 学习总结和收获

每日选做全部完成

练习了不少贪心的题，基本完成的都比较顺利。学会了双指针、冒泡排序

作业最后一题用到了元素为数组的列表来排序



