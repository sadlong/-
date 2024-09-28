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

然后，需要在udpservercomm.h文件中申明变量如下：
![1725676726087](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1725676726087.png)



**成果展示**

![1725676514079](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1725676514079.png)

因为没有服务端程序连接上，所以什么都没有显示...





##  天气预报系统

**项目准备工作**

首先导入图片，这个方法已经在3种技术模块中提到了，就不再说了。然后就是在.pro文件中第二行加入`Qt += network`和在.h文件中加入一些头文件的声明，头文件申明如下图：


**成果展示**

![1725761197540](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1725761197540.png)



**项目总结**
半成品项目，实话说至少还是学到了一点东西的，下拉框控件：Combo Box，日历控件：Calendar Widget，空白框控件：List Widget，时间显示控件：LCD Number。然后就是项目视频中提到如何添加下拉框的元素和显示系统时间到LCD管上。巩固了添加图片的操作。



**报错解决**

error: No rule to make target '../Qt_Weather_Prs/images/?.jpg', needed by 'debug/qrc_images.cpp'.  Stop.
原因是我的图片是中文名，也不知道为什么改成数字就好使了





##  汽车仪表盘

**项目创建**

与以往创建项目不同的是，这一次要把ui那个选项取消勾选，然后选择的基类是QWidget





##  Qt5开发文字处理软件项目



##  QML

###  Window介绍

在这一节主要是介绍了Window控件的一些调用，不会的话就去帮助文档搜索Window去试试。除此之外还有一次实例应用：`焦点在哪个控件上`，这里是给出了两个button控件来通过鼠标点击和键盘按钮来改变焦点位置，同时在改变的过程中用颜色高亮和控制台输出来证实程序的正确性，完整代码如下：

```cpp
import QtQuick 2.12
import QtQuick.Window 2.12
import QtQuick.Controls 2.5

Window {
    visible: true
    width: 640
    height: 480
    title: qsTr("Hello World")

    //以屏幕左上角为(0,0),运行之后窗口就会显示在相对于源点(50, 50)的位置
    x: 600
    y: 300

    //限定窗口大小，不能被拉伸 方法就是都对应上width和height的数值一样
    minimumWidth: 640
    minimumHeight: 480
    maximumWidth: 640
    maximumHeight: 480

    //透明度范围0-1
    opacity: 0.8

    //内置信号与槽函数 这个例子是改变窗口宽度来输出当前宽度 要调用这个槽函数通常是on+空间名称然后会显示出来
//    onWidthChanged: {
//        console.log("width:", width)
//    }

    Button {
        id: btn1
        objectName: "btn1"  //控件起名字
        focus: true //默认以btn1聚焦
        width: 50
        height: 50
        background: Rectangle {
            border.color: btn1.focus ? "blue" : "black"
        }

        //鼠标点击事件
        onClicked: {
            console.log("btn1 clicked")
        }

        //点击键盘右键事件
        Keys.onRightPressed: {
            btn2.focus = true
        }
    }

    Button {
        id: btn2
        objectName: "btn2"
        x: 100
        width: 50
        height: 50
        background: Rectangle {
            border.color: btn2.focus ? "blue" : "black"
        }
        onClicked: {
            console.log("btn2 clicked")
        }
        Keys.onLeftPressed: {
            btn1.focus = true
        }
    }

    onActiveFocusItemChanged: {
        console.log("active focus item changed", activeFocusItem, "object name:", activeFocusItem.objectName)
    }
}
```





###  Item与Rectangle

**解决哪个控件在上方的问题**

```cpp
import QtQuick 2.12
import QtQuick.Window 2.12
import QtQuick.Controls 2.5

Window {
    visible: true
    width: 640
    height: 480
    title: qsTr("My QML")
    color: "white"

    Rectangle {
        x: 100
        y: 100
        z: 1    //不加这一行默认蓝色矩形会覆盖黑色矩形，z坐标默认是0
        width: 100
        height: 50
        color: "black"
    }

    Rectangle {
        x: 120
        y: 120
        width: 100
        height: 50
        color: "blue"
    }

}
```

在这段代码中如果将`z:1`注释掉会让蓝色矩形覆盖掉黑色矩形，如果想要达到黑色矩形在上方的话就需要加上那一行



