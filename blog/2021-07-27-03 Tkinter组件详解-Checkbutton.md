---
id: 03 Tkinter组件详解-Checkbutton
title: 03 Tkinter组件详解-Checkbutton
author: Xxjzp11
author_title: studying
author_url: https://github.com/Xxjzp11
author_image_url: https://avatars2.githubusercontent.com/u/68409850?s=460&u=144d3c818e76fe4b88687db84279fad48b198818&v=4
tags: [python, notes, Tkinter组件详解]
---

# 03 Tkinter组件详解-Checkbutton

<!--truncate-->

------------------

## 简介

**Checkbutton（多选按钮）组件用于实现确定是否选择的按钮。Checkbutton 组件可以包含文本或图像，你可以将一个 Python 的函数或方法与之相关联，当按钮被按下时，对应的函数或方法将被自动执行**

**Checkbutton 组件仅能显示单一字体的文本，但文本可以跨越多行。另外，还可以为其中的个别字符加上下划线（例如用于表示键盘快捷键）。默认情况下，tab 按键被用于在按钮间切换**

------------

## 何时使用 Checkbutton 组件？

**Checkbutton 组件被用于作为二选一的按钮（通常为选择“开”或“关”的状态），当你希望表达“多选多”选项的时候，可以将一系列 Checkbutton 组合起来使用**

但是处理“多选一”的问题，还是交给 Radiobutton 和 Listbox 组件来实现吧。

--------------

## 用法

（参考 Button 组件的用法）

使用 Checkbutton，你必须创建一个 Tkinter 变量用于存放按钮的状态：

```python
import tkinter as tk

root = tk.Tk()

var = tk.IntVar()

c = tk.Checkbutton(root, text="我是帅锅", variable=var)
c.pack()

root.mainloop()
```

