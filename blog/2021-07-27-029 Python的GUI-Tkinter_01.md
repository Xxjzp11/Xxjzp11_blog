---
id: 029 Python的GUI-Tkinter_01
title: 029 Python的GUI-Tkinter_01
author: Xxjzp11
author_title: studying
author_url: https://github.com/Xxjzp11
author_image_url: https://avatars2.githubusercontent.com/u/68409850?s=460&u=144d3c818e76fe4b88687db84279fad48b198818&v=4
tags: [python, notes]
---

# 029 Python的GUI-Tkinter_01

<!--truncate-->

-------

## 简单例子

大家回顾一下，到目前为止，几乎我们所有的Python代码都是基于文字交互的界面。Python 的 GUI 工具包有很多，之前我们学过的 EasyGui 就是其中最简单的一个，不过呢，EasyGui 实在是太简单了，因此，它只适合大家接受 GUI 编程的敲门砖，这一次，我们要讲的可不是什么二流货色，这一次我们来讲讲 Tkinter，Tkinter 是什么呢？它有那么 niubi 吗？

**Tkinter 是Python 的标准工具库，它实际上是建立在 TK 技术上的，TK 技术最初是为 TCL 所设计的，TCL 是一门有名的工具命令语言，但是由于其可移植性和灵活性非常强，加上非常容易使用。**因此，TK 技术被移植到许多脚本语言里，包括大名鼎鼎的 Perl 、Ruby 和 Pytho。Tkinter 是 Python 的默认 GUI 库，所以，像 IDLE 使用的就是 Tkinter 设计出来的，因此，我们直接在 IDLE 中导入 tkinter，就可以使用了。tkinter 模块在默认安装 Python 时就会自动安装。

```
>>> import tkinter
```

简单的例子:

```python
import tkinter as tk

app = tk.Tk()
app.title('FishC Demo')

theLable = tk.Label(app, text="我的第二个窗口程序！")
theLable.pack()

app.mainloop()
```

- **tk.Tk() 就让tk 这个类生成了一个 顶层窗口的实例，top level 级别的窗口，我们也成为 root 窗口（根窗口）**

- **title** ，顾名思义，就是**设置窗口的标题**

- **theLbel 的变量，这个变量接收 tk.Label()**，Label 是一个组件，这个组件实例化之后，赋值到 tk.Label 变量中去，这个组件是放在 app 窗口上的，然后组件显示文字为 “我的第二个GUI程序”。（**Label 组件 基本上是最常用的组件了，可以用来显示文本，图像，图标等**）
- **theLabel.pack()：用于自动调节组件自身的尺寸和位置**
- **app.mainloop()：是窗口的主事件循环**，这基本是使用tkinter 的GUI序的最后一行代码，因为进入了主事件循环之后，就由tkinter接管一切，也就是说，一旦执行了这行代码，就不再由代码做主了，而是由 tkinter 来响应用户的输入（例如，用户按下一个按钮，tkinter就会感受到，然后就会响应你为这个事件安排好的方法，由tkinter来调用你的函数。）

进阶版的代码：

```python
import tkinter as tk

class APP():
    def __init__(self, master):
        master.title('Hi!')
        frame = tk.Frame(master)
        frame.pack(side='left', padx=10, pady=10)

        self.hi_there = tk.Button(frame, text="打招呼", fg="white", bg="black", command=self.say_hi)
        self.hi_there.pack()

    def say_hi(self):
        print('hi!')

root = tk.Tk()
app = APP(root)

root.mainloop()
```

- 实例化 tk.Tk()，创建一个 root 窗口，命名变量为 root。然后实例化 App，把 root 作为参数。最后就是 root.mainloop() 主事件循环。
- 我们使用 **tk.Frame 框架**，那么框架是什么呢？框架一般是用于在复杂的布局里面，将这些组件进行分组。
- pack() 方法是自动会调整对应的组件或者框架的位置
  - 默认是调整在 最上边 （top），它一共有4个位置：‘left’, ‘right’, ‘top’, 'bottom’
    - **frame.pack(side='left')**
  - 我们可以通过设置 pack() 方法的 padx 和 pady 参数来修改按钮的边距
    - **frame.pack(side='left', padx = 10, pady = 10)**
