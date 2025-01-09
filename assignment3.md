# Assign #3: Oct Mock Exam暨选做题目满百

Updated 1537 GMT+8 Oct 10, 2024

2024 fall, Complied by 吴道宁 元培学院



**说明：**

1）Oct⽉考： AC5 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++/C（已经在Codeforces/Openjudge上AC），截图（包含Accepted, 学号），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、作业评论有md或者doc。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E28674:《黑神话：悟空》之加密

http://cs101.openjudge.cn/practice/28674/



耗时：<15min



代码

```python
k=int(input())
s=input()
sl=[]
a='a b c d e f g h i j k l m n o p q r s t u v w x y z'
b=a.upper()
al=list(a.split())
bl=list(b.split())
for i in range(len(s)):
    if s[i] in al:
        x=(al.index(s[i])-k)%26
        sl.append(al[x])
    if s[i] in bl:
        x=(bl.index(s[i])-k)%26
        sl.append(bl[x])
print(''.join(str(j) for j in sl))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241011182724084](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241011182724084.png)



### E28691: 字符串中的整数求和

http://cs101.openjudge.cn/practice/28691/



耗时：2min



代码

```python
s1,s2=input().split()
print(10*int(s1[0])+int(s1[1])+10*int(s2[0])+int(s2[1]))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241011183039093](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241011183039093.png)



### M28664: 验证身份证号

http://cs101.openjudge.cn/practice/28664/



耗时：<10min



代码

```python
n=int(input())
last=['1','0','X','9','8','7','6','5','4','3','2']
number=[7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2]
for i in range(n):
    s=input()
    x=0
    for j in range(17):
        x+=number[j]*int(s[j])
    x%=11
    if s[17]==last[x]:
        print('YES')
    else:
        print('NO')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20241011183445963](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241011183445963.png)



### M28678: 角谷猜想

http://cs101.openjudge.cn/practice/28678/



耗时：5min



代码

```python
n=int(input())
while True:
    if n==1:
        print('End')
        break
    if n%2==1:
        a=3*n+1
        print(f'{n}*3+1={a}')
        n=a
    if n%2==0:
        b=n//2
        print(f'{n}/2={b}')
        n=b
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20241011183601415](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241011183601415.png)



### M28700: 罗马数字与整数的转换

http://cs101.openjudge.cn/practice/28700/



耗时：25min

思路：创建一个“字典”（列表l[i]为i对应的罗马数字），创建方法为把千位、百位、十位、个位分别转换为对应的罗马数字（这个过程中也用到了类似字典的列表）



##### 代码

```python
s=input()
number=['1','2','3','4','5','6','7','8','9']
l=[0]
for i in range(1,4000):
    a=i//1000
    b=(i-1000*a)//100
    c=(i-1000*a-100*b)//10
    d=i-1000*a-100*b-10*c
    r=[]
    l1=['','M','MM','MMM']
    l2=['','C','CC','CCC','CD','D','DC','DCC','DCCC','CM']
    l3=['','X','XX','XXX','XL','L','LX','LXX','LXXX','XC']
    l4=['','I','II','III','IV','V','VI','VII','VIII','IX']
    r.append(l1[a])
    r.append(l2[b])
    r.append(l3[c])
    r.append(l4[d])
    roman=''.join(j for j in r)
    l.append(roman)
if s[0] in number:
    n=int(s)
    print(l[n])
else:
    print(l.index(s))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20241011183713616](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241011183713616.png)



### *T25353: 排队 （选做）

http://cs101.openjudge.cn/practice/25353/



耗时：考场上用时45min，TLE，思路是判断每次新输入的元素插入到列表的哪个位置。后来看了题解AC的。



代码

```python
n,d=map(int,input().split())
h=[int(input()) for _ in range(n)]
used=[False]*n
h_new=[]
while False in used:
    free=[]
    for i in range(n):
        if used[i]:
            continue
        if len(free)==0:
            free.append(h[i])
            maxh=h[i]
            minh=h[i]
            used[i]=True
            continue
        maxh=max(h[i],maxh)
        minh=min(h[i],minh)
        if maxh-minh>2*d:
            break
        if maxh-h[i]<=d and h[i]-minh<=d:
            free.append(h[i])
            used[i]=True
    free.sort()
    h_new.extend(free)
for j in h_new:
    print(j)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20241013092315448](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20241013092315448.png)



## 2. 学习总结和收获

完成了每日选做到10.9

学会了用类似字典的方式使用列表，也在一些题中实践了贪心和递归。

考场上比较担心时间不够，所以最后一题感觉想的不是很清楚就开始写代码，方法比较暴力，导致最后一直TLE。感觉以后遇见难题还是应该先想清楚，最好找到比较好的方法再开始写。
