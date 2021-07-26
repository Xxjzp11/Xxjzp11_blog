---
id: 01 Tkinter组件详解-Label
title: 01 Tkinter组件详解-Label
author: Xxjzp11
author_title: studying
author_url: https://github.com/Xxjzp11
author_image_url: https://avatars2.githubusercontent.com/u/68409850?s=460&u=144d3c818e76fe4b88687db84279fad48b198818&v=4
tags: [python, notes]
---

# 01 Tkinter组件详解-Label

<!--truncate-->

---------

**Label（标签）组件用于在屏幕上显示文本或图像。Label 组件仅能显示单一字体的文本，但文本可以跨越多行。另外，还可以为其中的个别字符加上下划线（例如用于表示键盘快捷键）**

## 何时使用 Label 组件？

Label 组件用于显示文本和图像，并且使用双缓冲，这样你就可以随时更新内容，没有恼人的闪烁。

如果希望显示的数据用户可以进行操作，使用 Canvas 组件或许更为合适。

-----------------

## 用法

使用 Label 组件，你可以指定想要显示的内容（可以是文本、位图或者图片）：

```python
import tkinter as tk

master = tk.Tk()

w = tk.Label(master, text="一直没有脚的猪！")
w.pack()

master.mainloop()
```

**如果你没有指定 Label 的大小，那么 Label 的尺寸是正好可以容纳其内容而已**，如下：

