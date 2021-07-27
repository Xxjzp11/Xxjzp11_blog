---
id: 05 Tkinter组件详解-Frame
title: 05 Tkinter组件详解-Frame
author: Xxjzp11
author_title: studying
author_url: https://github.com/Xxjzp11
author_image_url: https://avatars2.githubusercontent.com/u/68409850?s=460&u=144d3c818e76fe4b88687db84279fad48b198818&v=4
tags: [python, notes, Tkinter组件详解]
---

# 05 Tkinter组件详解-Frame

<!--truncate-->

--------

## 简介

Frame（框架）组件是在屏幕上的一个矩形区域。Frame 主要是作为其他组件的框架基础，或为其他组件提供间距填充

------------------

## 何时使用 Frame 组件？

**Frame 组件主要用于在复杂的布局中将其他组件分组，也用于填充间距和作为实现高级组件的基类**

-------------

## 用法

Frame 组件可以用于装饰界面：

```python
import tkinter as tk

master = tk.Tk()

tk.Label(text="天王盖地虎").pack()

separator = tk.Frame(height=2, bd=1, relief="sunken")
separator.pack(fill="x", padx=5, pady=5)

tk.Label(text="小鸡炖蘑菇").pack()

master.mainloop()
```

![05-01.png](https://www.cdnjson.com/images/2021/07/27/05-01.png)

----------------

## 参数

Frame(master=None, **options) (class)

master -- 父组件

**options -- 组件选项，下方表格详细列举了各个选项的具体含义和用法：

| 选项                | 含义                                                         |
| ------------------- | ------------------------------------------------------------ |
| background          | 1. **设置 Frame 组件的背景颜色**<br/>2. 默认值由系统指定<br/>3. 为了防止更新，可以将颜色值设置为空字符串 |
| bg                  | 跟 background 一样                                           |
| borderwidth         | 1. **指定 Frame 的边框宽度**<br/>2. 默认值是 0               |
| bd                  | 跟 borderwidth 一样                                          |
| class               | 默认值是 Frame                                               |
| colormap            | 1. 有些显示器只支持 256 色（有些可能更少），这种显示器通常提供一个颜色映射来指定要使用要使用的 256 种颜色<br/>2. **该选项允许你指定用于该组件以及其子组件的颜色映射**<br/>3. 默认情况下，Frame 使用与其父组件相同的颜色映射<br/>4. 使用此选项，你可以使用其他窗口的颜色映射代替（两窗口必须位于同个屏幕并且具有相同的视觉特性）<br/>5. 你也可以直接使用 "new" 为 Frame 组件分配一个新的颜色映射<br/>6. 一旦创建 Frame 组件实例，你就无法修改这个选项的值 |
| container           | 1. **该选项如果为 True，意味着该窗口将被用作容器，一些其它应用程序将被嵌入** <br/>2. 默认值是 False |
| cursor              | 1. **指定当鼠标在 Frame 上飘过的时候的鼠标样式**<br/>2. 默认值由系统指定 |
| height              | 1. **设置 Frame 的高度**<br/>2. 默认值是 0                   |
| highlightbackground | 1. **指定当 Frame 没有获得焦点的时候高亮边框的颜色**<br/>2. 默认值由系统指定，通常是标准背景颜色 |
| highlightcolor      | 1. **指定当 Frame 获得焦点的时候高亮边框的颜色**<br/>2. 默认值由系统指定 |
| highlightthickness  | 1. **指定高亮边框的宽度**<br/>2. 默认值是 0（不带高亮边框）  |
| padx                | 水平方向上的边距                                             |
| pady                | 垂直方向上的边距                                             |
| relief              | 1. **指定边框样式**<br/>2. 默认值是 "flat"<br/>3. 另外你还可以设置 "sunken"，"raised"，"groove" 或 "ridge"<br/>4. 注意，如果你要设置边框样式，记得设置 borderwidth 或 bd 选项不为 0，才能看到边框 |
| takefocus           | 1. **指定该组件是否接受输入焦点**（用户可以通过 tab 键将焦点转移上来）<br/>2. 默认值是 False |
| visual              | 1. **为新窗口指定视觉信息**<br/>2. 该选项没有默认值          |
| width               | 1. **设置 Frame 的宽度**<br/>2. 默认值是 0                   |