**鼠标选中聚焦后接收键盘信息**

```cpp
import QtQuick 2.12
import QtQuick.Window 2.12
import QtQuick.Controls 2.5

Window {
    visible: true
    width: 640
    height: 480
    title: qsTr("My QML")
    color: "white"

    Rectangle {
        x: 100
        y: 100
        width: 100
        height: 50
        color: "black"
        focus: true	//设置默认聚焦

        MouseArea {
            anchors.fill: parent	//填充在父控件当中
            onClicked: {
                console.log("on clicked")
            }
        }

        //鼠标点击矩形框之后按下enter键就会在控制台上输出
        Keys.onReturnPressed: {
            console.log("on return pressed")
        }
    }
}
```





**anchor用法**

```cpp
import QtQuick 2.12
import QtQuick.Window 2.12
import QtQuick.Controls 2.5

Window {
    visible: true
    width: 640
    height: 480
    title: qsTr("My QML")
    color: "white"

    Rectangle {
        id: rect1
        width: 50
        height: 50
        color: "black"
        anchors.centerIn: parent    //控件居中 但是不知道为什么加了这一句另外两个控件显示就不对了
    }

    Rectangle {
        id: rect2
        width: 100
        height: 50
        anchors.left: rect1.right	//将rect2的左边接在rect1的右边
        anchors.leftMargin: 20	//设置两个控件之间的距离
        color: "black"
    }

    Rectangle {
        id: rect3
        width: 100
        height: 50
        anchors.top: rect1.bottom	//将rect2的顶边接在rect1的下面
        anchors.topMargin: 20	//设置两个控件之间的距离
        color: "black"
    }
}
```

显示效果如下：
![1726657285613](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1726657285613.png)



**scale和rotation**

- `scale: num`用来放缩控件，num是多少就放大多少倍
- `rotation: num`用来旋转控件，num是多少就顺时针旋转多少度

```cpp
import QtQuick 2.12
import QtQuick.Window 2.12
import QtQuick.Controls 2.5

Window {
    visible: true
    width: 640
    height: 480
    title: qsTr("My QML")
    color: "white"

    Rectangle {
        width: 100
        height: 50
        color: "black"
        border.width: 2 //边框粗细调节 越大越粗
        border.color: "green"  //边框颜色
        anchors.centerIn: parent    //将控件居中 以父控件为中心
        rotation: 30    //顺时针旋转30度
        scale: 2    //放缩控件，数字是多少就方法多少倍
        radius: 15  //调整圆角幅度 数值越大幅度越大
    }


    //渐变色gradient样例
    Rectangle {
        y: 100; width: 80; height: 80
        gradient: Gradient {
            GradientStop { position: 0.0; color: "lightsteelblue" }
            GradientStop { position: 1.0; color: "blue" }
        }
    }
}
```





###  自定义边框Rectangle

右键`/`文件选中add new...--->选中Qt(QML File)--->取名MyRectangle(取名随意)



**源码**

MyRectangle.qml

```cpp
import QtQuick 2.0

//实际上实现的是Rectangle内置的border.width,可以自定义长度边界
Rectangle {
    id: borderRect

    //将属性暴露出去 以便更好的灵活改变边距大小
    property int myTopMargin: 0
    property int myBottomMargin: 0
    property int myLeftMargin: 0
    property int myRightMargin: 0
    color: "red"    //边框颜色为红色
    Rectangle {
        id: innerRect
        color: "yellow" //实际内部的矩形为黄色
        anchors.fill: parent    //填充父控件borderRect可用的空间

        //设置边距
        anchors.topMargin: myTopMargin
        anchors.bottomMargin: myBottomMargin
        anchors.leftMargin: myLeftMargin
        anchors.rightMargin: myRightMargin
    }
}
```



main.qml

```cpp
import QtQuick 2.12
import QtQuick.Window 2.12
import QtQuick.Controls 2.5

Window {
    visible: true
    width: 640
    height: 480
    title: qsTr("Hello World")

    //调用自定义矩形
    MyRectangle {
        //显示的起始位置
        x: 100
        y: 50

        //设置长宽
        width: 200
        height: 100

        //设置边缘宽度
        myTopMargin: 5
        myBottomMargin: 5
        myLeftMargin: 10
    }
}
```



