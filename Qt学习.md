#  Qt学习

##  工程管理

一、创建项目

![1724764541702](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1724764541702.png)

Application：Qt的应用程序，包含Qt Quick和普通窗口程序

Library：它可以创建动态库、静态库、及Qt Creator自身插件、Qt Quick扩展插件

其它项目：创建单元测试项目、梓目录项目、Qt4设计师自定义控件

Non-Qt Project：可以创建纯C/C++的项目

Import Project：从版本控制系统来管理软件项目，导入一些我们使用过的项目



Qt应用程序拥有四个子模板：

1、Qt Widgets Application：普通窗口模板，传统基于部件的窗体应用程序
2、Qt Console Application：控制台应用程序，因为Qt主要用于图形界面设计
3、Qt Quick...



![1724765298542](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1724765298542.png)

基类的选择：

QMainWindow：基于主窗口类的应用程序，一般主要用于比较复杂的程序，除中央客户界面，还可以包括菜单栏、状态栏、工具栏及多个停靠的工具对话框等等。
QWidget：最简单最基本的窗口程序，它里面可以容纳很多个控件实现程序等功能
QDialog：基于对话框，对话框一般主要用于弹窗，也可以用于主界面显示，它是从QWidget继承过来的



![1724765888639](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1724765888639.png)

Qt各类型文件：

.pro项目描述文件
.h头文件
.cpp源程序文件
.ui界面描述文件
.pro.user用户描述文件
资源文件（音频、图片等等）



使用按钮测试QMessageBox函数

![1724842783062](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1724842783062.png)

显示如图需要进行以下步骤：先在.ui文件中将button按钮拖入ui组件中，然后右键这个按钮，选中转到槽...这个时候就会跳转到widget.cpp文件中，并且出现了一个on_pushButton_clicked()函数，在这个函数中按照如图输入就能实现这个效果，当然必不可少的是需要包括`#include "QMessageBox"`头文件。这里的QMessageBox其实就是相当于一个窗口，是通过按钮点击弹出来的窗口。对于information函数见下图
![1724844392771](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1724844392771.png)

然后就是第一个参数其实是起到一个关联作用，如果填this，那么我将wiget这个窗口关闭的话这个子的QMessageBox也会关闭





##  Qt控件介绍

![1724845110342](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1724845110342.png)

![1724845398966](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1724845398966.png)

![1724845711948](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1724845711948.png)

![1724845816208](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1724845816208.png)





##  3种技术模块---Qt_MTS_demos

- 菜单栏
- 工具栏
- 状态栏



**导入图片到项目中**

首先要准备好图片，从网上随便下载文件就行，放在你预先准备好的文件夹中，然后复制到项目主文件夹(Qt_MTS_demos)内

![1725095491830](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1725095491830.png)

在当前的主项目文件加Qt_MTS_demos右键选中add new...然后选择Qt->Qt Resource File，起个名称(只要不是中文就行)，版本控制选none

![1725095696436](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1725095696436.png)

先添加前缀然后再添加文件，再选中你全部准备好的图片添加进去即可，保存这以上步骤也很重要，在下图展示的位置点×会弹出窗口然后点击save all

![1725095907106](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1725095907106.png)



**this概念的解析**

在这个项目的实例中，遇到了一个this，这个this也是我一直学Qt困扰着我的地方，以下面为例

```cpp
//菜单栏设计与实现
QMenuBar* pMenuBar = new QMenuBar(this);
setMenuBar(pMenuBar);   //用于将 QMenuBar 设置为 QMainWindow 的菜单栏。这个函数的作用是将指定的 QMenuBar 对象作为主窗口的菜单栏，使其显示在窗口的顶部。
```

首先这个语句出现在mainwindow.cpp中，那么这里的this指的就是主窗口mainwindow实例。那么这一条语句执行后就包含了两种含义：1、创建pMenueBar对象。2、传递this作为父对象也就是mainwindow。那么这样做有什么好处呢？

- 内存管理： 通过将 `this` 传递给 `QMenuBar` 的构造函数，你指定了 `MainWindow` 作为 `QMenuBar` 的父对象。当 `MainWindow` 被销毁时，Qt 会自动销毁其子对象（包括 `QMenuBar`），这简化了内存管理。 
- 对象层级结构：Qt 的对象系统使用层级结构来组织和管理对象。通过设置父对象，你将 `QMenuBar` 作为 `MainWindow` 的子对象。这种结构有助于组织界面元素，使它们在视觉和功能上都与父窗口关联。
- 事件处理： 子对象可以继承父对象的事件处理。虽然 `QMenuBar` 不直接从 `MainWindow` 继承事件处理，但将其作为子对象可以使得 `MainWindow` 更好地管理和协调子对象的行为。 





**ui修改图标和窗口名称**

![1725102376596](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1725102376596.png)

在QWidget选项中找到windowTitle和windowIcon进行修改后效果如图

![1725102509560](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1725102509560.png)



**成果效果图**

![1725108899814](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1725108899814.png)





##  正则QRegExp技术

应用场景：在业务开发中，会碰到验证、查询、替换等等相关操作。正则表达式用描述一组字符串特性的模式，用来匹配特定的字符串。

正则表达式要素：数量限定符、位置限定符、字符类、特殊符号等



**成果展示图**

![1725180606278](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1725180606278.png)



用到的组件：

- label标签：请输入手机号码：字样就是以label为组件形成的

