---
title: Selenium 2 自动化测试实例
date: 2017-06-13 18:00:00
---

Selenium 2 自动化测试实例 更新中...

目录:

[TOC]

# 1. 自动化测试基础
## 1.1 软件测试分类
### 1. 根据项目流程阶段划分测试
1. 单元测试: 单个子程序测试
2. 集成测试: 模块由多个单元集成成子系统再测试
3. 系统测试: 针对整个产品系统的测试
4. 验收测试: 部署软件之前的最后一个测试阶段

### 2. 白盒测试、黑盒测试、灰盒测试
1. 黑盒：只关心软件的输入数据和输出结果
2. 白盒：产品内部动作和代码逻辑是否按照设计规格进行
3. 灰盒：介于黑盒和白盒之间，既关注输入输出的正确性，同时也关注内部的表现

### 3. 功能测试和性能测试
1. 功能测试：逻辑功能测试、界面测试、易用性测试、安装测试、兼容性测试等等
2. 性能测试：
    - 时间性能：具体响应时间
	- 空间性能：消耗占用系统资源，例如硬件资源，CPU、内存、网络带宽消耗等

### 4. 手工测试与自动化测试
1. 手工测试：由测试人员一个一个地去执行测试用例
2. 自动化测试：把人为驱动的测试行为转化为机器执行的一种过程
	- 功能自动化测试：测试工具（或者框架）录制/编写测试脚本，对软件的功能进行测试，并验证测试结果是否正确，从而替代部分手工测试工作，达到节约时间成本、人力成本
	- 性能自动化测试：通过性能工具来模拟成千上万的虚拟用户向系统发送请求，具而验证系统的处理能力

### 5. 冒烟测试、回归测试、随机测试、探索型测试和安全测试
1. 冒烟测试：先验证具体的基本功能是否实现，是否具备进行大规模系统测试
2. 回归测试：修改之后的旧代码，从新测试，检测有没有引进新的错误或者导致其他代码产生错误
3. 随机测试：输入数据是随机生成的，其目的是模拟用户的真实操作，并发现一些边缘型的错误
4. 探索性测试：一种测试思维方式，强调在碰到问题时及时改变测试策略		

## 1.2 分层的自动化测试
测试金字塔的概念由敏捷大师 Mike Cohn 在他的 Succeeding with agile 一书中首次提出。  
基本观念是：我们应该有更多的低级别的单元测试，而不仅仅是通过用户界面运行的端到端的测试。

所谓传统的自动化测试我们可以理解为基于产品的UI层的自动化测试，它是将黑盒功能测试转化为由程序或者工具执行的一种自动化测试。  
UI自动化测试成本维护高昂，UI易变。  
分层自动化测试倡导的是由黑盒（UI）单层到黑白盒多层的自动化测试体系，从全面的黑盒自动化测试到对系统的不同曾次进行自动化测试。

1. 单元自动化测试
	- 是指针对软件的最小可测试单元进行检查和验证。对于单元测试中的单元的含义，一般来说c语言是指一个函数，Java是指一个类，图形化软件是一个窗口或者菜单，需要用到测试框架。
		+ Java：Junit、TestNG
		+ C#：NUnit
		+ python：unittest、pytest
	- Code Review 代码审查
		+ Java：Eclipse的ReviewClipse和Jupiter
		+ python：Review Board
2. 接口自动化测试
	- 模块接口测试
		+ 测试模块之间的调用与返回，强调一个类方法或者函数的调用，并对返回结果的验证，同单元自动化测试
	- Web接口测试
		+ 服务器接口测试：是指测试浏览器与服务器的接口，通过HTTP协议实现前后端的数据传递测试
		+ 外部接口测试：指调用的接口由第三方系统提供，典型例子就是第三方登录，用户登录信息的验证由第三方完成，并返回给当前系统是否验证通过
	- 当然，接口测试也有类库或者工具，例如测试HTTP的有HttpUnit、Postman等
3. UI自动化测试
	- UI测试工具：UFT、Watir、Robot Framework、Selenium
	- 前端：QUnit就是针对JavaScript的单元测试工具

《Google测试之道》 一书中提到，测试类型分为大、中、小测试，采用比例1:2:7，大体对应UI层、Service、Unit  

| UI层 | Service | Unit |
|:-:|:-:|:-:|
|大|中|小|
|10%|20%|70%|

