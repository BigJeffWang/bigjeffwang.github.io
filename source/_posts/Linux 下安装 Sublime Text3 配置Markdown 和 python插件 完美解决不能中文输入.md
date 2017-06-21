---
title: Linux 下安装 Sublime Text3 配置Markdown 和 python插件 完美解决不能中文输入
date: 2017-06-13 18:00:00
---
<h1>目录:</h1>

[TOC]

# 1. 安装sublime text 3
## 1. 安装
### 1.1 安装过程非常简单,在terminal中输入：
> 1.   sudo add-apt-repository ppa:webupd8team/sublime-text-3 #添加sublime text 3的仓库
> 2.   sudo apt-get update #更新软件库
> 3.   sudo apt-get install sublime-text-installer #安装Sublime Text 3

### 1.2 使用
在terminal中输入：
> subl

### 1.3 卸载
> sudo apt-get remove sublime-text-installer

## 2. 安装插件
### 2.1 安装 Package Control 插件管理器
1. 从 Sublime Text 3 官方获取用于安装的代码。([地址请点击这里](https://packagecontrol.io/installation#st3))
1.1 或者从这里粘贴
```
import urllib.request,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```
2. 在sublime text 3的窗口上方,依次点击 View > Show Console 打开的控制台
2.1 ![image.png](http://upload-images.jianshu.io/upload_images/6298250-c41275ef170235a5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
2.2 ![image.png](http://upload-images.jianshu.io/upload_images/6298250-19b2b5daa1725ae3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
3. 把刚才从官网粘贴的代码,复制到控制台的输入框里,并回车
4. 其他一些相关命令如下： 
List Packages 显示所有已安装的插件 
Remove Packages 移除一个指定的插件 
Upgrade Package 更新一个指定的插件 
Upgrade/Overwrite All Packages 更新所有已安装的插件

### 2.2 安装anaconda插件
####2.2.1 介绍
Anaconda 是一个终极 [Python](http://lib.csdn.net/base/python) 插件。它为 ST3 增添了多项 IDE 类似的功能，例如：
-   Autocompletion 自动完成，该选项默认开启，同时提供多种配置选项。
-   Code linting 使用支持 pep8 标准的 PyLint 或者 PyFlakes。因为我个人使用的是另外的 linting 工具，所以我会在 Anaconda 的配置文件 Anaconda.sublime-settings 中将 linting 完全禁用。操作如下: Sublime > Preferences > Package Settings > Anaconda > Settings – User： {“anaconda_linting”: false}
-   McCabe code complexity checker 让你可以在特定的文件中使用 McCabe complexity checker. 如果你对软件复杂度检查工具不太熟悉的话，请务必先浏览上边的链接。
-   Goto Definitions 能够在你的整个工程中查找并且显示任意一个变量，函数，或者类的定义。
-   Find Usage 能够快速的查找某个变量，函数或者类在某个特定文件中的什么地方被使用了。
-   Show Documentation： 能够显示一个函数或者类的说明性字符串(当然，是在定义了字符串的情况下)

####2.2.2 anaconda安装
快捷键 cmd+shift+P 打开 Package Control 来安装其他的插件了。输入 install 然后你就能看见屏幕上出现了 Package Control: Install Package，点击回车然后搜索你想要的插件

![image.png](http://upload-images.jianshu.io/upload_images/6298250-a483d49c60a69ad2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

点击Anaconda安装,当然我已经装过了,所以列表里,没有.

![image.png](http://upload-images.jianshu.io/upload_images/6298250-bcb2465246401a63.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

####2.2.3 配置

1. 打开终端输入
> whereis python
2. 选择Preferences-Package Settings-Anacoda-Settings-Default选项，搜寻“python_interpreter” ， 并将“python_interpreter”：”Python” 改为“python_interpreter”：”/usr/bin/python2.7” (这里根据第一步显示的结果)
2.1 如图:![image.png](http://upload-images.jianshu.io/upload_images/6298250-67d8e5f2052b1b4c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
3. 选择Preferences-Package Settings-Anacoda-Settings-Users选项，键入以下json数据。保存，重启ST3即可。
```
{

    "python_interpreter": "/usr/bin/python2.7",
    "suppress_word_completions": true,
    "suppress_explicit_completions": true,
    "complete_parameters": true,
    "anaconda_linting":false
}
```
4. 测试,接下来，就会发现，ST3编写python代码时会有提示功能。 

![image.png](http://upload-images.jianshu.io/upload_images/6298250-d8f6faf5886b60ec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 2.3 安装Markdown用到的插件和编译器中文汉化插件
[这里有一篇,写的很详细,可以点击看看](http://www.jianshu.com/p/aa30cc25c91b)
- **打开sublime txt3>Ctrl+shift+P > install Package > 复制以下插件名即可安装**:
- **Chinese** : **汉化!**喜欢用英文的,建议不装!
- [MarkDown Editing](https://github.com/SublimeText-Markdown/MarkdownEditing) : 支持Markdown语法高亮；支持Github Favored Markdown语法；自带3个主题。
- [MarkdownPreview](https://github.com/revolunet/sublimetext-markdown-preview)：按CTRL + B 生成网页HTML；在最前面添加[TOC]自动生成目录；
- [OmniMarkupPreviwer](http://theo.im/OmniMarkupPreviewer/)：**实时**在浏览器中预，而MarkdownPreview是需要手动生成的和F5的。览如果双屏的话，应该具有不错的体验。快捷键如下：
  - Ctrl+Alt+O: Preview Markup in Browser. 这个非常有用!!!
  - Ctrl+Alt+X: Export Markup as HTML.
  - Ctrl+Alt+C: Copy Markup as HTML.
- [Markdown TOC](https://github.com/naokazuterada/MarkdownTOC)：编辑MD文件的时候可以查看自动生成，并且可以控制生产目录的层次，不过不会自动跳转。编辑的时候可以看看，如果需要生成的HTML具有超链接跳转的功能，还是用MarkdownPreview吧。
**Sublime Text 系列**
[Sublime Text：学习资源篇](http://www.jianshu.com/p/d1b9a64e2e37)
[Sublime插件：增强篇](http://www.jianshu.com/p/5905f927d01b)
[Sublime插件：Markdown篇](http://www.jianshu.com/p/aa30cc25c91b)
[Sublime插件：C语言篇](http://www.jianshu.com/p/595975a2a5f3)
[Sublime插件：主题篇](http://www.jianshu.com/p/13fedee165f1)
[Sublime插件：Git篇](http://www.jianshu.com/p/3a8555c273d8)
[Sublime 小技巧：文本自动换行显示？](http://www.jianshu.com/p/c75d21d2e967)

# 2. 相对的完美解决汉化问题
*本经验目前在Ubuntu14.04环境下，已有搜狗输入法 for Linux和Sublime Text 3的情况下安装成功。*
步骤:
1. 安装 C/C++ 的编译环境和 gtk libgtk2.0-dev
  > 1. sudo apt-get install build-essential
  > 2. sudo apt-get install libgtk2.0-dev
2. 保存下面的代码到文件sublime_imfix.c(位于~目录)
  ```
#include <gtk/gtkimcontext.h>
void gtk_im_context_set_client_window (GtkIMContext *context,
         GdkWindow    *window)
{
 GtkIMContextClass *klass;
 g_return_if_fail (GTK_IS_IM_CONTEXT (context));
 klass = GTK_IM_CONTEXT_GET_CLASS (context);
 if (klass->set_client_window)
   klass->set_client_window (context, window);
 g_object_set_data(G_OBJECT(context),"window",window);
 if(!GDK_IS_WINDOW (window))
   return;
 int width = gdk_window_get_width(window);
 int height = gdk_window_get_height(window);
 if(width != 0 && height !=0)
   gtk_im_context_focus_in(context);
}
```
3. 将上一步的代码编译成共享库libsublime-imfix.so，命令
  > 1. cd ~
  > 2. gcc -shared -o libsublime-imfix.so sublime_imfix.c  `pkg-config --libs --cflags gtk+-2.0` -fPIC
4. 然后将libsublime-imfix.so拷贝到sublime_text所在文件夹
  > sudo mv libsublime-imfix.so /opt/sublime_text/
5. 修改文件/usr/bin/subl的内容
  > 1. sudo gedit /usr/bin/subl
  > 2. 将源文件修改
  ```
  \#!/bin/sh 
  exec /opt/sublime_text/sublime_text "$@"
  ```
  修改为
  ```
  \#!/bin/sh
  export LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so
  exec /opt/sublime_text/sublime_text "$@"
  ```
6. 此时，在命令中执行 subl 将可以使用搜狗for linux的中文输入
7. 为了使用鼠标右键打开文件时能够使用中文输入，还需要修改文件sublime_text.desktop的内容。
  1. > sudo gedit /usr/share/applications/sublime_text.desktop
  将[Desktop Entry]中的字符串
  Exec=/opt/sublime_text/sublime_text %F
  修改为
  Exec=bash -c "LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so exec  /opt/sublime_text/sublime_text %F"
  2. > 将[Desktop Action Window]中的字符串
  Exec=/opt/sublime_text/sublime_text -n
  修改为
  Exec=bash -c "LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so exec   /opt/sublime_text/sublime_text -n"
  3. > 将[Desktop Action Document]中的字符串
  Exec=/opt/sublime_text/sublime_text --command new_file
  修改为
  Exec=bash -c "LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so exec   /opt/sublime_text/sublime_text --command new_file"
  4. > 注意：
  修改时请注意双引号"",否则会导致不能打开带有空格文件名的文件。
  此处仅修改了/usr/share/applications/sublime-text.desktop，但可以正常使用了。
  opt/sublime_text/目录下的sublime-text.desktop可以修改，也可不修改。


**经过以上步骤我们能在Sublime中输入中文了。如果感觉对你有帮助的话,请给我点个赞或分享给他人**

分销几个别人总结的Markdown的文章:
- [Markdown 语法手册 （完整整理版）][1]
- [Markdown 语法说明 (简体中文版)][2]
- 
[1]: (http://blog.leanote.com/post/freewalk/Markdown-%E8%AF%AD%E6%B3%95%E6%89%8B%E5%86%8C#title-5)
[2]: (http://www.appinn.com/markdown/#header)
