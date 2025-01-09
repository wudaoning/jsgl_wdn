# Assignment #2: 语法练习

Updated 0126 GMT+8 Sep 24, 2024

2024 fall, Complied by 吴道宁 元培学院

**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知9月19日导入选课名单后启用。**作业写好后，保留在自己手中，待9月20日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 263A. Beautiful Matrix

https://codeforces.com/problemset/problem/263/A



耗时：10min



##### 代码

```python
for i in range(5):
    s=input().split()
    if '1' in s:
        print(abs(i-2)+abs(s.index('1')-2))
        break
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240924084736031](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20240924084736031.png)



### 1328A. Divisibility Problem

https://codeforces.com/problemset/problem/1328/A



耗时：小于10min



##### 代码

```python
t=int(input())
for i in range(t):
    a,b=map(int,input().split())
    if a%b==0:
        print('0')
    else:
        print(b-(a%b))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240924084941592](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20240924084941592.png)



### 427A. Police Recruits

https://codeforces.com/problemset/problem/427/A



耗时：15min



##### 代码

```python
n=int(input())
x=0
y=0
l=list(map(int,input().split()))
for i in range(n):
    if l[i]==-1:
        if x==0:
            y+=1
        else:
            x=x-1
    else:
        x=x+l[i]
print(y)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240924085135009](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20240924085135009.png)



### 02808: 校门外的树

http://cs101.openjudge.cn/practice/02808/



耗时：20min



##### 代码

```python
L,M=map(int,input().split())
t=[1]*(L+1)
for i in range(M):
    b,e=map(int,input().split())
    for j in range(b,e+1):
        t[j]=0
print(t.count(1))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240924085359718](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20240924085359718.png)



### sy60: 水仙花数II

https://sunnywhy.com/sfbj/3/1/60



耗时：小于10min



##### 代码

```python
a,b=map(int,input().split())
l=[]
for i in range(a,b+1):
    x=i//100
    y=(i-100*x)//10
    z=i-100*x-10*y
    if i==x**3+y**3+z**3:
        l.append(i)
if len(l)==0:
    print('NO')
else:
    print(*l) 
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240924084305261](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20240924084305261.png)



### 01922: Ride to School

http://cs101.openjudge.cn/practice/01922/



耗时：约10min



##### 代码

```python
import math
while True:
    n=int(input())
    if n==0:
        break
    x=float('inf')
    for i in range(n):
        v,t=map(int,input().split())
        if t>=0:
            at=math.ceil(4.5*3600/v+t)
            x=min(x,at)
    print(x) 
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240924083608653](C:\Users\wudaoning\AppData\Roaming\Typora\typora-user-images\image-20240924083608653.png)



## 2. 学习总结和收获

（1）python列表的基本操作：

​	（a）创建n个元素全为0的列表：listname=[0]*n

​	（b）列表切片：listname[start : end : step]

​	（c）list3=list1+list2

​	（d）在列表的末尾加元素：listname.append(obj) 或 listname.extend(obj) （obj可以是单个元素、列表、元组）

​	（e）在列表的指定位置插入元素：listname.insert(index , obj)

​	（f）根据索引值删除元素：del listname[index] 或 del listname[start : end]（不包括end）或 listname.pop(index)

​	（g）根据元素值删除元素：listname.remove(obj)

​	（h）修改元素：listname[index]=new_value（索引可以使用负数，例如最后一个元素是-1）（字符串不能这样）

​	（i）查找元素：listname.index(obj , start , end)

​	（j）统计元素出现次数：listname.count(obj)

​	（k）对列表进行排序：升序listname.sort()，降序listname.sort(reverse=True)

​	（m）列表长度l=len(listname)

​	（l）遍历列表：for obj in listname:

​	（n）new_list = [x*2 for x in listname]

​	（o）把列表元素颠倒顺序：listname.reverse()

​	（p）输出列表，元素之间以空格隔开：print(*listname)

​	（q）判断元素在不在列表里：if obj in listname: 或 if obj not in listname:

（2）一些题中可以创建一个全为0的列表，依据一些条件把其中的一些元素变为1，然后统计1的个数

（3）python中表示“无穷大”的方式：float('inf')

（4）一些字符串的基本操作：

​	（a）全部大写：s.upper()	全部小写：s.lower()

​			首字母大写，其他全部小写：s.capitalize()	每个单词的首字母大写，其他全部小写：s.title()

​	（b）查找子字符串：s.find(substring , start , end)	s.index(substring , start , end)

​	（c）替换子字符串：new_string = old_string.replace(old_substring , new_substring , count)

​	（d）字符串拆分：s.split(separator, maxsplit)

​	（e）去除首尾指定字符：s.strip()（默认为空格）

​	（f）字符串长度l=len(s)（同列表）

（5）从数学上优化算法，减少暴力枚举

额外练习：每日选做全部完成