![01-01.png](https://www.cdnjson.com/images/2021/07/26/01-01.png)

当然你可以通过 **height** 和 **width** 选项来明确设置 **Label** 的大小：如果你显示的是文本，那么这两个选项是以文本单元为单位定义 Label 的大小；如果你显示的是位图或者图像，那么它们以像素为单位（或者其他屏幕单元）定义 Label 大小。

你可以通过 **foreground（或 fg）**和 **background（或 bg）**选项来设置 Label 的**前景色**和**背景色**。你也可以选择 Label 中的文本用哪种字体来显示。指定颜色和字体时需谨慎，除非你有一个很好的理由，否则建议使用默认值（主要是考虑到不同平台的兼容性）。

```python
w = tk.Label(master, text="你好，来自江南的你", font=("华文行楷", 20), fg="green")
```

![01-02.png](https://www.cdnjson.com/images/2021/07/26/01-02.png)

*注：你还可以使用 #RRGGBB 的格式指定具体的颜色值，例如 “#%02x%02x%02x” % (123, 188, 233)*

Label 可以显示**多行文本**，你可以**直接使用换行符**或使用 **wraplength 选项**来实现。**当文本换行的时候，你可以使用 anchor 和 justify 选项来使得文本如你所希望的显示出来**：

```python
longtext = """
Label 可以显示多行文本，你可以直接使用换行符
或使用 wraplength 选项来实现。当文本换行的时
候，你可以使用 anchor 和 justify 选项来使得
文本如你所希望的显示出来。
"""

w = tk.Label(master, text=longtext, anchor="w", justify="left")
```

![01-03.png](https://www.cdnjson.com/images/2021/07/26/01-03.png)

**Label 可以显示 Tkinter 变量的内容。言下之意就是当变量的内容发生改变时，Label 中显示的内容也会自动更新**：

```python
v = tk.StringVar()
w = tk.Label(master, textvariable=v)
v.set("~新的文本~")
w.pack()
```

![01-04.png](https://www.cdnjson.com/images/2021/07/26/01-04.png)

你可以使用 Label 显示 **PhotoImage** 和 **BitmapImage** 对象。当你这么做的时候，请务必保留一份图片对象的引用，以防止被 Python 的垃圾回收机制回收。你可以使用一个全局变量，或一个实例的属性，或者再简单点，在实例上添加一个属性即可：

```python
photo = tk.PhotoImage(file="2.gif")
w = tk.Label(master, image=photo)
w.pack()
```

![01-05.png](https://www.cdnjson.com/images/2021/07/26/01-05.png)

--------

## 参数

**Label(master=None, *\*options) (class)**

master -- 父组件

**options -- 组件选项，下方表格详细列举了各个选项的具体含义和用法：

| 选项                | 含义                                                         |
| ------------------- | ------------------------------------------------------------ |
| activebackground    | 1. **设置当 Label 处于活动状态（通过 state 选项设置状态）的背景色**<br/>2. 默认值由系统指定 |
| activeforeground    | 1. **设置当 Label 处于活动状态（通过 state 选项设置状态）的前景色**<br/>2. 默认值由系统指定 |
| anchor              | 1. **控制文本（或图像）在 Label 中显示的位置**<br/>2. "n", "ne", "e", "se", "s", "sw", "w", "nw", 或者 "center" 来定位（ewsn 代表东西南北，上北下南左西右东）<br/>3. 默认值是 "center" |
| background          | 1. **设置背景颜色**<br/>2. 默认值由系统指定                  |
| bg                  | 跟 background 一样                                           |
| bitmap              | 1. **指定显示到 Label 上的位图**<br/>2. 如果指定了 image 选项，则该选项被忽略 |
| borderwidth         | 1. **指定 Label 的边框宽度**<br/>2. 默认值由系统指定，通常是 1 或 2 像素 |
| bd                  | 跟 borderwidth 一样                                          |
| compound            | 1. **控制 Label 中文本和图像的混合模式**<br/>2. 默认情况下，如果有指定位图或图片，则不显示文本<br/>3. **如果该选项设置为 "center"，文本显示在图像上（文本重叠图像）**<br/>4. 如果该选项设置为 "bottom"，"left"，"right" 或 "top"，那么图像显示在文本的旁边（如 "bottom"，则图像在文本的下方）<br/>5. 默认值是 NONE<br/> |
| cursor              | 1. **指定当鼠标在 Label 上飘过的时候的鼠标样式**<br/>2. 默认值由系统指定 |
| disabledforeground  | 1. **指定当 Label 不可用的时候前景色的颜色**<br/>2. 默认值由系统指定 |
| font                | 1. **指定 Label 中文本的字体**(注：如果同时设置字体和大小，应该用元组包起来，如 **("楷体", 20)**<br/>2. 一个 Label 只能设置一种字体<br/>3. 默认值由系统指定 |
| foreground          | 1. **设置 Label 的文本和位图的颜色**<br/>2. 默认值由系统指定 |
| fg                  | 跟 foreground 一样                                           |
| height              | 1. **设置 Label 的高度**<br/>2. 如果 Label 显示的是文本，那么单位是文本单元<br/>3. 如果 Label 显示的是图像，那么单位是像素（或屏幕单元）<br/>4. 如果设置为 0 或者干脆不设置，那么会自动根据 Label 的内容计算出高度 |
| highlightbackground | 1. **指定当 Label 没有获得焦点的时候高亮边框的颜色**<br/>2. 默认值由系统指定，通常是标准背景颜色 |
| highlightcolor      | 1. **指定当 Label 获得焦点的时候高亮边框的颜色**<br/>2. 默认值由系统指定 |
| highlightthickness  | 1. **指定高亮边框的宽度**<br/>2. 默认值是 0（不带高亮边框）  |
| image               | 1. **指定 Label 显示的图片**<br/>2. 该值应该是 PhotoImage，BitmapImage，或者能兼容的对象<br/>3. 该选项优先于 text 和 bitmap 选项 |
| justify             | 1. **定义如何对齐多行文本**<br/>2. 使用 "left"，"right" 或 "center"<br/>3. 注意，文本的位置取决于 anchor 选项<br/>4. 默认值是 "center" |
| padx                | 1. **指定 Label 水平方向上的额外间距（内容和边框间）**<br/>2. 单位是像素 |
| pady                | 1. **指定 Label 垂直方向上的额外间距（内容和边框间）**<br/>2. 单位是像素 |
| relief              | 1. **指定边框样式**<br/>2. 默认值是 "flat"<br/>3. 另外你还可以设置 "groove", "raised", "ridge", "solid" 或者 "sunken" |
| state               | 1. **指定 Label 的状态**<br/>2. 这个标签控制 Label 如何显示<br/>3. 默认值是 "normal<br/>4. 另外你还可以设置 "active" 或 "disabled" |
| takefocus           | 1. **如果是 True，该 Label 接受输入焦点**<br/>2. 默认值是 False |
| text                | 1. **指定 Label 显示的文本**<br/>2. 文本可以包含换行符<br/>3. 如果设置了 bitmap 或 image 选项，该选项则被忽略 |
| textvariable        | 1. **Label 显示 Tkinter 变量（通常是一个 StringVar 变量）的内容**<br/>2. 如果变量被修改，Label 的文本会自动更新 |
| underline           | 1. **跟 text 选项一起使用，用于指定哪一个字符画下划线（例如用于表示键盘快捷键）** <br/>2. 默认值是 -1<br/>3. 例如设置为 1，则说明在 Button 的第 2 个字符处画下划线 |
| width               | 1. **设置 Label 的宽度**<br/>2. 如果 Label 显示的是文本，那么单位是文本单元<br/>3. 如果 Label 显示的是图像，那么单位是像素（或屏幕单元）<br/>4. 如果设置为 0 或者干脆不设置，那么会自动根据 Label 的内容计算出宽度 |
| wraplength          | 1. **决定 Label 的文本应该被分成多少行**<br/>2. 该选项指定每行的长度，单位是屏幕单元<br/>3. 默认值是 0 |



