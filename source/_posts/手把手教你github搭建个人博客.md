---
title: 手把手教你github搭建个人博客
date: 2017-06-13 18:00:00
---

本文是 记录了 Ubuntu16.04 下 通过 Hexo + GitHub 搭建的博客的完整记录，希望大家可以耐心阅读下。

最开始的时候，都是把自己的技术文档、安装攻略，整理到云笔记上，但是后来，云笔记渐渐的不好用了 ，主要原因还是因为他们都开始通过各种方式收费或者限制了，我用过 印象、有道、为知 等等，当我一次次的迁徙我的笔记的时候，就是我一次次的跳入一个坑。当然，我是支持云笔记收费的，只是他们还不到让我买账的程度，因为他们在收费后与之前相比，并没有变的更好用。但是，我知道总有一天，我还是会为他们买单的，当他们可以在Linux系统下运行的时候，期待中吧：）

目录流程：


[TOC]


## 1. 搭建 Node.js 环境

为什么要搭建 Node.js 环境？ - 因为 Hexo 博客系统是基于 Node.js 编写的

Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境，可以在非浏览器环境下，解释运行 JS 代码。

[node.js官网](https://nodejs.org/en/)：下载安装包 v6.10.3LTS(下载最新的即可)[这是我下载的安装包的地址](https://nodejs.org/dist/v6.10.3/node-v6.10.3-linux-x64.tar.xz)

步骤：

Windows 安装

保持默认设置即可，一路Next，安装很快就结束了，然后打开命令提示符win + R，输入

1. > node -v

2. > npm -v

出现版本号则说明 Node.js 环境配置成功，第一步完成！！！

![Alt text](http://upload-images.jianshu.io/upload_images/6298250-7522dbe127fbd1fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Ubuntu安装

我是通过浏览器下载到 （/home/wy/下载），你们可以找到相应的位置（如果位置与你们的有出入可以做相应修改）：

![](http://upload-images.jianshu.io/upload_images/6298250-978afc21a56aa177.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


1. > tar zxvf ~/下载/node-v6.10.3-linux-x64.tar.xz -C /opt

2. > cd /opt/node-v6.10.3-linux-x64/

3. > ./node -v

	![](http://upload-images.jianshu.io/upload_images/6298250-6802cc3c09f784fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 

4. > ln -s /opt/node-v6.10.3-linux-x64/bin/node /usr/local/bin/node

5. > ln -s /opt/node-v6.10.3-linux-x64/bin/npm /usr/local/bin/npm

意思就是创建软链接，在/usr/local/bin里，就可以全局使用

还有一种就是shell提示的apt-get方式，我之前就被这种方式坑了。。。强烈不推荐啊

另一种：

1. > sudo apt-get install nodejs

2. > sudo apt-get install npm

3. > node -v

4. > npm -v

## 2. 搭建 Git 环境

为什么要搭建 Git 环境？ - 因为需要把本地的网页和文章等提交到 GitHub 上。

Git 是一款免费、开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。

[git的安装配置](http://www.runoob.com/git/git-install-setup.html)

[Git安装教程](http://www.jianshu.com/p/dc90b9aac18c)

[GitHub - 账户的创建和配置](https://git-scm.com/book/zh/v2/GitHub-%E8%B4%A6%E6%88%B7%E7%9A%84%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE)

在Ubuntu上安装git

1. > sudo apt-get update

    > sudo apt-get install git

2. > git config --global user.name "your name"

3. > git config --global user.email "your email"

4. > git config --global push.default simple  # 每次push仅push当前分支

5. > git config --global core.autocrlffalse  # 忽略window/unix换行符

5. > git config --global gui.encoding utf-8  # 避免乱码

6. > git config --global core.quotepath off  # 避免git status显示的中文文件名乱码

7. > git --version  # 版本

8. > git config--globalmerge.tool vimdiff  # 差异分析工具

9. > git config --list  # 查看配置信息

10. > ssh-keygen -t rsa -C "your email"

11. > ssh-add ~/.ssh/id_rsa  # github用的公钥就在~/.ssh/id_rsa.pub

## 3. GitHub 注册和配置

GitHub 是一个代码托管平台，因为只支持 Git 作为唯一的版本库格式进行托管，故名 GitHub。

Github注册：[https://github.com/](https://github.com/)

![](http://upload-images.jianshu.io/upload_images/6298250-53ce8d7ea0817c35.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


1. > 选择 New repository

2. > Repository name 必须选择 相应的格式 "yourname.github.io"

	点击绿色按钮 Create repository 创建
	![](http://upload-images.jianshu.io/upload_images/6298250-c42cd1e1fd2e8578.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. > 点击 Settings 完成相应配置
	
	![](http://upload-images.jianshu.io/upload_images/6298250-310894e2777e8fbb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4. > 选择 Deploy keys 选项,配置ssh秘钥

	![](http://upload-images.jianshu.io/upload_images/6298250-fca9a9db15b49601.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5. > 点击 Add deploy key,添加相应秘钥

	![](http://upload-images.jianshu.io/upload_images/6298250-170e6e0a52af8c97.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

6. > 添加内容 ,title 随便写,key 需要在你的本地查看

	打开终端,输入:

	> vim ~/.ssh/id_rsa.pub

	![](http://upload-images.jianshu.io/upload_images/6298250-0fabc6342c6e477a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	鼠标右键复制所有内容,到 github刚才配置秘钥页面的 key 里

	![](http://upload-images.jianshu.io/upload_images/6298250-194d2fa997c505d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	完成内容如下,并点击 Add key

	![](http://upload-images.jianshu.io/upload_images/6298250-83b0eabdfdd7a84c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

7. > 最后测试:  输入  ssh git@github.com

	如果最后出现,

	ERROR: Hi tekkub! You’ve successfully authenticated, but GitHub does not provide shell access

	Connection to github.com closed.

	说明配置成功

## 4. 安装配置 Hexo

Hexo 是一个快速、简洁且高效的博客框架，使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

强烈建议你花20分钟区读一读 Hexo 的官方文档：https://hexo.io/zh-cn/

1. 如果之前node.js 安装配置正确的话,可以运行如下命令:

	![](http://upload-images.jianshu.io/upload_images/6298250-311c09a2eb7466f1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	当然命令需要变通一下,不能完全按照下边的执行


	在Linux终端 输入 cd ~

	进入你的Home目录

2. npm install hexo-cli -g   # 这一步是通过必备的node.js安装成功后,既可以用npm安装

	安装成功后,会装在 /opt/node-v6.10.3-linux-x64/bin 这个目录

	下边的命令,需要hexo全局使用,这里创建软链接 :

	ln -s /opt/node-v6.10.3-linux-x64/bin/hexo /usr/local/bin/hexo

	这里完成才可以执行第三部

3. hexo init bigjeffwang.github.io

	我这里是在 Home目录执行安装初始化 先 cd ~ 进入Home目录,在执行

4. cd bigjeffwang.github.io

5. npm install

6. hexo server

## 5. 关联Hexo与GitHub Pages

基本到这里,完成第5部,算是安装完成,因为之前的github的配置,会关联github

可能需要注意的几点:

在使用npm 安装 Hexo：在命令行中输入npm install hexo-cli -g

然后你将会看到下图，可能你会看到一个

WARN

，但是不用担心，这不会影响你的正常使用。

![](http://upload-images.jianshu.io/upload_images/6298250-f53c5875bfd8b22e.JPEG&access=215967316?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

查看Hexo的版本hexo version

![](http://upload-images.jianshu.io/upload_images/6298250-478e58faaa20e65f.JPEG&access=215967316?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

最后在进行hexo相关配置:

打开 你本地项目里的 vim _config.yml

![](http://upload-images.jianshu.io/upload_images/6298250-c6f68a03bcfb7a20.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

_config.yml配置参考

![](http://upload-images.jianshu.io/upload_images/6298250-cc524789ea634828.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

需要改一下 你的 标题 author作者 等等,按照你的意愿,下边有许多可以改的地方,请参考hexo的 [官方文档](https://hexo.io/zh-cn/docs/configuration.html)

![](http://upload-images.jianshu.io/upload_images/6298250-89677e673fc92f6e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

最后在文档的最后,  deploy 需要改一下,一定要注意 文档格式 所有的: 后边都必须有空格!!!

type 设置 git

repository 设置 你github上的项目的 克隆地址 这里一定不要用https:// 开头的地址,因为这样还是需要账户密码登录,后期维护麻烦,之前设置github秘钥,也是为了方便这里,用ssh的地址方式 git@github.com:后边接你的名字+/项目地址

branch 分支就设置master就可以

![](http://upload-images.jianshu.io/upload_images/6298250-fc73891ea5804372.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

安装一个扩展 这个很有用 如下:

npm install hexo-deployer-git --save  # 它可以让你代替git, push你的博客项目

hexo new "hello world" 这样可以创建你的一篇博客 安装扩展后

hexo g  # 执行这个,就可以编译你的项目,当然这是简写,完整是 hexo generate

hexo d  # 同样 执行这个,就可以部署你的项目,并推送到github上了

项目里的source/_post 这个目录,就是你生成和存放文档的目录

在浏览器中输入 https://bigjeffwang.github.io （用户名当然改成你的）看到了 Hexo 与 GitHub Pages 已经成功关联了，哇哇哇哇哇哇，开心死你了，不要忘了回来给我点赞哟 ~

下边设置,修改hexo主题

在 _config.yml 里边有一项是  theme:  它后边接的就是你的主题

这里需要如下步骤:

1. 进入你的博客项目的themes

	cd ~/bigjeffwang.github.io/themes

2. 从github上克隆一个 别人的主题  这里提供一下别人的主题链接,以供参考 [hexo主题](https://www.zhihu.com/question/24422335)

	> git clone https://github.com/wuchong/jacman.git ./jacman

	> cd ./jacman

	> git pull

jacman 里边 也是有 _config.yml ,里边怎么修改,需要你自己琢磨,大同小异.请参考 [官方文档](https://hexo.io/zh-cn/docs/configuration.html)

当然,你也可以自己优化,相当于一个简单的web项目,里边也有JS CSS IMG 目录,可以替换相应你喜欢的图片

最后别忘了,修改你项目里的_config.yml,替换你的主题的文件夹名字

我这里是 jacman

![](http://upload-images.jianshu.io/upload_images/6298250-60e163ffa362f0e7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 6. 多个git账号，该如何设置

这里懒得写,借用一下,别人总结好的 [原作者文档](http://www.linuxidc.com/Linux/2016-05/131079.htm)

场景：使用github的时候，大家都知道需要给该账号添加一个SSH key才能访问，参考 [具体设置](https://help.github.com/articles/generating-ssh-keys)。当然如果你在多台机器使用一个账户，你可以为该账户添加多个SSH key。由于github是使用SSH key的fingerprint来判定你是哪个账户，而不是通过用户名，这样你就可以在设置完之后，在本地直接执行下面的语句，它就会自动使用你的.ssh/id_rsa.pub所对应的账户进行登陆，然后执行相关命令。

1. > 本地建库
2. > git init
3. > git commit -am"first commit'
4. > push到github上去
5. > git remote add origin git@github.com:xxxx/test.git
6. > git push origin master

但是如果你想在一台机器使用两个github账号（比如私人账号和工作用账号）。这个时候怎么指定push到哪个账号的test仓库上去呢？

解决方案（假设你已经拥有私有账号且已经OK，现在想使用另一个工作用账号）：

1. 为工作账号生成SSH Key

	> ssh-keygen -t rsa -C"your-email-address"#存储key的时候，不要覆盖现有的id_rsa，使用一个新的名字，比如id_rsa_work

2. 把id_rsa_work.pub加到你的work账号上

3. 把该key加到ssh agent上。由于不是使用默认的.ssh/id_rsa，所以你需要显示告诉ssh agent你的新key的位置

	> ssh-add ~/.ssh/id_rsa_work#可以通过ssh-add -l来确认结果

4. 配置.ssh/config

	> vi .ssh/config#加上以下内容#default githubHost github.com

```
HostName github.com

	IdentityFile~/.ssh/id_rsa

	Host github_work

	HostName github.com

	IdentityFile~/.ssh/id_rsa_work
```

5. 这样的话，你就可以通过使用github.com别名github_work来明确说你要是使用id_rsa_work的SSH key来连接github，即使用工作账号进行操作。

	本地建库: 

	> git init

	> git commit-am"first commit'#push到github上去$ git remote add origin git@github_work:xxxx/test.git

	> git push origin master

## 7. Hexo 的常用操作

[官方文档](https://hexo.io/zh-cn/docs/writing.html)建议看看

你可以执行下列命令来创建一篇新文章。

> hexo new [文章名]

您可以在命令中指定文章的布局（layout），默认为post，可以通过修改_config.yml中的default_layout参数来指定默认布局。

[布局](https://hexo.io/zh-cn/docs/writing.html#%E5%B8%83%E5%B1%80%EF%BC%88Layout%EF%BC%89)（Layout）

Hexo 有三种默认布局：post、page和draft，它们分别对应不同的路径，而您自定义的其他布局和post相同，都将储存到source/_posts文件夹。

布局路径

> postsource/_posts

> pagesource

> draftsource/_drafts

不要处理我的文章

如果你不想你的文章被处理，你可以将 Front-Matter 中的layout:设为false。

[文件名称](https://hexo.io/zh-cn/docs/writing.html#%E6%96%87%E4%BB%B6%E5%90%8D%E7%A7%B0)

Hexo 默认以标题做为文件名称，但您可编辑new_post_name参数来改变默认的文件名称，举例来说，设为:year-:month-:day-:title.md可让您更方便的通过日期来管理文章。

变量描述

:title标题（小写，空格将会被替换为短杠）

:year建立的年份，比如，2015

:month建立的月份（有前导零），比如，04

:i_month建立的月份（无前导零），比如，4

:day建立的日期（有前导零），比如，07

:i_day建立的日期（无前导零），比如，7

[草稿](https://hexo.io/zh-cn/docs/writing.html#%E8%8D%89%E7%A8%BF)

刚刚提到了 Hexo 的一种特殊布局：draft，这种布局在建立时会被保存到source/_drafts文件夹，您可通过publish命令将草稿移动到source/_posts文件夹，该命令的使用方式与new十分类似，您也可在命令中指定layout来指定布局。

$ hexo publish [layout]

草稿默认不会显示在页面中，您可在执行时加上--draft参数，或是把render_drafts参数设为true来预览草稿。

[模版（Scaffold）](https://hexo.io/zh-cn/docs/writing.html#%E6%A8%A1%E7%89%88%EF%BC%88Scaffold%EF%BC%89)

在新建文章时，Hexo 会根据scaffolds文件夹内相对应的文件来建立文件，例如：

$ hexo new photo"My Gallery"

在执行这行指令时，Hexo 会尝试在scaffolds文件夹中寻找photo.md，并根据其内容建立文章，以下是您可以在模版中使用的变量：

变量描述

layout布局

title标题

date文件建立日期

Markdown 11种基本语法

引用自http://www.cnblogs.com/hnrainll/p/3514637.html

1. 标题设置（让字体变大，和word的标题意思一样）

在Markdown当中设置标题，有两种方式：

第一种：通过在文字下方添加“=”和“-”，他们分别表示一级标题和二级标题。

第二种：在文字开头加上 “#”，通过“#”数量表示几级标题。（一共只有1~6级标题，1级标题字体最大）

2. 块注释（blockquote）

通过在文字开头添加“>”表示块注释。（当>和文字之间添加五个blank时，块注释的文字会有变化。）

3. 斜体

将需要设置为斜体的文字两端使用1个“*”或者“_”夹起来

4. 粗体

将需要设置为斜体的文字两端使用2个“*”或者“_”夹起来

5. 无序列表

在文字开头添加(*,+, and-)实现无序列表。但是要注意在(*,+, and-)和文字之间需要添加空格。（建议：一个文档中只是用一种无序列表的表示方式）

6. 有序列表

使用数字后面跟上句号。（还要有空格）

7. 链接（Links）

Markdown中有两种方式，实现链接，分别为内联方式和引用方式。

内联方式：This is an [example link](http://example.com/).

引用方式：

I get 10 times more traffic from [Google][1] than from [Yahoo][2] or [MSN][3].

[1]: http://google.com/        "Google"

[2]: http://search.yahoo.com/  "Yahoo Search"

[3]: http://search.msn.com/    "MSN Search"

8. 图片（Images）

图片的处理方式和链接的处理方式，非常的类似。

内联方式：![alt text](/path/to/img.jpg "Title")

引用方式：

![alt text][id]

[id]: /path/to/img.jpg "Title"

9. 代码（HTML中所谓的Code）

实现方式有两种：

第一种：简单文字出现一个代码框。使用`

`。（`不是单引号而是左上角的ESC下面~中的`）

第二种：大片文字需要实现代码框。使用Tab和四个空格。

10. 脚注（footnote）

实现方式如下：

hello[^hello]

[^hello]: hi

11. 下划线

在空白行下方添加三条“-”横线。（前面讲过在文字下方添加“-”，实现的2级标题）

## 8. 结束语

深夜仓促总结的,因为之前已经安装过,所以过程,有些,就不方便截图,实在懒得从新装了,但是基本保证没漏洞,少了部分截图,也绝对可以顺利安装.文章里少部分摘抄了别人的总结,基本我全都放出了原文的链接.对于我转载的原作者,而没有署名的,本着以分享的目的,请多多见谅,哈哈.

最后的最后,我啰里啰嗦的写了一大堆,如果你仔细看完了,并且安装成功了,那么恭喜你加入了这个集体.

愿大家都能写出有质量的技术博客,分享于众吧!