**效果图**

![1726731606227](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1726731606227.png)

**小结**

这个demo主要是实现了上一节课讲的border.width，由于border.width修改的是整个边界，而不能仅仅修改某一边，通过这个实例很好的展现了将不同边设置不同边距，或者不设置的案例。除此之外这里还涉及到工程中的灵活性，就是将属性暴露出去，这样就能灵活的设置边距了。





###  state与transitions动画效果制作

帮助文档来源：Animation and Transitions in Qt Quick

**state状态机**

```cpp
import QtQuick 2.12
import QtQuick.Window 2.12

Window {
    visible: true
    width: 640
    height: 480
    title: qsTr("Hello World")

    //本段代码从Item中states中复制过来的样例
    Rectangle {
        id: root
        width: 100; height: 100
        state: "normal" //样例中没有的 需要自己手动添加

        //各种状态 在状态中进行属性修改 将所有修改都封装在state中
        states: [
            State {
                name: "normal"
                PropertyChanges { target: root; color: "black"}
            },
            State {
                name: "red_color"
                PropertyChanges { target: root; color: "red"; width: 200}
            },
            State {
                name: "blue_color"
                PropertyChanges { target: root; color: "blue"; height: 200}
            }
        ]

        //添加鼠标操作
        MouseArea {
            anchors.fill: parent

            //默认显示黑色
            //按下鼠标不放显示红色
            onPressed: {
                root.state = "red_color"
            }

            //松开鼠标显示蓝色
            onReleased: {
                root.state = "blue_color"
            }
        }
    }
}
```



**小结**

这一小段demo其实有一点动画的感觉了，运行时显示黑色，点击显示红色，松开显示蓝色。这一小段demo学到的点还挺多，首先是代码规范，将所有状态封装到state中，当事件发生的时候直接改变`root.state`的状态即可





**直接属性动画(Direct Property Animation)**

```cpp
import QtQuick 2.12
import QtQuick.Window 2.12

Window {
    visible: true
    width: 640
    height: 480
    title: qsTr("Hello World")

    //本段代码从Animation and Transitions in Qt Quick复制过来
    Rectangle {
        id: flashingblob
        width: 75; height: 75
        color: "blue"
        opacity: 1.0

        //鼠标点击 动画开启
        MouseArea {
            //使鼠标区域填满整个矩形
            anchors.fill: parent
            
            //当鼠标点击时 启动三个动画
            onClicked: {
                animateColor.start()
                animateOpacity.start()
                animateWidth.start()
            }
        }

        //此动画将 flashingblob 的颜色从蓝色变为绿色，持续时间为1秒
        PropertyAnimation {
            id: animateColor
            target: flashingblob
            properties: "color"	//属性名称
            to: "green"
            duration: 1000  //持续时间1s
        }

        //此动画将透明度从0.1（半透明）变为1.0（不透明），持续时间为2秒
        NumberAnimation {
            id: animateOpacity
            target: flashingblob
            properties: "opacity"
            from: 0.1
            to: 1.0
            duration: 2000  //持续时间2s
            //loops: Animation.Infinite //意思是该动画将无限次重复播放，直到被手动停止或界面关闭
       }

        //此动画将矩形的宽度从75增加到150，持续时间为2秒
        NumberAnimation {
            id: animateWidth
            target: flashingblob
            properties: "width"
            from: 75
            to: 150
            duration: 2000  //持续时间2s
            //loops: Animation.Infinite
       }
    }
}
```

这个demo主要是记住它的用法吧，要是要用到的话就直接去对应模块的帮助文档找例子，然后复制过来再根据自己的需求去改



**使用预定义的目标和属性(Using Predefined Targets and Properties)**

