---
id: 06 Tkinter组件详解-LabelFrame
title: 06 Tkinter组件详解-LabelFrame
author: Xxjzp11
author_title: studying
author_url: https://github.com/Xxjzp11
author_image_url: https://avatars2.githubusercontent.com/u/68409850?s=460&u=144d3c818e76fe4b88687db84279fad48b198818&v=4
tags: [python, notes, Tkinter组件详解]
---

# 06 Tkinter组件详解-LabelFrame

<!--truncate-->

----------

## 简介

LabelFrame 组件是 Frame 组件的变体。默认情况下，LabelFrame 会在其子组件的周围绘制一个边框以及一个标题。

---------

## 何时使用 LabelFrame 组件？

当你想要将一些相关的组件分为一组的时候，可以使用 LabelFrame 组件，比如一系列 Radiobutton（单选按钮）组件

-------

## 用法

**为组件分组，需要先创建一个 LabelFrame，然后像往常一样将子组件添加进去。LabelFrame 组件会自动绘制一个边框将子组件包围起来，并在它们上方显示一个文本标题**

```python
import tkinter as tk

master = tk.Tk()

group = tk.LabelFrame(master, text="你喜欢什么语言", padx=5, pady=5)
group.pack(padx=10, pady=10)

v = tk.IntVar()
r1 = tk.Radiobutton(group, text="Python", variable=v, value=1).pack(anchor="w")
r2 = tk.Radiobutton(group, text="C++", variable=v, value=2).pack(anchor="w")
r3 = tk.Radiobutton(group, text="Java", variable=v, value=3).pack(anchor="w")

master.mainloop()
```

![06-01.png](https://www.cdnjson.com/images/2021/07/27/06-01.png)


你还可以通过选项定义如何绘制标签和边界，请看下边详细说明

---------------

## 参数

**LabelFrame(master=None, \**options) (class)**

master -- 父组件

**options -- 组件选项，下方表格详细列举了各个选项的具体含义和用法：

| 选项                | 含义                                                         |
| ------------------- | ------------------------------------------------------------ |
| background          | 1. **设置 LabelFrame 组件的背景颜色**<br/>2. 默认值由系统指定<br/>3. 为了防止更新，可以将颜色值设置为空字符串 |
| bg                  | 跟 background 一样                                           |
| borderwidth         | 1. **指定 LabelFrame 的边框宽度**<br/>2. 默认值是 0          |
| bd                  | 跟 borderwidth 一样                                          |
| class               | 默认值是 LabelFrame                                          |
| colormap            | 1. 有些显示器只支持 256 色（有些可能更少），这种显示器通常提供一个颜色映射来指定要使用要使用的 256 种颜色<br/>2. **该选项允许你指定用于该组件以及其子组件的颜色映射**<br/>3. 默认情况下，LabelFrame 使用与其父组件相同的颜色映射<br/>4. 使用此选项，你可以使用其他窗口的颜色映射代替（两窗口必须位于同个屏幕并且具有相同的视觉特性）<br/>5. 你也可以直接使用 "new" 为 LabelFrame 组件分配一个新的颜色映射<br/>6. 一旦创建 LabelFrame 组件实例，你就无法修改这个选项的值 |
| container           | 1. **该选项如果为 True，意味着该窗口将被用作容器，一些其它应用程序将被嵌入** <br/>2. 默认值是 False |
| cursor              | 1. **指定当鼠标在 LabelFrame 上飘过的时候的鼠标样式**<br/>2. 默认值由系统指定 |
| foreground          | 1. **设置 LabelFrame 的文本颜色**<br/>2. 默认值由系统指定    |
| fg                  | 跟 foreground 一样                                           |
| font                | 1. **指定 LabelFrame 中文本的字体**<br/>2. 默认值由系统指定  |
| height              | 1. **设置 LabelFrame 的高度**<br/>2. 默认值是 0              |
| highlightbackground | 1. **指定当 LabelFrame 没有获得焦点的时候高亮边框的颜色**<br/>2. 默认值由系统指定，通常是标准背景颜色 |
| highlightcolor      | 1. **指定当 LabelFrame 获得焦点的时候高亮边框的颜色**<br/>2. 默认值由系统指定 |
| highlightthickness  | 1. **指定高亮边框的宽度**<br/>2. 默认值是 1 或 2 像素        |
| labelanchor         | 1. **控制文本在 LabelFrame 的显示位置** <br/>2. "n", "ne", "e", "se", "s", "sw", "w", "nw", 或 "center" 来定位（ewsn代表东西南北，上北下南左西右东） <br/>3. 默认值是 NW |
| labelwidget         | 1. **指定一个组件替代默认的文本 Label**<br/>2. 如果同时设置此选项和 text 选项，则忽略 text 选项的内容 |
| padx                | 1. **指定 FrameLabel 水平方向上的额外间距**（内容和边框间）<br/>2. 默认值是 0 |
| pady                | 1. **指定 FrameLabel 垂直方向上的额外间距**（内容和边框间）<br/>2. 默认值是 0 |
| relief              | 1. **指定边框样式**<br/>2. 默认值是 "groove"<br/>3. 另外你还可以设置 "flat"，"sunken"，"raised" 或 "ridge"<br/>4. 注意，如果你要设置边框样式，记得设置 borderwidth 或 bd 选项不为 0，才能看到边框 |
| takefocus           | 1. **指定该组件是否接受输入焦点**（用户可以通过 tab 键将焦点转移上来）<br/>2. 默认值是 False |
| text                | 1. **指定 LabelFrame 显示的文本**<br/>2. 文本可以包含换行符  |
| visual              | 1. **为新窗口指定视觉信息**<br/>2. 该选项没有默认值          |
| width               | 1. **设置 LabelFrame 的宽度**<br/>2. 默认值是 0              |