- Line Edit行编辑器：输入框，用来输入电话号码
- Push Button按钮：点击弹出提示框，验证输入框内的电话号码是否符合条件
- Group Box：是一个框框的形式，可以将多个控件固定在一起，保持其相对位置，注意一定要`右键选中放到后面，不然会覆盖之前的控件无法选中`





##  可视化数据技术

- QChart类（用来管理数据）
- QChartView类（用来显示图表类）



项目准备：

- 在.pro工程文件中的`QT       += core gui`下一行加上`QT += charts`
- 在.h文件中加上头文件`#include <QtCharts>`和`#include <QtCharts/QChartView>`
- 在MainDialog类中添加成员指针变量

![1725281533123](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1725281533123.png)



**出现的问题**

为什么不能将pChart放在maindialog.h中的的成员变量中声明？

解答：将 `pChart` 作为 `MainDialog` 类中的成员变量可能会导致问题，主要是因为 `pChart` 是在 `MainDialog` 构造函数中动态创建的。如果你将 `pChart` 作为成员变量，需要确保在类的析构函数中正确释放它，以避免内存泄漏。此外，确保在图表被销毁之前它的所有引用都有效也是个挑战。如果处理不当，可能会引发程序崩溃或不稳定的行为。使用动态创建的对象需要额外的内存管理和生命周期管理工作。 

![1725326146229](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1725326146229.png)

这里和视频做的稍微不一样的点就是把销售数量的标签给遮掉了，如果显示在柱状图上显得很丑



##  QML高级编程

**创建项目**

new project->Qt Quick Application-Empty...省略的步骤和之前的都一样，该选的选，不该选的不选
打开.main.qml文件，配置以下操作，如图所示：
![1725437183863](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1725437183863.png)



右键"/"然后点击add new...，选择Qt->QML File(Qt Quick2)分别创建GreenMenuBar.qml、GreenMenuBarBg.qml和GreenMenuItem.qml。然后在每一个新创建的qml文件中都要和maiin一样Import文件，具体import什么文件差不多和main文件中的一致，效果如图：

![1725438173932](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1725438173932.png)



**报错解决**

在跟着视频敲完一小段之后发现在main.qml文件中一直出现invalid name menuBar的bug，将window改成ApplicationWindow就不会报错了。 

**原因：**`ApplicationWindow` 是一个专门为 Qt Quick Controls 设计的窗口类型，它提供了一个完整的应用窗口，包括菜单栏、工具栏和状态栏等功能，而 `Window` 是更基础的窗口类型，主要用于简单的显示和布局。  代码中，`MenuBar` 和 `Menu` 是 Qt Quick Controls 的组件，它们依赖于 `ApplicationWindow` 来提供完整的功能支持。因此，当你将 `Window` 改为 `ApplicationWindow` 时，它能够正确地渲染和管理菜单栏及其组件。 



**成果展示**

![1725446392020](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1725446392020.png)

免费的课程就是粗糙，做的东西既随意又不完整，仔细一看那个菜单栏还没有对齐，看着真难受，幸好是免费的课，要是不知道花钱买课会是个咋样的结果。跟着敲了几节课的qt项目发现了一个很重要的点，就是你要熟悉这些函数调用，绝大部分的实现其实都是qt自带的函数，这一点的积累肯定是要长期才能形成的。还有就是要搞清楚控件之间的联系啊，层次关系之类的，目前学到这里的感觉就是这样了...代码详细的解释放在了注释里了~





##  多线程讲解

**1、Qt多线程的重要性**

- 提高应用程序的性能
- 优化资源利用
- 处理复杂逻辑
- 增加用户体验
- 网络通信应用
- 让软件拥有灵敏的响应
- 充分利用多核处理器
- 更加高校的通信
- 开销比进程小

**2、操作系统大致分为**

- 单进程、单进程：MS-DOS
- 多进程、单线程：Unix
- 多进程、多线程：Solaris操作系统
- 单进程、多线程：VxWorks操作系统

**3、线程是程序的最小执行单位，是操作系统分配额CPU时间的最小实体**

- 在进程内部创建、终止线程比创建、终止进程要快
- 同一个进程内的线程之间切换比进程间的切换速度快，尤其是用户级线程间的切换
- 线程对解决客户端/服务器模型非常有效
- 每个进程都具有独立的地址空间，而该进程内所有线程共享该地址空间

**4、使用多线程必须考虑如下情况**

- 某些任务耗时比较多
- 应用程序中各种任务相对独立
- 实时系统应用
- 各个任务有不同优先级；一个进程中的所有线程共享父进程的变量，但是同时每个线程都可以拥有自己的变量



##  TCP/UDP实战

TCP---任何需要可靠数据传输和连接管理(文件传输、远程登录、数据库访问)

UDP---无连接的传输协议(多播和广播、实时性、低延迟)



**TCP/UDP原理**

TCP是一种面向连接、可靠的传输层协议，提供可靠的数据传输、确保数据按顺序到达目标主机，并且具备流量控制和拥塞控制的功能。TCP协议基本原理（连接建立、可靠性保证、拥塞控制、流量控制、数据分段和重组、连接释放）

UDP是一种无连接的传输协议，提供简单、搞笑的数据传输机制，与TCP相比，UDP不保证可靠性和顺序性，单具有较低的延迟和网络开销。UDP协议基本原理（无连接性、数据报格式、不可靠性、高效性）。



---

**UDP项目实战**

项目准备工作：

创建QDialog项目-->在ui下的windowTitle修改窗口名"UDP网络服务器"-->在.pro文件中第二行加上`QT += network`->右键Headers选中add new...，创建类的时候一定要继承QObject类
![1725618947058](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1725618947058.png)