```cpp
import QtQuick 2.12
import QtQuick.Window 2.12

Window {
    visible: true
    width: 640
    height: 480
    title: qsTr("Hello World")

    //从Using Predefined Targets and Properties复制而来
    Rectangle {
        id: rect
        width: 100; height: 100
        color: "red"

        //模板就是 PropertyAnimation on 属性 {...}
        //变x和y坐标
        PropertyAnimation on x {
            to: 100
            duration: 2000
        }
        PropertyAnimation on y {
            to: 100
            duration: 2000
        }
        
        //变宽度和颜色 都是2秒完成
        PropertyAnimation on width {
            to: 300
            duration: 2000
        }
        PropertyAnimation on color {
            to: "yellow"
            duration: 2000
        }
        
        //按顺序变颜色的写法
//        SequentialAnimation on color {
//            ColorAnimation { to: "yellow"; duration: 1000 }
//            ColorAnimation { to: "blue"; duration: 1000 }
//        }
    }
}
```

模板大概就是` PropertyAnimation on 属性 {...}`



**state和transition结合实现点击高亮**

```cpp
import QtQuick 2.12
import QtQuick.Window 2.12

Window {
    visible: true
    width: 640
    height: 480
    title: qsTr("Hello World")

    //复制自Transitions During State Changes
    Rectangle {
        width: 75; height: 75
        id: button
        state: "RELEASED"

        MouseArea {
            anchors.fill: parent
            onPressed: button.state = "PRESSED"
            onReleased: button.state = "RELEASED"
        }

        states: [
            State {
                name: "PRESSED"
                PropertyChanges { target: button; color: "lightblue"}
            },
            State {
                name: "RELEASED"
                PropertyChanges { target: button; color: "lightsteelblue"}
            }
        ]

        //如果duration时间很短的话不加这一段其实是一样的效果 加上这一段并且长一点的duration就是多了点击有颜色渐变的过程
        transitions: [
            Transition {
                from: "PRESSED"
                to: "RELEASED"
                ColorAnimation { target: button; duration: 100}
            },
            Transition {
                from: "RELEASED"
                to: "PRESSED"
                ColorAnimation { target: button; duration: 100}
            }
        ]
    }
}
```

这个就用来当作点击高亮的模板吧！



**弹出文本动画效果**

```cpp
import QtQuick 2.12
import QtQuick.Window 2.12

Window {
    visible: true
    width: 640
    height: 480
    title: qsTr("Hello World")

    Rectangle {
        id: banner
        width: 150; height: 100; border.color: "black"

        Column {
            anchors.centerIn: parent
            Text {
                id: code
                text: "lzl好帅"
                opacity: 0.01
            }
            Text {
                id: create
                text: "lzl超级帅"
                opacity: 0.01
            }
            Text {
                id: deploy
                text: "lzl真的超级帅"
                opacity: 0.01
            }
        }

        MouseArea {
            anchors.fill: parent
            onPressed: playbanner.start()
        }

        SequentialAnimation {
            id: playbanner
            running: false
            NumberAnimation { target: code; property: "opacity"; to: 1.0; duration: 200}
            NumberAnimation { target: create; property: "opacity"; to: 1.0; duration: 200}
            NumberAnimation { target: deploy; property: "opacity"; to: 1.0; duration: 200}
        }
    }
}
```



**总结**

个人觉得`点击高亮`和`弹出文本`是最重要的，这两个完全可以做成模板！



###  Component与Loader

**动态创建并销毁组件、加载动图**

```cpp
import QtQuick 2.12
import QtQuick.Window 2.12
import QtQuick.Controls 2.5

Window {
    visible: true
    width: 640
    height: 480
    title: qsTr("Hello World")



//    Component {
//        id:com
//        Rectangle {
//            id: rect
//            width: 200
//            height: 100
//            color: "black"
//            //调用component属性的内置槽函数   调用component后自动调用
//            Component.onCompleted: {
//                console.log("onCompleted", width, height, color)
//            }

//            //关闭component后自动调用
//            Component.onDestruction: {
//                console.log("onDestruction", width, height, color)
//            }
//        }
//    }

    Component {
        id: com
        //加载动图 AnimatedImage继承自Image
        AnimatedImage {
            id: img
            source: "qrc:/test.gif"
            width: 200
            height: 200
            speed: 10    //改变动图倍速
        }

    }

    Loader {
        id: loader
        //source: "MyRectangle.qml" //实现不了 不知道为啥
        asynchronous: true  //设置为异步
        sourceComponent: com
        onStateChanged: {
            console.log("status: ", status)
        }
    }

    Button {
        width: 50
        height: 50
        x: 200
        onClicked: {
            //loader.sourceComponent = null   //点击消除component

            //点击后暂停，再次点击继续动
            loader.item.paused = !loader.item.paused

            //点击后更改控件大小 只能这么改
//            loader.item.width = 100
//            loader.item.height = 100
//            loader.item.color = "red"

            //错误示范
            //com.width = 50
        }
    }
}

```

