---
id: github生成配置ssh秘钥
title: github生成配置ssh秘钥
author: Xxjzp11
author_title: studying
author_url: https://github.com/Xxjzp11
author_image_url: https://avatars2.githubusercontent.com/u/68409850?s=460&u=144d3c818e76fe4b88687db84279fad48b198818&v=4
tags: [Git, notes]
---

# github生成配置ssh秘钥

如果安装github成功后，当从本地提交文件到github的时候，提交不成功，报错，可能问题就是你还没有生成ssh秘钥

<!--truncate-->

## 生成密钥

找到本地环境：C:\Users\用户名\\.ssh

在这路径下，打开gitbub的命令控制台

> git init //初始化一下，看看路径对不对
>
> ssh-keygen -t rsa -C "邮箱"

## 传递公钥

到本地环境.ssh路径下查看，是否生成id_rsa、id_rsa.pub这个两个文件

生成后，现在把id_rsa.pub里面的内容复制到githubd的Settings --> SSH and GPG keys -->New SSH key

![01.png](https://www.cdnjson.com/images/2021/08/11/014bbb3da844fe0888.png)

![02.png](https://www.cdnjson.com/images/2021/08/11/02.png)

![03.png](https://www.cdnjson.com/images/2021/08/11/03.png)

第一次提交，配置密钥，需要输入github的密码

## 验证

密钥配置成功后，要验证一下是否配置成功

> ssh -T git@github.com  

![04.png](https://www.cdnjson.com/images/2021/08/11/04.png)

------------

# 通过SSH方法使用git

使用git提交文件到github,每次都要输入用户名和密码，操作起来很麻烦，通过以下方法解决

**原因**：在clone 项目的时候，使用了 https方式，而不是ssh方式

默认clone 方式是：https

![05.png](https://www.cdnjson.com/images/2021/08/11/05.png)

切换到：shh 方式

![06.png](https://www.cdnjson.com/images/2021/08/11/06.png)

## 配置使用SSH方式的Git

 到本地项目文件夹子，打开git bash 

### 移除https的方式

>  git remote rm origin

### 添加新的git方式

ssh方式，ssh方式地址的话，在github上，切换到ssh方式，然后复制地址。

![07.png](https://www.cdnjson.com/images/2021/08/11/07.png)

>  git remote add origin git地址

![08.png](https://z3.ax1x.com/2021/08/11/fa9otJ.png)

### 查看push方式是否修改成功：

> git remote -v

看到如下，说明成功，地址是以git开头

![09.png](https://www.cdnjson.com/images/2021/08/11/09.png)

### 重新push（提交一下）

> git push origin master

![10.png](https://www.cdnjson.com/images/2021/08/11/10.png)





























