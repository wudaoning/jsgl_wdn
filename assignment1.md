# Assignment #1: 自主学习

2024 fall, Complied by 吴道宁 元培学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知9月19日导入选课名单后启用。**作业写好后，保留在自己手中，待9月20日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

因为这些题目我大部分都是假期做的，所以记不太清具体花费的时间了，但大部分应该都在10分钟以内。

### 02733: 判断闰年

http://cs101.openjudge.cn/practice/02733/

##### 代码

```python
a=int(input())
if (a%3200==0) or ((a%100==0) and (a%400!=0)):
    print("N")
elif a%4==0:
    print("Y")
else:
    print("N")
```



代码运行截图 

![image-20240912091022122](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20240912091022122.png)



### 02750: 鸡兔同笼

http://cs101.openjudge.cn/practice/02750/

##### 代码

```python
a=int(input())
if a%4==0:
    print(int(a/4),int(a/2))
elif a%2==0:
    print(int((a+2)/4),int(a/2))
else:
    print(0,0)
```



代码运行截图 

![image-20240912091116423](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20240912091116423.png)



### 50A. Domino piling

greedy, math, 800, http://codeforces.com/problemset/problem/50/A

##### 代码

```python
import math
M,N=map(int,input().split())
print(math.floor(M*N/2))
```



代码运行截图![image-20240912090816495](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20240912090816495.png)



### 1A. Theatre Square

math, 1000, https://codeforces.com/problemset/problem/1/A

##### 代码

```python
import math
n,m,a=map(int,input().split())
l=math.ceil(n/a)
w=math.ceil(m/a)
print(l*w)
```



代码运行截图 

![image-20240912090742516](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20240912090742516.png)



### 112A. Petya and Strings

implementation, strings, 1000, http://codeforces.com/problemset/problem/112/A

##### 代码

```python
s1=input().lower()
s2=input().lower()
if s1>s2:
    print('1')
elif s1<s2:
    print('-1')
else:
    print('0')
```



代码运行截图

![image-20240912090703401](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20240912090703401.png)



### 231A. Team

bruteforce, greedy, 800, http://codeforces.com/problemset/problem/231/A

##### 代码

```python
n=int(input())
a=0
for i in range(n):
    p=list(map(int,input().split()))
    s=sum(p)
    if s>1:
        a+=1
print(a)
```



代码运行截图

![image-20240912090405392](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20240912090405392.png)



## 2. 学习总结和收获

（1）对输入的处理

一行输入多个数，以空格隔开时，一般用：

```python
a,b,c=map(int,input().split())

list(map(int,input().split()))
```

（2）字符串比较大小

按位比较，两个字符串第一位字符的ASCII码谁大，字符串就大，不再比较后面的；第一个字符相同的情况下，就比第二个字符串，以此类推。

常见ASCII码的大小规则：0～9　<　A～Z　<　a～z

（3）range(n)是0~n-1

（4）数学类的题目应该先从数学上找到更简单的运算方法，然后再依据此编程。

额外练习的题目：每日选做