不知道为啥Loader里面不会输出status，其它效果不错~



###  MouseArea

```cpp
import QtQuick 2.12
import QtQuick.Window 2.12

Window {
    visible: true
    width: 640
    height: 480
    title: qsTr("Hello World")

    MouseArea {
        id: mouseArea
        width: 200
        height: 200
        acceptedButtons: Qt.LeftButton | Qt.RightButton //让鼠标左右键都能触发
        Rectangle {
            anchors.fill: parent
            color: "black"
        }

        //点击事件
        onClicked: {
            console.log("clicked")
        }
//        //按下事件
//        onPressed: {
//            //验证按下是哪个键只能在onPressed中判断而不是onClicked中判断
//            var ret1 = pressedButtons & Qt.LeftButton
//            var ret2 = pressedButtons & Qt.RightButton
//            console.log(ret1 ? "left" : ret2 ? "right" : "other")   //三目运算符嵌套
//            console.log("pressed")
//        }
//        //松开事件
//        onReleased: {
//            console.log("release")
//        }
    }
}
```

点击事件的各种操作，详见帮助文档MouseArea



###  Button

需要导入：`import QtQuick.Controls 2.5 `

其实总的来说，Button其实就是Rectangle+MouseArea



**多个button保证只有一个button选中**

```json
//多个按钮 确保只有一个按钮是被选中的 在每个button中加上autoExclusive: true
Button {
    id: btn1
    width: 50
    height: 50
    autoExclusive: true
    checkable: true
}

Button {
    id: btn2
    width: 50
    height: 50
    x: 60
    autoExclusive: true
    checkable: true
}

Button {
    id: btn3
    width: 50
    height: 50
    x: 120
    autoExclusive: true
    checkable: true
}
```





##  feiyangqingyun的demo学习

###  电池控件

**层次分析**

首先说frmbattery.cpp，这个是基于QWidget的一个继承类，也就是最开始创建项目的时候起的名字，然后创建完工程之后batter.cpp是之后创建的，在frmbattery的ui中放着两个对象：横向拖拉条(horizontalSlider)和电池图像

####  反锯齿函数

```cpp
QPainter painter(this);
painter.setRenderHints(QPainter::Antialiasing | QPainter::TextAntialiasing);
```

在这个电池控件中，由于这个图像是弯曲的，所以要用到反锯齿函数来美化图形，调用了反锯齿函数之后那些有弧线的地方会变得圆滑



####  固定矩形位置

```cpp
QPointF batteryRect;	//先声明对象
int borderWidth = 5;
QPointF topLeft(borderWidth, borderWidth);  //确定左上角
QPointF bottomRight(batteryWidth, height() - borderWidth);  //确定右上角
batteryRect = QRectF(topLeft, bottomRight);
```

这是一段关于`QPointF`api的使用方法，这一段的作用是将矩形固定在一个位置





####  渐变色调用方法

```cpp
QLinearGradient batteryGradient(QPointF(0, 0), QPointF(0, height()));   //纵向的渐变色
if (currentValue <= alarmValue) {
    batteryGradient.setColorAt(0.0, alarmColorStart);   //第一个参数是position，范围是[0,1]
    batteryGradient.setColorAt(1.0, alarmColorEnd);
} else {
    batteryGradient.setColorAt(0.0, normalColorStart);
    batteryGradient.setColorAt(1.0, normalColorEnd);
}
painter->setBrush(batteryGradient); //用渐变色填充
```

对于这个电池组件，他会有一个电量低的警戒状态（也就是红色），所以才会有中间的if和else部分，要是仅仅只有一类颜色的渐变的话就只需要其中的两行即可，第一个参数是`double`类型，第二个参数是`QColor`类型





####  QPainter的基本使用步骤