## 1.3 什么项目适合做自动化测试
1. 任务测试明确，不会频繁变动
2. 每日构建后的测试验证
3. 比较频繁的回归测试
4. 软件系统的界面稳定，变动少
5. 需要在多平台上运行的测试案例，组合便利型的测试，大量的重复任务
6. 软件维护周期长
7. 项目进度压力不算太大
8. 被测软件系统开发较为规范，能够保证系统的可测试性
9. 具备大量的自动化测试平台
10. 测试人员较强的变成能力

## 1.4 市面上常见的自动化测试工具
1. UFT：HP开发，QTP与ST合并而来。企业级自测工具，提供强大医用的录制回放功能，兼容对象识别模式与图像识别模式两种识别方式，支持B/S C/S两种架构
2. Robot Framework：基于Python编写的自动化测试框架，可扩展，支持关键字，同时可以测试多种客户端或者接口，可以分布式测试
3. Watir：基于Web模式的自动化功能测试工具。Wair是一个Ruby语言库
4. Selenium：是一个Web应用程序测试工具，支持多平台、多浏览器、多语言，应用广泛

## 1.5 Selenium工具介绍
基于Web应用程序的自动化测试，但不局限于此，它还支持所有基于web的管理任务自动化

特点：

- 开源免费
- 多浏览器支持：Firefox、Chrome、IE、Opera、Edge
- 多平台支持：Linux、windows、Mac
- 多语言：Java、Python、Ruby、JavaScript、C#、C++
- 对web页面的良好的支持
- 简单API、灵活（用开发语言驱动）
- 支持分布式测试用例
 
Selenium：

- Selenium IDE：嵌入火狐Firefox的一个插件，实现简单的浏览器操作录制、回放，快速创建bug重现脚本，通过IDE将重现的步骤记录下来，重现BUG
- Selenium Grid：自动化测试辅助工具，Grid通过利用现有的计算机基础设施，能加快Web-App的功能测试，利用Grid可以很方便的实现多台机器上和异构环境中测试用例
- Selenium RC：家族的核心部分，通过Selenium RC的服务器作为代理服务器去访问应用。Selenium Libraries库主要用于编写测试脚本，用来控制Selenium Server库。Selenium Server负责控制浏览器行为。
	+ client
	+ Server
		* Launcher：用于启动浏览器，把Selenium Core加载到浏览器页面当中，并把浏览器的代理设置为Selenium Server的Http Proxy
		* Http Proxy：代理服务器(Proxy)是网络信息的中转站
		* Core：是被Selenium Server嵌入到到浏览器的页面中，其实 Selenium Core就是一堆JavaScript函数的集合，通过这些JS函数，可以实现程序对浏览器的操作

Selenium 2.0 = Selenium 1.0 + WebDriver  
WebDriver是Selenium RC的替代品，为了保持向下兼容，并没有完全抛弃 Selenium Core，新的项目可以直接使用WebDriver

- Selenium RC：是在浏览器中运行JS脚本，使用浏览器内置的JS的编译器来翻译和执行selenese（selenese是Selenium命令合集）
- WebDriver：是通过原生浏览器支持或者浏览器扩展来直接控制浏览器。WebDriver针对各个浏览器而开发，取代了嵌入到被测Web应用中的JavaScript，与浏览器紧密集成，因此支持创建更高级的测试，便面的JavaScript安全模型导致的限制，还利用操作系统级别的调用，模拟用户输入。可以绕过JavaScript沙箱

## 1.6 前端技术介绍
1. HTML
2. JavaScript
3. XML

## 1.7 前端工具介绍
1. FireBug
2. FirePath：快速检查和生成XPath1.0表达式
3. Chrome、IE

## 1.8 开发语言选择
本文选择的是Python


# 2. 测试环境搭建
## 2.1 Windows下的环境搭建
### 2.1.1 安装Python
### 2.1.2 安装setuptools与pip
### 2.1.3 安装Selenium
### 2.1.4 ActivePython
- Python专用编程和调试工具，包含Python内核，同时可以访问Windows API的所有服务
- 集成PIP，可以用PIP安装Selenium库

## 2.2 Ubuntu下环境搭建

## 2.3 使用IDLE编写Python

## 2.4 编写第一个自动化脚本
在执行程序的时候，如果遇到错误代码是如下样子：  

> selenium.common.exceptions.WebDriverException: Message: 'geckodriver' executable needs to be in PATH.   