- 使用 **tk.Button()** 方法创建一个 按钮组件，这个按钮就放在 frame 框架中，
  - 按钮文本为 “打招呼”，**fg（Foreground） 设置前景色，bg 设置背景色**
  - **command  参数来调用 say_hi() 方法**
  - self.hi_there.pack() 就是自动调整按钮的位置

------------

##  Label 和 Button

### Label

Label组件时用于在界面上输出描述性的标签，比如提示的文字和图片

Label组件载入一张图片的方法

```python
import tkinter as tk 

root = tk.Tk()
photo = tk.PhotoImage( file = '[填写文件的路径]')
imglable = tk.Lable (root, image=pohto)
imglable.pack()

root.mainloop()
```

#### 例子一：

```python
import tkinter as tk

root = tk.Tk()
root.title('Hi!')

textlabel = tk.Label(root,
                     text='Hi Hi!\n ooo!',
                     fg='blue',
                     justify='left',	#文字左对齐
                     padx=10,
                     pady=10)
textlabel.pack(side='left')		#文字在左

img = tk.PhotoImage(file=r'D:\Desktop\1.gif')
imglabel = tk.Label(root, image=img)
imglabel.pack()

root.mainloop()
```

输出结果：

![029-01.png](https://www.cdnjson.com/images/2021/07/27/029-01.png)

#### 例子二：设置背景图

```python
import tkinter as tk

root = tk.Tk()
root.title('Hi!')

img = tk.PhotoImage(file=r'D:\Desktop\2.gif')
thelabel = tk.Label(root,
                    text='Hi Hi!\n ooo!',
                    fg='white',
                    justify='center',
                    image=img,
                    compound='center',	#文本显示在图像上
                    font=('微软雅黑', 20))	#字体
thelabel.pack()

root.mainloop()
```

输出结果：

![029-02.png](https://www.cdnjson.com/images/2021/07/27/029-02.png)

### Button

Botton 就是按钮，Botton 的绝大多数 选项 都和 Label 是一样的。

不过，Bottom 有一个功能，就是可以接收用户的信息，简而言之，Botton 组件就是用于让用户自己下达开始的指令，然后通过按钮上的文字让用户清楚按下此按钮是干什么用的。

#### 例子：在按钮被按下时，Label 文本发生改变

Botton 组件有一个叫做 command 的选项，用于指定一个函数或者方法，它的作用就是当用户点下这个按钮的时候，tkinter 就会自动调用这个指定的函数或是方法

添加一个按钮，然后在按钮被按下时，Label 文本发生改变

```python
import tkinter as tk

root = tk.Tk()
root.title('Hi!')

frame1 = tk.Frame(root)
frame2 = tk.Frame(root)

def click():
    var.set('Everything will be OK!')

var = tk.StringVar()
var.set('Hi Hi!\n ooo!')

img = tk.PhotoImage(file=r'D:\Desktop\2.gif')
thelabel = tk.Label(frame1,
                    textvariable=var,
                    fg='white',
                    justify='center',
                    image=img,
                    compound='center',
                    font=('微软雅黑', 20))
thelabel.pack()

button = tk.Button(frame2, text='Hi!', command=click)
button.pack()

frame1.pack()
frame2.pack()

root.mainloop()
```

输出结果：

![029-03.png](https://www.cdnjson.com/images/2021/07/27/029-03.png)

![029-04.png](https://www.cdnjson.com/images/2021/07/27/029-04.png)

----------------------

## Checkbutton、Radiobutton 和 LabelFrame

### Checkbutton（多选框）

#### 简单例子：

```python
import tkinter as tk

root = tk.Tk()

v = tk.IntVar()
#设置一个tk 变量用于表示按钮是否被选中，这里用整型变量 IntVar

c = tk.Checkbutton(root, text="测试一下", variable=v)
c.pack()

root.mainloop()
```

没有按按钮时：

 ![029-05.png](https://www.cdnjson.com/images/2021/07/27/029-05.png)    

点下按钮的时候：

 ![029-06.png](https://www.cdnjson.com/images/2021/07/27/029-06.png)

当我们点下按钮的时候，这个框框里会出现一个小勾，为了更直观的让大家知道选中和未选中时 v 的表现状态，我们可以把它显示出来，显示在 Label 标签里面

```python
import tkinter as tk

root = tk.Tk()

v = tk.IntVar()
#设置一个tk 变量用于表示按钮是否被选中，这里用整型变量 IntVar

c = tk.Checkbutton(root, text="测试一下", variable=v)
c.pack()

l = tk.Label(root, textvariable = v)
l.pack()

root.mainloop()
```

没有选中时：

 ![029-07.png](https://www.cdnjson.com/images/2021/07/27/029-07.png)

选中的时候：

 ![029-08.png](https://www.cdnjson.com/images/2021/07/27/029-08.png)

#### 例子：翻牌子程序

```python
import tkinter as tk

root = tk.Tk()

girls = ['西施', '貂蝉', '王昭君', '杨玉环']
v = []

for girl in girls:
    v.append(tk.IntVar())
    b = tk.Checkbutton(root, text=girl, variable=v[-1])
    b.pack(anchor='w')
    # anchor选项，实现文本在Button中左对齐，默认是'center'

root.mainloop()
```

运行结果如下：

![029-09.png](https://www.cdnjson.com/images/2021/07/27/029-09.png)

### Radiobutton（单选框）

**Radiobutton（单选框），Radiobutton 的用法和 Checkbutton 的用法基本一致，唯一不同的就是 Radiobutton 要实现单选的效果，就是需要同一组内所有的 Radiobutton 只能共享一个 variable 选项，并且需要设置不同的 value 选项的值**

#### 例子一：

```python
import tkinter as tk

root = tk.Tk()

v = tk.IntVar()

tk.Radiobutton(root, text='One', variable=v, value=1).pack(anchor='w')
tk.Radiobutton(root, text='Two', variable=v, value=2).pack(anchor='w')
tk.Radiobutton(root, text='Three', variable=v, value=3).pack(anchor='w')

root.mainloop()
```


运行结果如下：

![029-10.png](https://www.cdnjson.com/images/2021/07/27/029-10.png)

这里有两点需要注意的：

- **variable 选项只能设置为同一个变量，这里都是 v**
- **value 选项的值 一定要不同，才能实现互测**

**Radiobutton 的原理就是：你每一次点中一个按钮，它就会把这个按钮的 value 给 v，然后根据 v 的值来选中对应的框。**

#### 例子二：

```python
import tkinter as tk

root = tk.Tk()

LANGS = [('Pyhton', 1),
         ('Perl', 2),
         ('Ruby', 3),
         ('Lua', 4)]

v = tk.IntVar()
v.set(1)

for lang, num in LANGS:
    b = tk.Radiobutton(root, text=lang, variable=v, value=num)
    b.pack(anchor='w')

root.mainloop()
```


运行结果如下：

![029-11.png](https://www.cdnjson.com/images/2021/07/27/029-11.png)

#### 修改按钮样式：

只需要加一个选项 **indicatoron = False**（indicatoron 就是指示器，就是前面的小圆圈，把它设置为 False，就不会显示了）

```python
b = tk.Radiobutton(root, text = lang, variable = v, value = num, indicatoron = False)
b.pack(anchor = "w")
```

![029-12.png](https://www.cdnjson.com/images/2021/07/27/029-12.png)

横向填充按钮

```python
b = tk.Radiobutton(root, text = lang, variable = v, value = num, indicatoron = False)
b.pack(fill = "x")
```

![029-13.png](https://www.cdnjson.com/images/2021/07/27/029-13.png)

### LabelFrame

**LabelFrame（标签框架），这实际上是 Frame 框架的进化版，从形态上来说，也就是添加了 Label 的 Frame，但是有了它，Checkbutton 和 Radiobutton 的分组就变得简单了**

```python
import tkinter as tk

root = tk.Tk()

group = tk.LabelFrame(root, text="最好的脚本语言是？", padx=5, pady=5)
group.pack(padx=10, pady=10)

LANGS = [('Pyhton', 1),
         ('Perl', 2),
         ('Ruby', 3),
         ('Lua', 4)]

v = tk.IntVar()

for lang, num in LANGS:
    b = tk.Radiobutton(group, text=lang, variable=v, value=num)
    b.pack(anchor='w')

root.mainloop()
```

运行结果如下：

![029-14.png](https://www.cdnjson.com/images/2021/07/27/029-14.png)

-------

##  Entry （输入框）

输入框是跟程序打交道的途径，比如 程序要求你输入 账号 和 密码。那么它就要提供两个输入框，并且接收密码的输入框还会用 星号 * 将实际的内容给隐藏起来。

我们学了几个 tkinter 的组件之后，你自然就会发现，其实，**很多方法和选项，它们之间都是通用的，这些选项对于不同的组件来说，名字一样，内容也一样**。比如说，**在输入框中，用代码增加和删除内容，也就是使用 insert() 和 delete() 方法**

### 创建一个输入框

我们来尝试一下：

```python
import tkinter as tk

root = tk.Tk()

e = tk.Entry(root)
e.pack(padx=20, pady=20)

root.mainloop()
```

运行一下：

![029-15.png](https://www.cdnjson.com/images/2021/07/27/029-15.png)

就得到了一个输入框，我们可以在里面填写任意的字符，当字符太长时，它会自动滚动

```python
import tkinter as tk

root = tk.Tk()

e = tk.Entry(root)
e.pack(padx=20, pady=20)

e.delete(0, 'end') #清空输入框
e.insert(0, '默认文本') #在 索引0 位置写入字符

root.mainloop()
```

运行一下：

![029-16.png](https://www.cdnjson.com/images/2021/07/27/029-16.png)

### 获取输入框中的内容

- **可以使用 Entry 组件的 get() 方法**

- **也可以将一个 tkinter 的变量（通常是一个 StringVar 变量）挂钩到 textvariable 选项，然后通过变量的 get() 方法来获取**

下面这个例子 ，要实现如图的效果，按 获取信息 按钮时，会清空输入框，然后打印信息

![029-17.png](https://www.cdnjson.com/images/2021/07/27/029-17.png)

当我们按下 获取信息 按钮时：

![029-18.png](https://www.cdnjson.com/images/2021/07/27/029-18.png)

代码如下：

```python
import tkinter as tk

root = tk.Tk()

# 生成两个 Label，显示作品和作者
tk.Label(root, text="作品：").grid(row=0, column=0)
tk.Label(root, text="作者：").grid(row=1, column=0)

e1 = tk.Entry(root)
e2 = tk.Entry(root)
e1.grid(row=0, column=1, padx=10, pady=5)
e2.grid(row=1, column=1, padx=10, pady=5)

def show():
    print("作品：《%s》" % e1.get())
    print("作者：%s" % e2.get())
    e1.delete(0, "end")
    e2.delete(0, "end")

tk.Button(root, text="获取信息", width=10, command=show)\
    .grid(row=3, column=0, sticky="w", padx=10, pady=5)
tk.Button(root, text="退出", width=10, command=root.quit)\
    .grid(row=3, column=1, sticky="e", padx=10, pady=5)  # 退出就直接调用root的 quit() 方法

root.mainloop()
```

传统的做法是用两个 Frame 把它包围起来，现在教你一个新的方法

**tkinter 总共提供了三种不同的 布局组件的方法，一种就是我们熟悉的 pack，还有一种就是 grid （网格），就是使用表格的形式来管理你的组件。另一种就是 place（在后面的笔记中介绍）**

> ### grid() 
>
> 是允许你使用表格的形式来管理组件的位置，它有两个选项
>
> - row 表示 行
> - column 表示 列
> - 行数列数都是从0开始

然后是生成两个输入框。

最后是添加两个按钮。第一个是 “获取信息”，设置宽度 width ，command 为show()函数，另一个是“退出”按钮，我们直接调用 quit() 方法即可

**关于按钮的布局，因为我们不仅要放在最后一行，还要分别靠左、靠右，这就需要设置 grid() 的 sticky 选项**

> ### sticky 用法
>
> - 控制组件在 grid 分配的空间中的位置
> - 可以使用 "n", "e", "s", "w" 以及它们的组合来定位（ewsn代表东西南北，上北下南左西右东）
> - 使用加号（+）表示拉长填充，例如 "n" + "s" 表示将组件垂直拉长填充网格，"n" + "s" + "w" + "e" 表示填充整个网格
> - 不指定该值则居中显示

### 接下来就是如何设计一个密码输入框（用星号*代替你实际输入的内容）

需要设置一个 show 选项

> ### show 用法
>
> - 设置输入框如何显示文本的内容
> - 如果该值非空，则输入框会显示指定字符串代替真正的内容
> - 将该选项设置为 "*"，则是密码输入框（你这是为什么字符，就以什么字符代替）

我们直接在上面的代码上修改：

```python
import tkinter as tk

root = tk.Tk()

# 生成两个 Label，显示作品和作者
tk.Label(root, text="账号：").grid(row=0, column=0)
tk.Label(root, text="密码：").grid(row=1, column=0)

v1 = tk.StringVar()
v2 = tk.StringVar()

e1 = tk.Entry(root, textvariable=v1)
e2 = tk.Entry(root, textvariable=v2, show='*')
e1.grid(row=0, column=1, padx=10, pady=5)
e2.grid(row=1, column=1, padx=10, pady=5)

def show():
    print("账号：%s" % e1.get())
    print("密码：%s" % e2.get())
    e1.delete(0, "end")
    e2.delete(0, "end")

tk.Button(root, text="获取信息", width=10, command=show)\
    .grid(row=3, column=0, sticky="w", padx=10, pady=5)
tk.Button(root, text="退出", width=10, command=root.quit)\
    .grid(row=3, column=1, sticky="e", padx=10, pady=5)  # 退出就直接调用窗口的 quit() 方法

root.mainloop()
```

**另一种获取输入框内容的方法：“你也可以将一个 tkinter 的变量（通常是一个 StringVar 变量）挂钩到 textvariable 选项，然后通过变量的 get() 方法来获取。”**

```
print("账号：%s" %v1.get())
```

运行一下：

![029-19.png](https://www.cdnjson.com/images/2021/07/27/029-19.png)

### 设计一个计算器

```python
import tkinter as tk

master = tk.Tk()

frame = tk.Frame(master)
frame.pack(padx=10, pady=10)

v1 = tk.StringVar()
v2 = tk.StringVar()
v3 = tk.StringVar()

def test(content):
    if content.isdigit() or content == "":
        return True
    else:
        return False

testCMD = master.register(test)  # 冷却，就是调用 register() 方法将验证函数包装起来

e1 = tk.Entry(frame, width=10, textvariable=v1, validate="key", validatecommand=(testCMD, '%P')).grid(row=0, column=0)
tk.Label(frame, text="+").grid(row=0, column=1)
e2 = tk.Entry(frame, width=10, textvariable=v2, validate="key", validatecommand=(testCMD, '%P')).grid(row=0, column=2)
tk.Label(frame, text="=").grid(row=0, column=3)
e3 = tk.Entry(frame, width=10, textvariable=v3, state="readonly").grid(row=0, column=4)

def calc():
    if v1.get() == "" or v2.get() == "":
        result = ""
        v3.set(str(result))
    else:
        result = int(v1.get()) + int(v2.get())
        v3.set(str(result))


tk.Button(frame, text="退出", command=frame.quit).grid(row=1, column=1, pady=10)
tk.Button(frame, text="计算结果", command=calc).grid(row=1, column=3, pady=10)

master.mainloop()
```

运行一下：

![029-20.png](https://www.cdnjson.com/images/2021/07/27/029-20.png)