![03-01.png](https://www.cdnjson.com/images/2021/07/27/03-01.png)

**默认情况下，variable 选项设置为 1 表示选中状态，反之设置为 0**

**你可以使用 onvalue 和 offvalue 选项修改它们的值，例如下边代码，只要 var 被设置为“T”即选中状态，设置为“F”则相反**

```python
var = tk.StringVar()
var.set("T")
c = tk.Checkbutton(root, text="你喜欢Python吗", variable=var, onvalue="T", offvalue="F")
c.pack()
```

![03-02.png](https://www.cdnjson.com/images/2021/07/27/03-02.png)

**如果你需要同时跟踪 variable 选项以及 Checkbutton 组件对象，你不妨可以试试将两者结合起来（下边在 CheckButton 组件对象中新建一个 var 变量，存放 variable 的值 v）**

```python
v = tk.IntVar()
c = tk.Checkbutton(root, text="加特技", variable=v)
c.var = v
```

**如果你的 Tkinter 代码是放在类中的（在实际编程中你就应该这么干），那么将 variable 选项的值作为属性存储可能是更好的选择**

```python
import tkinter as tk

def __init__(self, master):
    self.var = tk.IntVar()
    c = tk.Checkbutton(master, text="DUANG~", variable=self.var, command=self.cb)
    c.pack()

def cb(self, event):
    print("variable is", self.var.get())
```

---

## 方法

### deselect()

-- 取消 Checkbutton 组件的选中状态，也就是设置 variable 为 offvalue。

### flash()

-- 刷新 Checkbutton 组件，该方法将重绘 Checkbutton 组件若干次（在"active" 和 "normal" 状态间切换）。

### invoke()

-- 调用 Checkbutton 中 command 选项指定的函数或方法，并返回函数的返回值。
-- 如果 Checkbutton 的state(状态)"disabled"是 （不可用）或没有指定 command 选项，则该方法无效。

### select()

-- 将 Checkbutton 组件设置为选中状态，也就是设置 variable 为 onvalue。

### toggle()

-- 切换 Checkbutton 组件的状态（选中 -> 未选中 / 未选中 -> 选中）。

----------

## 参数

**Checkbutton(master=None, \**options) (class)** 

master -- 父组件

**options -- 组件选项，下方表格详细列举了各个选项的具体含义和用法：

| 选项                | 含义                                                         |
| ------------------- | ------------------------------------------------------------ |
| activebackground    | 1. **设置当 Checkbutton 处于活动状态（通过 state 选项设置状态）的背景色** <br/>2. 默认值由系统指定 |
| activeforeground    | 1. **设置当 Checkbutton 处于活动状态（通过 state 选项设置状态）的前景色** <br/>2. 默认值由系统指定 |
| anchor              | 1. **控制文本（或图像）在 Checkbutton 中显示的位置** <br/>2. "n", "ne", "e", "se", "s", "sw", "w", "nw", 或者 "center" 来定位（ewsn 代表东西南北，上北下南左西右东） <br/>3. 默认值是 "center" |
| background          | 1. **设置背景颜色** <br/>2. 默认值由系统指定                 |
| bg                  | 跟 background 一样                                           |
| bitmap              | 1. **指定显示到 Checkbutton 上的位图** <br/>2. 如果指定了 image 选项，则该选项被忽略 |
| borderwidth         | 1. **指定 Checkbutton 的边框宽度** <br/>2. 默认值由系统指定，通常是 1 或 2 像素 |
| bd                  | 跟 borderwidth 一样                                          |
| command             | 1. **指定于该按钮相关联的函数或方法**<br/>2. 当按钮被按下时由 Tkinter 自动调用对应的函数或方法<br/>3. 如果不设置此选项，那么该按钮被按下后啥事儿也不会发生 |
| compound            | 1. **控制 Checkbutton 中文本和图像的混合模式** <br/>2. 默认情况下，如果有指定位图或图片，则不显示文本 <br/>3. **如果该选项设置为 "center"，文本显示在图像上（文本重叠图像）** <br/>4. 如果该选项设置为 "bottom"，"left"，"right" 或 "top"，那么图像显示在文本的旁边（如 "bottom"，则图像在文本的下方） <br/>5. 默认值是 NONE |
| cursor              | 1. **指定当鼠标在 Checkbutton 上飘过的时候的鼠标样式** <br/>2. 默认值由系统指定 |
| disabledforeground  | 1. **指定当 Checkbutton 不可用的时候前景色的颜色** <br/>2. 默认值由系统指定 |
| font                | 1. **指定 Checkbutton 中文本的字体**(注：如果同时设置字体和大小，应该用元组包起来，如 **("楷体", 20)** <br/>2. 一个 Checkbutton 只能设置一种字体 <br/>3. 默认值由系统指定 |
| foreground          | 1. **设置 Checkbutton 的文本和位图的颜色** <br/>2. 默认值由系统指定 |
| fg                  | 跟 foreground 一样                                           |
| height              | 1. **设置 Checkbutton 的高度** <br/>2. 如果 Checkbutton 显示的是文本，那么单位是文本单元 <br/>3. 如果 Checkbutton 显示的是图像，那么单位是像素（或屏幕单元） <br/>4. 如果设置为 0 或者干脆不设置，那么会自动根据 Checkbutton 的内容计算出高度 |
| highlightbackground | 1. **指定当 Checkbutton 没有获得焦点的时候高亮边框的颜色** <br/>2. 默认值由系统指定，通常是标准背景颜色 |
| highlightcolor      | 1. **指定当 Checkbutton 获得焦点的时候高亮边框的颜色** <br/>2. 默认值由系统指定 |
| highlightthickness  | 1. **指定高亮边框的宽度** <br/>2. 默认值是1                  |
| image               | 1. **指定 Checkbutton 显示的图片** <br/>2. 该值应该是 PhotoImage，BitmapImage，或者能兼容的对象 <br/>3. 该选项优先于 text 和 bitmap 选项 |
| indicatoron         | 1. **指定前边作为选择的小方块是否绘制**<br/>2. 默认是绘制的<br/>3. 该选项会影响到按钮的样式，如果设置为 False，则点击后该按钮变成 "sunken"（凹陷），再次点击变为 "raised"（凸起） |
| justify             | 1. **定义如何对齐多行文本** <br/>2. 使用 "left"，"right" 或 "center" <br/>3. 注意，文本的位置取决于 anchor 选项 <br/>4. 默认值是 "center" |
| offvalue            | 1. **默认情况下，variable 选项设置为 1 表示选中状态，反之设置为 0**<br/>2. 设置 offvalue 的值可以自定义未选中状态的值（详见上方用法举例） |
| onvalue             | 1. **默认情况下，variable 选项设置为 1 表示选中状态，反之设置为 0**<br/>2. 设置 onvalue 的值可以自定义选中状态的值（详见上方用法举例） |
| padx                | 1. **指定 Checkbutton 水平方向上的额外间距（内容和边框间）** <br/>2. 单位是像素，默认值是 1 |
| pady                | 1. **指定 Checkbutton 垂直方向上的额外间距（内容和边框间）**<br/>2. 单位是像素，默认值是 1 |
| relief              | 1. **指定边框样式** <br/>2. 该值通常是 "flat"，除非你设置 indicatoron 选项为 False<br/>3. 如果 indicatoron 为 False，你还可以设置 "sunken"，"raised"，"groove" 或 "ridge" |
| selectcolor         | 1. **选择框的颜色（就是打勾勾的那个正方形小框框**）<br/>2. 默认值由系统指定 |
| selectimage         | 1. **设置当 Checkbutton 为选中状态的时候显示的图片**<br/>2. 如果没有指定 image 选项，该选项被忽略 |
| state               | 1. **指定 Checkbutton 的状态** <br/>2. 这个标签控制 Checkbutton 如何显示 <br/>3. 默认值是 "normal <br/>4. 另外你还可以设置 "active" 或 "disabled" |
| takefocus           | 1. **如果是 True，该 Checkbutton 接受输入焦点** <br/>2. 默认值是 False |
| text                | 1. **指定 Checkbutton 显示的文本** <br/>2. 文本可以包含换行符 <br/>3. 如果设置了 bitmap 或 image 选项，该选项则被忽略 |
| textvariable        | 1. **Checkbutton 显示 Tkinter 变量（通常是一个 StringVar 变量）的内容** <br/>2. 如果变量被修改，Checkbutton 的文本会自动更新 |
| underline           | 1. **跟 text 选项一起使用，用于指定哪一个字符画下划线（例如用于表示键盘快捷键）**  <br/>2. 默认值是 -1 <br/>3. 例如设置为 1，则说明在 Checkbutton 的第 2 个字符处画下划线 |
| variable            | 1. **将 Checkbutton 跟一个 Tkinter 变量关联**<br/>2. 当按钮按下时，该变量在 onvalue 和 offvalue 之间切换<br/>3. 这个切换的过程是完全自动的 |
| width               | 1. **设置 Checkbutton 的宽度** <br/>2. 如果 Checkbutton 显示的是文本，那么单位是文本单元 <br/>3. 如果 Checkbutton 显示的是图像，那么单位是像素（或屏幕单元） <br/>4. 如果设置为 0 或者干脆不设置，那么会自动根据 Checkbutton 的内容计算出宽度 |
| wraplength          | 1. **决定 Checkbutton 的文本应该被分成多少行** <br/>2. 该选项指定每行的长度，单位是屏幕单元 <br/>3. 默认值是 0 |