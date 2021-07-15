---
id: 020 Python的else语句和with语句
title: 020 Python的else语句和with语句
author: Xxjzp11
author_title: studying
author_url: https://github.com/Xxjzp11
author_image_url: https://avatars2.githubusercontent.com/u/68409850?s=460&u=144d3c818e76fe4b88687db84279fad48b198818&v=4
tags: [python, notes]
---

# 020 Python的else语句和with语句

<!--truncate-->

---------

## else语句

### else语句的用法一

```python
if a>b:
    print(a)
else:
    print(b)
```

### else语句的用法二

```python
#*************************************************#  
#      判断给定数的最大公约数，如果是素数，则打印        #  
#*************************************************#  
def showMaxFactor(num):  
    count = num//2  
    while count > 1:  
        if num %count == 0:  
            print('%d最大的约数是%d'%(num,count))  
            break  
        count -= 1  
    else:  # 只在循环完成后才执行，如果循环中执行使用到break，则else不执行
        print('%d是素数！'%num)  

num = int(input('请输入一个数：'))  
showMaxFactor(num) 
```

### else语句的用法三

```python
try:  
    print(int('abc'))  
except ValueError as reason:  
    print('出错啦：' + reason)  
else:  
    print('没有任何异常！')  # 如果没有出错，则打印出‘没有任何异常！’
```

---------------------------

## with语句

**with 语句的语法格式如下：**

```python
with context_expression [as target(s)]:
    with-body
```

这里 context_expression要返回一个上下文管理器对象，该对象并不赋值给as 子句中的 target(s) ，如果指定了 as 子句的话，会将上下文管理器的 **enter()**方法的返回值赋值给 target(s)。target(s) 可以是单个变量，或者由()括起来的元组（不能是仅仅由“,”分隔的变量列表，必须加“()”）。

Python 对一些内建对象进行改进，加入了对上下文管理器的支持，可以用于 with 语句中，比如可以自动关闭文件、线程锁的自动获取和释放等。假设要对一个文件进行操作，使用 with 语句可以有如下代码：

```python
#********************************************* #  
#        异常处理配合with语句                     #  
#        可以避免已打开文件没关闭的情况             #  
#********************************************* #  
try:  
    with open('data.txt','w') as f:  
        for each_line in f:  
            print(each_line)  
except OSError as reason:  
    print('出错啦：' + str(reason))  
```

这里使用了 with 语句，不管在处理文件过程中是否发生异常，都能保证 with 语句执行完毕后已经关闭了打开的文件句柄。

如果使用传统的try/finally 方式，则要使用类似如下代码：

```python
try:
    f = open('data.txt','w')
    for each_line in f:
        print(each_line)
except OSError as reason:
    print('出错啦：' + str(reason))
finally:
    f.close()
```

--------------

## 测试题

**0.在 Python中，else语句能跟哪些语句进行搭配？**

在Python中，else语句不仅能跟if语句搭配，构成“要么怎样，要么不怎么样”的语境；Ta还能跟循环语句（for语句或者while语句），构成“干完了能怎样，不干完就别想怎样”的语境；其实else语句还能够跟我们刚刚讲的异常处理进行搭配，构成“没有问题，那就干吧”的语境



**1.请问以下例子中，循环中的 break语句会跳过 else语句吗？**

```python
def showMaxFactor(num):  
    count = num // 2  
    while count > 1:  
        if num % count == 0:  
            print('%d最大的约数是%d'%(num,count))  
            break  
        count -= 1  
    else:  
        print('%d是素数！'%num)  
 
num = int(input('请输入一个数：'))  
showMaxFactor(num)
```

会，因为如果将else语句与循环语句（while和for语句）进行搭配，那么只有在循环正常执行完成后才会执行else语句



**2.请目测以下代码会打印什么内容？**

```python
try:  
    print('ABC')  
except:  
    print('DEF')  
else:  
    print('GHI')  
finally:  
    print('JKL')  
```

因为try语句块中并没有异常，则else语句块也会被执行，故只有except语句中的内容不被打印



**3.使用什么语句可以使你不比再担心文件打开后却忘了关闭的尴尬？**

使用with语句。

```python
try:
    with open('data.txt','w') as f:
        for each_line in f:
            print(each_line)
except OSError as reason:
    print('出错啦：' + str(reason))
```



**4.使用with语句固然方便，但如果出现异常的话，文件还会自动正常关闭吗？**

with语句会自动处理文件的打开和关闭，如果中途出现异常，会执行清理代码，然后确保文件自动关闭