则需要下载 geckodriver驱动文件，放在/usr/local/bin目录里。  
下载网址是：[https://github.com/mozilla/geckodriver/releases/](https://github.com/mozilla/geckodriver/releases/)  
如果是Linux系统，下载文件名是：geckodriver-v0.16.1-linux64.tar.gz （最新版本即可）

```
# coding:utf-8
from selenium import webdriver
from time import sleep

driver = webdriver.Firefox()
driver.get("http://www.baidu.com")

driver.find_element_by_id("kw").send_keys("Selenium2")
driver.find_element_by_id("su").click()

sleep(5)
driver.quit()
```

## 2.5 安装浏览器驱动
地址：[Selenium - Web Browser Automation](http://www.seleniumhq.org/download)

如果打不开，百度搜索相应的驱动。安装位置，Windows安装在path环境变量下，Linux安装在/usr/local/bin  
[FireFoxdriver地址](https://addons.mozilla.org/en-US/firefox/addon/selenium-expert-selenium-ide/)  
[Chromedriver地址](http://chromedriver.storage.googleapis.com/2.26/chromedriver_linux64.zip)  
[IEdriver地址](http://selenium-release.storage.googleapis.com/index.html) 需要对应你的Selenium版本  [windows下 IEDriver相关设置](http://blog.csdn.net/jichuang123/article/details/53008581)
[HTMLTestRunner.py地址](https://pypi.python.org/pypi/HTMLTestRunner)


```
sudo apt-get install xvfb
sudo apt-get install unzip

wget -N http://chromedriver.storage.googleapis.com/2.26/chromedriver_linux64.zip
unzip chromedriver_linux64.zip
chmod +x chromedriver

sudo mv -f chromedriver /usr/local/share/chromedriver
sudo ln -s /usr/local/share/chromedriver /usr/local/bin/chromedriver
sudo ln -s /usr/local/share/chromedriver /usr/bin/chromedriver
```
[FireFox驱动地址](https://addons.mozilla.org/en-US/firefox/addon/selenium-expert-selenium-ide/)


```
selenium官方加上第三方宣布支持的驱动有很多种；除了PC端的浏览器之外，还支持iphone、Android的driver；大概记录一下selenium支持的各种driver的用途与说明。
selenium可支持的PC浏览器驱动包括：
FF driver【包含在各自语言的客户端里】
safari driver【包含在selenium server中】
ie driver
chrome driver 【第三方】
opera driver【第三方】

selenium可支持的伪浏览器驱动：
PhantomJS Driver【第三方】
HtmlUnit Driver【包含在selenium server中】

selenium可支持的移动端驱动：
Windows Phone driver 【第三方】
Selendroid -Selenium for android【第三方】
ios-driver 【第三方】
Appium  支持iphone、ipad、android、FirefoxOS【第三方】
上述的所有驱动不仅可以直接通过各自语言客户端来调用，还是注册到selenium grid中进行分布式的远程调用。

因为移动端的driver都没有尝试过，所以就不做说明。PC端的driver都是基于浏览器的，主要分为2种类型：
一种是真实的浏览器driver
比如：safari、ff都是以插件形式驱动浏览器本身的；ie、chrome都是通过二进制文件来驱动浏览器本身的；
这些driver都是直接启动并通过调用浏览器的底层接口来驱动浏览器的，因此具有最真实的用户场景模拟，主要用于进行web的兼容性测试使用。

一种是伪浏览器driver
selenium支持的伪浏览器包括htmlunit、PhantomJS；他们都不是真正的在浏览器、都没有GUI，而是具有支持html、js等解析能力的类浏览器程序；这些程序不会渲染出网页的显示内容，但是支持页面元素的查找、JS的执行等；由于不进行css及GUI渲染，所以运行效率上会比真实浏览器要快很多，主要用在功能性测试上面。
htmlunit是Java实现的类浏览器程序，包含在selenium server中，无需驱动，直接实例化即可；其js的解析引擎是Rhino
PhantomJS是第三方的一个独立类浏览器应用，可以支持html、js、css等执行；其驱动是Ghost driver在1.9.3版本之后已经打包进了主程序中，因此只要下载一个主程序即可；其js的解析引擎是chrome 的V8。

driver类型	优点	缺点	应用
真实浏览器driver	真实模拟用户行为	效率、稳定性低	兼容性测试
HtmlUnit	速度快	js引擎不是主流的浏览器支持的	包含少量js的页面测试
PhantomJS	速度中等、模拟行为接近真实	不能模拟不同/特定浏览器的行为	非GUI的功能性测试
PS：除上述的几种真实浏览器driver中，也可以通过不同的手段来取消浏览器的css解析、界面渲染等目的；这样既可以保证浏览器的真实兼容性、也可以提高执行效率问题；使用的手段有：autoit、pyvirtualdisplay、浏览器设置等。
```

## 2.6 不同语言使用WebDriver
- 导入selenium（WebDriver）相关模块
- 调用浏览器驱动，获取浏览器句柄，并启动
- 通过句柄访问地址百度
- 通过句柄操作页面元素（百度输入框和按钮）
- 通过句柄关闭浏览器


# 3. Python基础
## 3.1 Python哲学
## 3.2 输入输出
## 3.3 分支与循环
## 3.4 数组与字典
## 3.5 函数、类和方法
## 3.6 模组、类库、模块
当多个模块之间存在引用，模块内之间文件里的类存在继承和引用关系  
需要在模块内创建一个空的__init__.py文件  
当一个模块调用另一个模块的时候  
用：  
```
import sys  
sys.path.append("./model")  # (model就是相应的被引用模块)  
from model import new_count
```

# 4. WebDriver API
## 4.1 从定位元素开始
WebDriver在Python中一个有8种方法找到页面元素：  

标签|定位元素
:-|:-
id|name
class name|tag name
link text|partial link text
xpath|css selector
find_element_by_id()|find_element_by_name()
find_element_by_class_name()|find_element_by_tag_name()
find_element_by_link_text()|find_element_by_partial_link_text() 通过部分文字定位
find_element_by_xpath()|find_element_by_css_selector()

XPath定位：  
绝对路径定位  
find_element_by_xpath("/html/body/div/div[2]/div/div/from/span/input")

利用元素属性定位：  
find_element_by_xpath("//input[@id='kw']")  
find_element_by_xpath("//input[@name='wd']")  
find_element_by_xpath("//input[@class='s_ipt']")  
find_element_by_xpath("//*[@class='s_ipt']")  
find_element_by_xpath("//input[@maxlength='100']")  
find_element_by_xpath("//input[@autocomplete='off']")  
find_element_by_xpath("//input[@type='submit']")  

层级与属性结合：  
find_element_by_xpath("//span[@class='bg_s_ipt_wr']/input")  
find_element_by_xpath("//form[@id='form']/span/input")

使用逻辑运算符：  
find_element_by_xpath("//input[@id='kw' and @class='su']/span/input")

css定位  
通过class属性定位：
find_element_by_css_selector(".s_ipt")  
find_element_by_css_selector(".bg s_btn")

通过id属性定位：  
find_element_by_css_selector("#kw")  
find_element_by_css_selector("#su")

通过标签名定位：
find_element_by_css_selector("input")  
find_element_by_css_selector("span>input")

通过属性定位：
find_element_by_css_selector("[autocomplete=off]")  
find_element_by_css_selector("[name='kw']")  
find_element_by_css_selector("[type='submit']")

组合定位：
find_element_by_css_selector("form.fm>span>input.s_ipt")  
find_element_by_css_selector("form.fm>span>input#kw")

用by定位元素  
略过。。

## 4.2 控制浏览器
## 4.3 元素控制
命令|效果
:-|:-
driver.set_window_size(480,800)|控制浏览器宽400高800
driver.get(url)|获取url地址页面
driver.forward()|前进
driver.back()|后退
driver.quit()|退出
driver.refresh()|刷新页面
driver.find_element_by_css_selector("#id").clear()|清除文本
driver.find_element_by_css_selector("#id").send_keys("abc")|模拟按键输入
driver.find_element_by_css_selector("#id").click()|单击元素
driver.find_element_by_css_selector("#id").submit()|提交
size = driver.find_element_by_css_selector("#id").size|输入框的尺寸
driver.find_element_by_css_selector("#id").text|文本
driver.find_element_by_css_selector("#id").get_attribute()|获取id、name、type其他任意属性
driver.find_element_by_css_selector("#id").is_displayed()|返回元素结果是否可见

## 4.4 鼠标事件
命令|效果
:-|:-
perform()|执行所有ActionChains中储存的行为
context_click()|右击
double_click()|双击
drag_and_drop()|拖动
move_to_element()|鼠标悬停

```
# coding:utf-8
from selenium import webdriver
from selenium.webdriver.common.action_chains import ActionChains

driver = webdriver.Firefox()
driver.get("https://www.baidu.com/")
# 定位右击的元素
right_click = driver.find_element_by_id("su")
# 执行右击操作
ActionChains(driver).context_click(right_click).perform()

# 将浏览器句柄driver作为参数，传入ActionChains行动链
# context_click() 鼠标右击操作，需要传入元素定位
# perform() 可以理解为对所有行动操作列表的提交
# ActionChains(driver).move_to_element(above).perferm() 鼠标悬停
# ActionChains(driver).double_click(double_click).perferm() 鼠标双击
# element, target = driver.find_element_by_id("xx"), driver.find_element_by_id("xx")
# ActionChains(driver).drag_and_drop(element, target).perferm() 鼠标拖放

```

## 4.5 键盘事件
```
# coding:utf-8
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from time import sleep

driver = webdriver.Firefox()
driver.get("https://www.baidu.com/")

driver.find_element_by_id("kw").send_keys("seleniumm")
# driver.find_element_by_id("su").click()

driver.find_element_by_id("kw").send_keys(Keys.BACK_SPACE)  # 回退 删除

# driver.find_element_by_id("kw").send_keys(Keys.SPACE)  # 添加空格
driver.find_element_by_id("kw").send_keys(u" ")  # 添加空格

driver.find_element_by_id("kw").send_keys(u"教程")  # 添加文字

driver.find_element_by_id("kw").send_keys(Keys.CONTROL, 'a')  # 输入框全选

driver.find_element_by_id("kw").send_keys(Keys.CONTROL, 'x')  # 输入框剪切

driver.find_element_by_id("kw").send_keys(Keys.CONTROL, 'v')  # 输入框复制

driver.find_element_by_id("kw").send_keys(Keys.ENTER)  # 回车代替单击

sleep(5)

driver.quit()
```

常用键盘操作：
操作|效果
:-|:-
send_keys(Keys.BACK_SPACE)|删除
send_keys(Keys.SPACE)|空格
send_keys(Keys.TAB)|制表符
send_keys(Keys.ESCAPE)|回退
send_keys(Keys.ENTER)|回车
send_keys(Keys.CONTROL, 'a')|全选
send_keys(Keys.CONTROL, 'c')|复制
send_keys(Keys.CONTROL, 'v')|粘贴
send_keys(Keys.CONTROL, 'x')|剪切
send_keys(Keys.F1)|键盘F1
send_keys(Keys.F12)|键盘F12

## 4.6 获取验证信息
title = driver.title  
now_url = driver.current_url  
user = driver.find_element_by_id('spanUid').text

## 4.7 设置元素等待
WebDirverWait(driver, 5, 0.5)  
WebDirverWait(driver, timeout, poll_frequency=0.5, ignored_exceptions=None)
- driver:浏览器驱动
- timeout：超时时长
- poll_frequency:间隔时长
- ignored_exceptions:超时后的异常信息

```
# coding:utf-8

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.keys import Keys
import time
driver = webdriver.Firefox()
driver.get("https://www.baidu.com")

element = WebDriverWait(driver, 5, 0.5).until(
    EC.presence_of_all_elements_located((By.ID, "kw"))
)

driver.find_element_by_id("kw").send_keys('selenium')
driver.find_element_by_id("kw").send_keys(Keys.ENTER)
# element.send_keys('selenium')
time.sleep(5)
driver.quit()

# until(method, message='') 调用该方法提供的驱动程序作为一个参数，直到返回为True

```

第二种方法：  
隐式等待 implicitly_wait()

```
# coding:utf-8

from selenium import webdriver
from selenium.common.exceptions import NoSuchElementException
from time import ctime

driver = webdriver.Firefox()
driver.implicitly_wait(10)  # 休眠时间
driver.get("http://www.baidu.com")
try:
    print(ctime())
    driver.find_element_by_id("kw22").send_keys('selenium')
except NoSuchElementException as e:
    print(e)
finally:
    print(ctime())
    driver.quit()
```

第三种方法：
sleep  
from time import sleep
sleep(10)

## 4.8 复选
```
# coding:utf-8

from selenium import webdriver
import os, time

driver = webdriver.Firefox()
file_path = 'file:///' + os.path.abspath('checkbox.html')  # abspath()返回绝对路径
driver.get(file_path)

# inputs = driver.find_element_by_tag_name('input')
# 
# for i in inputs:
#     if i.get_attribute('type') == 'checkbox':
#         i.click()
#         time.sleep(1)

# checkboxs = driver.find_elements_by_xpath("//input[@type='checkbox']")
checkboxs = driver.find_elements_by_css_selector("input[type=checkbox]")

for checkbox in checkboxs:
    checkbox.click()
    time.sleep(1)

driver.find_elements_by_css_selector('input[type=checkbox]').pop().click()  # 去掉最后一个

# pop(0) 第一个
# pop(-1) 最后一个
# pop(1) 第二个

driver.quit()
```

## 4.9 多表单切换
```
driver.switch_to.frame("if")  # 切换到id = if的frame框架，frame()可以去id或者name属性 或者
xf = driver.find_element_by_xpath("//*[@class='if']")
driver.switch_to.frame(xf)
switch_to.default_content()  # 跳到最外层表单
```

## 4.10 多窗口切换
```
# coding:utf-8

from selenium import webdriver
import time

driver = webdriver.Firefox()
driver.implicitly_wait(10)
driver.get("http://www.baidu.com")

# 获得百度搜索窗口句柄
sreach_windows = driver.current_window_handle
# a.lb:nth-child(7)
# html body div#wrapper div#head div.head_wrapper div#u1 a.lb

# a_links = driver.find_element_by_css_selector("a.lb:nth-child(7)")
# print a_links.text

# links = driver.find_elements_by_link_text('登录')
# print links

driver.find_elements_by_link_text('登录').pop().click()
driver.find_element_by_link_text("立即注册").click()

# driver.find_element_by_link_text('登录').click()
# driver.find_element_by_link_text("立即注册").click()

# 获得当前所有打开的窗口的句柄
all_handles = driver.window_handles

# 进入注册窗口
for handle in all_handles:
    if handle != sreach_windows:
        driver.switch_to.window(handle)
        print 'now register window!'
        driver.find_element_by_name("account").send_keys('username')
        driver.find_element_by_name("password").send_keys('password')
        time.sleep(2)

# 回到搜索窗口
for handle in all_handles:
    if handle == sreach_windows:
        print 'now sreach window'
        driver.find_element_by_id('TANGRAM__PSP_2__closeBtn').click()
        driver.find_element_by_id("kw").send_keys("selenium")
        driver.find_element_by_id("su").click()
        print driver.current_window_handle
        time.sleep(5)

driver.quit()
```

## 4.11 警告框处理
switch_to_alert()方法 定位到 alert/confirm/prompt  
text/accept/dismiss/send_keys等方法进行操作
命令|效果
:-|:-
text|返回alert/confirm/prompt中的文字
accpet()|接受现有警告框
dismiss()|解散现有警告框
send_keys(keysToSend)|发送文本至警告框 keysToSend:将文本发送至警告框
switch_to_alert()|方法接受弹出来的窗口
```
# coding:utf-8
from selenium import webdriver
from selenium.webdriver.common.action_chains import ActionChains
import time

driver = webdriver.Firefox()
driver.implicitly_wait(10)
driver.get("http://www.baidu.com")

# 鼠标悬停至“设置”链接
# link = driver.find_element_by_link_text('设置')
link = driver.find_elements_by_link_text('设置').pop()
ActionChains(driver).move_to_element(link).perform()

# 打开搜索设置
# time.sleep(5)
# print driver.find_element_by_link_text('搜索设置')
driver.find_element_by_link_text('搜索设置').click()

js = "var q=document.getElementsByClassName(\"bdlayer pfpanel\");q.style=\"display: block; top: 0px; opacity: 1;\""
driver.execute_script(js)
time.sleep(3)

# res = driver.find_element_by_css_selector(".bdlayer.pfpanel")
# print res
# print res.is_displayed()

# 设置
driver.find_element_by_css_selector("#sh_1").click()

# 保存设置
# driver.find_element_by_class_name("prefpanelgo").click()
driver.find_element_by_css_selector(".prefpanelgo").click()
# driver.find_element_by_link_text('恢复默认').click()
time.sleep(2)

# 接受警告框
driver.switch_to_alert().accept()

driver.quit()
```

## 4.12
### 4.12.1 send_keys实现上传
找到对应的input标签，直接send_keys(文件),传入对应文件
```
# coding:utf-8
from selenium import webdriver
import os

driver = webdriver.Firefox()
driver.implicitly_wait(5)
file_path = 'file:///' + os.path.abspath('upfile.html')
driver.get(file_path)

# 定位上传的input，添加本地文件
driver.find_element_by_name('file').send_keys('D:\\upload_file.txt')

driver.quit()

```
### 4.12.2 AutoIt实现上传
官方下载地址：[http://www.aotuitscript.com/site/](http://www.aotuitscript.com/site/)
windows GUI(图形用户界面)自动化测试

功能|作用
:-|:-
AutoIt Windows Info|用于识别Windows控件信息
Compile Script to.exe|用于将AutoIt生成exe执行文件
Run Script|用于执行AutoIt脚本
SciTE Script Editor|用于编写AutoIt脚本

### 4.13 下载文件
WebDriver允许我们设置默认的文件下载路径，也就是说，文件会自动下载并且存放到设置的目录中。  
HTTP Content-type 常用对照表：[http://tool.oschina.net/commons](http://tool.oschina.net/commons)  
curl -I 可以查看Content-type的值  
```
# coding:utf-8

from selenium import webdriver
import os

fp = webdriver.FirefoxProfile()

fp.set_preference("browser.download.folderList", 2)  # 设置成0代表保存在默认的浏览器下载目录，设置2代表保存在指定的目录
fp.set_preference("browser.download.manager.showWhenStarting", False)  # 是否显示开始 True为显示，False为不显示
fp.set_preference("browser.download.dir", '/home/wy/')
# fp.set_preference("browser.download.dir", os.getcwd())  # 设置下载目录 os.getcwd()当前的目录
fp.set_preference("browser.helperApps.neverAsk.saveToDisk", "application/octet-stream")  # 下载文件的类型 指定要下载页面的Content-type值，‘application/octet-stream’为文件类型

driver = webdriver.Firefox(firefox_profile=fp)
driver.get("https://pypi.python.org/pypi/selenium#downloads")
# driver.find_element_by_css_selector(".button.green").click()
# driver.find_element_by_partial_link_text("selenium-2").click()

driver.find_element_by_css_selector(".even>td>span>a").click()

driver.quit()
```

Chrome浏览器类似，设置其options：  
download.default_directory：设置下载路径  
profile.default_content_settings.popups：设置为 0 禁止弹出窗口  
它的设置就简单多了，看个示例：  

```
# -*- coding: utf-8 -*-

from selenium import webdriver
from time import sleep


options = webdriver.ChromeOptions()
prefs = {'profile.default_content_settings.popups': 0, 'download.default_directory': 'd:\\'}
options.add_experimental_option('prefs', prefs)

driver = webdriver.Chrome(executable_path='D:\\chromedriver.exe', chrome_options=options)
driver.get('http://sahitest.com/demo/saveAs.htm')
driver.find_element_by_xpath('//a[text()="testsaveas.zip"]').click()
sleep(3)
driver.quit()
```

### 4.14 操作Cookie
操作|效果
:-|:-
get_cookies()|获得所有cookie信息
get_cookie(name)|返回字典的key为"name"的cookie信息
add_cookie(cookie_dict)|添加cookie ‘cookie_dict’指字典对象，必须有name和value值
delete_cookie(name,optionsString)|删除cookie信息 “name”是要删除的cookie的名称，“optionsString”是该cookie的选项，目前支持的选项包括“路径”，“域”
delete_all_cookies()|删除所有cookie信息
```
# coding:utf-8
from selenium import webdriver

driver = webdriver.Firefox()
driver.implicitly_wait(3)

# 添加cookie
driver.add_cookie({'name': 'key-aaa', 'value': 'key-bbb'})

driver.get("http://www.youdao.com")

# 获得cookie信息
cookies = driver.get_cookies()

print cookies

for cookie in cookies:
    print cookie['name'], '->', cookie['value']
driver.quit()
```

### 4.15 调用JavaScript

```
# coding:utf-8
from selenium import webdriver
from time import sleep

driver = webdriver.Firefox()
driver.get("http://www.baidu.com")

# 设置浏览器窗口大小
driver.set_window_size(600, 600)

# 搜索
driver.find_element_by_id("kw").send_keys("selenium")
driver.find_element_by_id("su").click()
sleep(2)

# 通过JS设置浏览器窗口的滚动条位置
js = "window.scrollTo(100,450)"
driver.execute_script(js)
sleep(3)

driver.quit()

```
### 4.16 处理HTML5的视频播放
```
# coding:utf-8

from selenium import webdriver
from time import sleep

driver = webdriver.Firefox()
driver.implicitly_wait(5)
driver.get("http://videojs.com/")

video = driver.find_element_by_xpath(".//*[@id='preview-player_html5_api']")
# video = driver.find_element_by_xpath("body/Section[1]/div/video")

# 返回播放文件地址
url = driver.execute_script("return arguments[0].currentSrc;", video)
print url

# 播放视频
print "start"
driver.execute_script("return arguments[0].play()", video)

sleep(15)

# 暂停视频
print "pause"
driver.execute_script("arguments[0].pause()", video)

driver.quit()

```

### 4.17 窗口截图
```
# coding:utf-8

from selenium import webdriver
from time import sleep

driver = webdriver.Firefox()
driver.get('http://www.baidu.com')

driver.find_element_by_id('kw').send_keys('selenium')
driver.find_element_by_id('su').click()
sleep(2)

# 截取当前窗口，并指定截图保存位置
driver.get_screenshot_as_file("/home/wy/")

driver.quit()
```

### 4.18 关闭窗口
driver.close()

### 4.19 验证码的处理
1. 叫开发人员去掉验证码
2. 设置万能验证码
3. Python-tesseract光学识别 Tesseract OCR引擎的封装类
4. 记录 cookie 绕过验证码

```
# ...
# 访问某网站...

driver.get("http://xxx.com")

driver.add_cookie({'name':'Login_UserNumber','value':'username'})
driver.add_cookie({'name':'Login_Password','value':'password'})
```

### 4.20 WebDriver原理
1. WebDriver启动浏览器，绑定指定端口，作为Remote Server
2. Client 通过CommandExcuter发送HTTPRequest给Remote Server帧听端口
3. Remote Server需要依赖原声的浏览器组件 转化浏览器的native调用


接收客户端DEBUG
```
# coding:utf-8
from selenium import webdriver
import logging

logging.basicConfig(level=logging.DEBUG)
driver = webdriver.Firefox()
driver.get("http://www.baidu.com")

driver.find_element_by_id("kw").send_keys("selenium")
driver.find_element_by_id("su").click()

driver.quit()
```
# 5. 自动化测试模型
测试模型：
1. 线性测试
2. 模块化驱动测试
3. 数据驱动测试
4. 关键字测试

## 5.1 自动化测试模型介绍
### 5.1.1 线性测试
通过录制或编写对应用程序的操作步骤产生相应的线性脚本，每个测试脚本相对独立，且不产生其他依赖与调用，这是早期的自动化测试的形式，  
单纯的模拟用户完整的操作场景，优势完整独立，缺点开发和维护的成本很高

### 5.1.2 模块化测试
把重复的操作独立成公共模块，当用例执行过程中用到这一个模块时，则被调用，最大限度的消除了重复，提高可维护性

### 5.1.3 数据驱动测试
数据驱动说的直白一点就是数据的参数化，因为输入数据的不同而引起不同的输出结果 Datapool

### 5.1.4 关键字驱动
无法是把"数据"换成"关键字"，通过关键字的改变引起测试结果的改变  
目前市面上的典型关键字驱动工具 QTP(目前已更名UFT-Unified Functional Testing)、Robot Framework(RIDE)工具为主  
这类工具封装了底层的代码，提供用户独立的图形界面，以"填表格"的形式免除测试人员对写代码的恐惧，从而减低编写难度



# 6. selenium IDE
不用翻墙的 安装地址：[https://addons.mozilla.org/en-US/firefox/addon/selenium-ide/](https://addons.mozilla.org/en-US/firefox/addon/selenium-ide/)
# 7. unittest 单元测试框架

# 8. 自动化测试高级应用

# 9. Selenium Grid2

# 10. Python多线程

# 11. 自动化测试实战
- mztestpro/目录
	+ bbs/	论坛项目
		* data/	存放测试数据
		* report/	用于存放HTML测试报告
			- image/	创建了image目录用于存放测试过程中的截图
		* test_case/	测试用例目录，用于存放测试用例及相关模块
			- models/	该目录下存放了一些公共的配置函数及公共类
				+ driver.py 
				+ function.py
				+ myunit.py
			- page_obj/		该目录用于存放测试用例的页面对象(Page Object)，根据自定义规则，以“*Page.py”命名的文件为封装的页面对象文件
				+ *Page.py
			- *_sta.py 	测试用例文件。根据测试文件匹配规则，”*_sta.py“命名的文件将被当作自动化测试用例执行
	+ driver/
	+ package/
	+ run_bbs_test.py
	+ startup.bat
	+ 自动化测试项目说明文档.md


# 12. BDD框架指Lettuce入门

# 13. GitHub托管项目

# 14. 持续继承Jenkins入门