```cpp
painter->save();

//固定位置
QPointF headRectTopLeft(batteryRect.topRight().x(), height() / 3);
QPointF headRectBottomRight(width(), height() - height() / 3);
QRectF headRect(headRectTopLeft, headRectBottomRight);

//设置渐变色 可有可无
QLinearGradient headRectGradient(headRect.topLeft(), headRect.bottomLeft());
headRectGradient.setColorAt(0.0, borderColorStart);
headRectGradient.setColorAt(1.0, borderColorEnd);

painter->setPen(Qt::NoPen);	//笔用来画边界
painter->setBrush(headRectGradient);	//刷子用来填充颜色
painter->drawRoundedRect(headRect, headRadius, headRadius);

painter->restore();
```





####  复现过程中遇到的问题

**构造函数前加explicit关键字**

```cpp
explicit frmBattery(QWidget *parent = nullptr);
```

在初始qt构建项目的时候是不会有explicit关键字的，explicit关键字的作用就是防止隐式转换，只有明确的构造函数才能调用



**painter相关**

```cpp
//setpen()里面参数是QPen类型的，QPen类型中需要两个参数，分别是QColor和画笔粗细
painter->setPen(QPen(borderColorStart, borderWidth));

//画刷 填充颜色
painter->setBrush(Qt::NoBrush);

//用来定形 绘制带圆角的函数 参数1：QRectF类型用来确定位置，后两个参数分别是x和y的圆角幅度
painter->drawRoundedRect(batteryRect, borderRadius, borderRadius);
```



**自定义控件封装**

这个很重要很重要！！！也是找了好久猜搞明白这个操作怎么弄的。就拿这个battery类为例，当我写完画边框的函数之后，想要跑一下看看能不能有个画边框的样子，结果什么都没有显示！？拿自己代码和它对比了一下发现自己的.ui文件中没有battery类？？？这玩意咋出来的呢？

首先这个battery是一个QWidget类，然后打开.ui文件，在Containers中选中Widget拖出来，然后右键这个框框选中提升为，这时候会弹出一个对话框，然后将你的自定义控件的类名复制过来添加即可，最保险的操作就是将类名直接复制过来，可能有时候因为大小写不同而出错！
![1727269504178](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1727269504178.png)



**Q_EMIT+函数**

代表Qt信号发射函数，以`Q_EMIT valuechanged(value);`为例，当value发生变化 连接到`valuechanged(value)`信号的槽函数都会被调用，前提是这个`valuechanged(value)`是一个槽函数哦！



**画完了电池电量为什么不显示？**

破案了，原来是frmbattery.cpp中的initForm函数没写。。。



**如何通过滑动轴控件来实现电池电量变化的？**

这个要看到frmbattery.cpp中的initForm函数，复现的时候就是没有写这个函数导致没有出现电量。。。也就是这一步实现了轴移动电量也跟着移动的效果



**小结 **

大佬写出来的代码就是不一样，其实看到现在感觉是懂了绝大部分了，主要是想独立复现出来还是有点困难，还是难在电量的显示上。第一遍看源码的时候还是没有理解透，现在再看一遍这个代码又懂了很多东西。首先需要弄懂的是他在Q_OBJECT中写的一大堆宏定义，这其实是Qt的一种特色吧，`可以通过 Qt 的元对象系统（如信号与槽机制）方便地访问和修改这些属性`。通过这一个小demo其实学到的东西还挺多！首先是代码的规范吧，有一说一确实舒服，虽然从这里调用到那里，函数名一样但参数不一样，但是我认为这样写反而十分严谨，映像比较清楚的是这里面的几个value，他为了从int统一到double写了很多对同名函数





###  高亮按钮---lightButton

####  main.cpp大致模板(4.10版本)

```cpp
#include "frmlightbutton.h"

#include <QApplication>
#include <QTextCodec>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    QFont font;
    font.setFamily("Microsoft Yahei");
    font.setPixelSize(13);
    a.setFont(font);

    QTextCodec* codec = QTextCodec::codecForName("utf-8");
    QTextCodec::setCodecForLocale(codec);

    frmLightButton w;
    w.setWindowTitle("lightButtonDemo");
    w.show();
    return a.exec();
}
```



####  求min函数

```cpp
int side = qMin(width, height);
```