**5.你可以换一种形式写出下边的伪代码吗？**

```python
with A() as a:
    with B() as b:
        suite
```

```python
with A() as a,B() as b:  
    suite
```



**6.使用 with语句改写以下代码，让 Python去关心文件的打开与关闭吧**

```python
def file_compare(file1,file2):  
    f1 = open(file1)  
    f2 = open(file2)  
    count = 0#统计行数  
    differ = []#统计不一样的数量  
 
    for line1 in f1:  
        line2 = f2.readline()  
        count += 1  
        if line1 != line2:  
            differ.append(count)  
 
    f1.close()  
    f2.close()  
    return differ  
 
file1 = input('请输入需要比较的头一个文件名：')  
file2 = input('请输入需要比较的另一个文件名：')  
 
differ = file_compare(file1,file2)  
 
if len(differ) == 0:  
    print('两个文件完全一样！')  
else:  
    print('两个文件共有【%d】处不同：'%len(differ))  
    for each in differ:  
        print('第%d行不一样'%each)  
```

仅将file_compare()函数修改为：

```python
def file_compare(file1,file2):  
    with open(file1) as f1, open(file2) as f2:  
        count = 0#统计行数  
        differ = []#统计不一样的数量  
 
        for line1 in f1:  
            line2 = f2.readline()  
            count += 1  
            if line1 != line2:  
                differ.append(count)  
    return differ  
```



**7. 你可以利用异常的原理，修改下面的代码使得更高效率的实现吗？**

```python
print('|--- 欢迎进入通讯录程序 ---|')
print('|--- 1：查询联系人资料  ---|')
print('|--- 2：插入新的联系人  ---|')
print('|--- 3：删除已有联系人  ---|')
print('|--- 4：退出通讯录程序  ---|')

contacts = dict()

while 1:
    instr = int(input('\n请输入相关的指令代码：'))

    if instr == 1:
        name = input('请输入联系人姓名：')
        if name in contacts:
            print(name + ' : ' + contacts[name])
        else:
            print('您输入的姓名不再通讯录中！')

    if instr == 2:
        name = input('请输入联系人姓名：')
        if name in contacts:
            print('您输入的姓名在通讯录中已存在 -->> ', end='')
            print(name + ' : ' + contacts[name])
            if input('是否修改用户资料（YES/NO）：') == 'YES':
                contacts[name] = input('请输入用户联系电话：')
        else:
            contacts[name] = input('请输入用户联系电话：')

    if instr == 3:
        name = input('请输入联系人姓名：')
        if name in contacts:
            del(contacts[name])         # 也可以使用dict.pop()
        else:
            print('您输入的联系人不存在。')

    if instr == 4:
        break

print('|--- 感谢使用通讯录程序 ---|')
```

使用条件语句的代码非常直观明了，但是效率不高。因为程序会两次访问字典的键，一次判断是否存在（if name in contacts），一次获得值（例如：print(name + ' : ' + contacts[name]）。

如果利用异常解决方案，我们可以简单避开每次需要使用in判断是否key存在字典中的操作。

因为**只要当key不存在字典中时，会触发KeyError异常**，利用此特性我们可以修改代码如下：

```python
print('|--- 欢迎进入通讯录程序 ---|')
print('|--- 1：查询联系人资料  ---|')
print('|--- 2：插入新的联系人  ---|')
print('|--- 3：删除已有联系人  ---|')
print('|--- 4：退出通讯录程序  ---|')

contacts = dict()

while 1:
    instr = int(input('\n请输入相关的指令代码：'))

    if instr == 1:
        name = input('请输入联系人姓名：')
        try:
            print(name + ' : ' + contacts[name])
        except KeyError:
            print('您输入的姓名不再通讯录中！')

    if instr == 2:
        name = input('请输入联系人姓名：')
        try:
            contacts[name] 
            print('您输入的姓名在通讯录中已存在 -->> ', end='')
            print(name + ' : ' + contacts[name])
            if input('是否修改用户资料（YES/NO）：') == 'YES':
                contacts[name] = input('请输入用户联系电话：')
        except KeyError:
            contacts[name] = input('请输入用户联系电话：')

    if instr == 3:
        name = input('请输入联系人姓名：')
        try:
            del(contacts[name]) # 也可以使用dict.pop()
        except KeyError:
            print('您输入的联系人不存在。')

    if instr == 4:
        break

print('|--- 感谢使用通讯录程序 ---|')
```