####  在控件中央显示文本

```cpp
QFont font;
font.setPixelSize(side - 200);
painter.setFont(font);	//将刚刚创建并设置好的字体应用到绘图对象 (painter) 上
painter.setPen(textColor);	//设置笔刷的颜色 这决定了文本的颜色
//this->rect()是widget内置的表示当前绘图区域 Qt::AlignCenter表示文本居中对齐
painter.drawText(this->rect(), Qt::AlignCenter, text);
```



####  不显示控件的原因

1、可能是frmxxx.cpp中的构造函数中没有调用`this->initForm();`

2、evenFliter没有写。。。这个问题出现在写lightButton项目的时候出现的

通过这两次的demo学习我发现了第二点的根本原因，就是一定要注意类中的signals所绑定的信号函数，当这个被调用之后才会触发这个控件的绘制，例如lightButton中的clicked()和battery中的valueChanged()



####  自定义事件过滤器

第一次遇见，记下来吧~注释都在代码上了，其实也不是很懂。。。

```cpp
//这个函数必须写 不写不显示控件 实现一个可拖动的按钮 watched 是被监视的对象，event 是接收到的事件
bool LightButton::eventFilter(QObject *watched, QEvent *event) {
    int type = event->type();   //获取事件的类型，并将其存储在 type 变量中
    QMouseEvent* mouseEvent = (QMouseEvent*) event;
    //检查事件类型是否为鼠标按下（MouseButtonPress）
    if(type == QEvent::MouseButtonPress) {
        //检查鼠标点击的位置是否在按钮的矩形区域内 判断鼠标是否是左键点击
        if(this->rect().contains(mouseEvent->pos()) && (mouseEvent->button() == Qt::LeftButton)) {
            lastPoint = mouseEvent->pos();
            pressed = true;
        }
    } else if(type == QEvent::MouseMove && pressed) { //检查事件类型是否为鼠标移动（MouseMove），并且按钮当前是被按下状态（pressed）
        //如果允许移动（canMove 为 true），计算鼠标当前位置与上一次记录位置的偏移量 dx 和 dy
        if(canMove) {
            int dx = mouseEvent->pos().x()-lastPoint.x();
            int dy = mouseEvent->pos().y()-lastPoint.y();
            //使用 this->move() 方法，将按钮移动到新的位置，实现拖动效果
            this->move(this->x()+dx, this->y()+dy);
        }
    } else if(type == QEvent::MouseButtonRelease && pressed) {//检查事件类型是否为鼠标释放（MouseButtonRelease），并且按钮当前是被按下状态
        pressed = false;
        //触发 clicked() 信号，表示按钮被点击完成，可以连接到其他槽函数进行处理
        Q_EMIT clicked();
    }

    //调用基类的 eventFilter 方法以确保其他事件仍然得到处理，返回该值以指示事件是否被处理
    return QWidget::eventFilter(watched, event);
}
```





####  画圆形案例

```cpp
void LightButton::drawBorderOut(QPainter *painter) {
    int radius = 100;   //设置半径
    painter->save();
    painter->setPen(Qt::NoPen);
    //创建一个线性渐变对象 borderGradient，其起始点为 (0, -radius)，终止点为 (0, radius)。这意味着渐变将沿着 Y 轴垂直方向进行
    QLinearGradient borderGradient(0, -radius, 0, radius);
    //在渐变的起始位置（Y=−radius）设置开始颜色
    borderGradient.setColorAt(0, borderOutColorStart);
    //在渐变的结束位置（Y=radius）设置结束颜色
    borderGradient.setColorAt(1, borderOutColorEnd);
    painter->setBrush(borderGradient);
    //使用 drawEllipse 方法绘制一个圆形。圆心在 (0, 0)，宽和高均为 radius * 2（即直径为 200），因此绘制的圆形的边界从 (-radius, -radius) 开始，覆盖到 (radius, radius)
    painter->drawEllipse(-radius, -radius, radius*2, radius*2); //画圆形
    painter->restore();
}
```

我就说为什么分为了外圆和内圆，原来画完之后的效果图是这样啊！

![1727523410422](C:\Users\123\AppData\Roaming\Typora\typora-user-images\1727523410422.png)

