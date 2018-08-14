**ubuntu安装qt4**

<http://www.linuxidc.com/Linux/2012-05/60770.htm>

<http://blog.csdn.net/xsl1990/article/details/8299756>



快速入门系列教程:

<http://bbs.qter.org/forum.php?mod=viewthread&tid=193>

Qt帮助文档中文翻译：

<http://www.kuqin.com/qtdocument/index.html>





#####手工生成执行文件

1. **qmake -project**   生成一个和平台无关的项目文件hello.pro 

2. **qmake hello.pro**    生成一个和平台有关的文件的Makefile 

3. 键入**make** 运行Makefile

4. 生成执行文件hello 

6. ./hello 运行执行文件 



#####Qt参考文档：

<http://www.kuqin.com/qtdocument/index.html>

<http://www.kuqin.com/qtdocument/tutorial.html>



##### 将信号和特定事件连接起来,如： 

```

int main(int argc,char *argv[]) 
{ 
    QApplication app(argc,argv); 
    QPushButton *button = new QPushButton("Quit"); 
     QObject::connect(button,SIGNAL(clicked()), &app,SLOT(quit()));
    button->show(); 

    return app.exec(); 
} 

```

##### 布局管理器就是一个能够对其所负责的窗口部件的尺寸大小和位置进行设置的对象。有三个主要的布局管理器类： 

1. QHBoxLayout:在水平方向排列窗口部件 

2. QVBoxLayout:在竖直方向排列窗口部件 

3. QGridLayout:排列在一个网格里 



`QWidget::setLayout()`函数用来安装布局管理器。 



一般先声明所需的窗口部件，然后设置他们的属性，并把他们添加到布局中，布局会自动设置他们的位置和大小，再利用信号和槽机理，通过窗口部件之间的连接就可以管理用户的交互行为。



#####对于定义了信号和槽的类，在类的开始处必需插入`Q_OBJECT`宏。 



Qt由数个模块构成，每个模块都有自己的类库。最为重要的模块有**QtCord,QtGui,QtNetwork,QtOpenGL,QtScript,QtSql,QtSvg,QtXml**。 



`try()`函数用于把字符串翻译成其他语言的标记。**在用户可见的字符串周围使用try()函数是一个好习惯**。 

```
QVBoxLayout *leftLayout = new QVBoxLayout; 

leftLayout->addStretch();//添加“伸展器”，占用下面余下的空白区域，这样可以确保窗口部件占用他们所在布局的上部空间。 

```



`QWidget::sizeHint()`可以返回一个窗口部件所“理想”的尺寸大小。 


#####窗口部件固定大小： 

`setFixedSize(sizeHint().width(),sizeHint().height())； `

#####窗口部件名称： 

`setWindowTitle(tr("xxxx")); `

#####使用宏 emit发射信号，如： 
`emit findNext(text,cs);//发射信号findNext `



**一个信号可以连接多个槽。在发射这个信号时，会以不确定的顺序一个接一们的调用这些槽。 **

**多个信号可以连接一个槽。无论发射的是哪一个信号，都会调用这个槽。 **

**一个信号可以与另一个信号连接。**

**可以用`disconnect`来移除连接。 **



**要把信号成功连接到槽，它们的参数必须具有相同的顺序和相同的类型。 **
**但如果信号的参数比它所连接的槽多，那么多余的参数会被简单的忽略掉。 **

**信号和槽可用于任何QObject子类。**



setupUi自动将那些符合**on_objectName_signalName()**命名惯例的任意槽与相应的**objectName_signalName**信号连接到一起. 
如：如果定义了槽`on_lineEdit_textChanged()`，那么lineEdit的信号**textChanged将会**和**on_lineEdit_textChanged**连接起来



qt有三个内置检验器类:**QIntValidator,QDoubleValidator,QRegExpValidator. **

**正则表达式QRegExp**

<http://blog.csdn.net/wang_xuehen/article/details/7459567>

<http://www.cnblogs.com/frankbadpot/archive/2009/10/18/1583617.html>

常用正则表达式:

```

^\d+$　　//匹配非负整数（正整数 + 0）
^[0-9]*[1-9][0-9]*$　　//匹配正整数
^((-\d+)|(0+))$　　//匹配非正整数（负整数 + 0）
^-[0-9]*[1-9][0-9]*$　　//匹配负整数
^-?\d+$　　　　//匹配整数
^\d+(\.\d+)?$　　//匹配非负浮点数（正浮点数 + 0）
^(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*))$　　//匹配正浮点数
^((-\d+(\.\d+)?)|(0+(\.0+)?))$　　//匹配非正浮点数（负浮点数 + 0）
^(-(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*)))$　　//匹配负浮点数
^(-?\d+)(\.\d+)?$　　//匹配浮点数
^[A-Za-z]+$　　//匹配由26个英文字母组成的字符串
^[A-Z]+$　　//匹配由26个英文字母的大写组成的字符串
^[a-z]+$　　//匹配由26个英文字母的小写组成的字符串
^[A-Za-z0-9]+$　　//匹配由数字和26个英文字母组成的字符串
^\w+$　　//匹配由数字、26个英文字母或者下划线组成的字符串
^[\w-]+(\.[\w-]+)*@[\w-]+(\.[\w-]+)+$　　　　//匹配email地址           

```





**QDialog的返回值：QDialog::Acceped，QDialog::Rejected。分别通过调用QDialog的槽accept()和reject()可让返回前面的值。**



动态对话框：P49 



**使用QUiLoader类载入.ui文件; **

**使用QObject::findChild<T>来访问各个子窗口部件。 **

**在.pro文件里加入：CONFIG += uitools **


`closeEvent`是QWidget的虚函数，当**关闭窗口时**这个函数被调用。 



CMainWindow的`menuBar()`为主菜单，使用`addMenu`就可以添加菜单了。 



#####任何QT窗口都有个QActions列表，向这个列表里添加Action就可提供一个上下文菜单（右键弹出菜单）： 

```
    spreadsheet->addAction(cutAction); 
    spreadsheet->addAction(copyAction); 
    spreadsheet->addAction(pasteAction); 

    spreadsheet->setContextMenuPolicy(Qt::ActionsContextMenu); 
```

也可以重新实现`QWidget::contextMenuEvent()`函数，创建一个QMenu窗口部件，在其中添加动作，然后调用`exec()`. 



`QMainWindow::statusBar()`  状态栏. 



`QMainWindows::addToolBar()`添加工具栏 

```

fileToolBar = addToolBar(tr("&File")); 
fileToolBar->addAction(newAction); 
fileToolBar->addAction(openAction); 
fileToolBar->addAction(saveAction);

```

**整形转字符串：**`QString::number(xx) `



**对话框： **

`QMessageBox::warning(...); `



**当最后一个窗口关闭后，应用程序就结束了。**如果需要，可以将QApplication的**quitOnLastWindowClosed**设置为false，可以禁止应用程序结束，此时需要调用`QApplication::quit()`函数来结束应用程序。 



**字符串赋值： 

`try("%1-%2").arg(val1).arg(val2) `



每个QWidget都有**windowModified**属性。 



`qobject_cast<T>`函数可在Qt的moc所生成的信息基础上执行动态类型强制转换，他返回一个指向所需QObject子类的指针，或者是**在该对象不能被转换成所需的类型时返回0**.



手工设置中文标题，并且不会乱码：

```

#include <QTextCodec> 

...... 

QTextCodec::setCodecForTr(QTextCodec::codecForLocale()); 

...... 

ui->pushButton->setText(tr("新窗口")); 



动态添加菜单：
     QAction *actOpen = new QAction(tr("打开(&O)"),this); 
    QIcon icon(":/images/Open.ico"); 
    actOpen->setIcon(icon); 
    actOpen->setShortcut(QKeySequence("Ctrl+O")); 

    ui->menu_F->addAction(actOpen); 

```



Qt 提供了四个类来处理图像数据：**QImage、QPixmap、QBitmap和QPicture**，它们也都是常用的绘图设备。其中QImage主要用来进 行I/O处理，它对I/O处理操作进行了优化，而且也可以用来直接访问和操作像素；QPixmap主要用来在屏幕上显示图像，它对在屏幕上显示图像进行了 优化；QBitmap是QPixmap的子类，它是一个便捷类，用来处理颜色深度为1的图像，即只能显示黑白两种颜色；QPicture用来记录并重演 QPainter命令。



对于图形项的移动，我们有很多办法实现，也可以在很多层面上对其进行控制，比如说在View上控制或者在Scene上控制。但是对于大量的不同类型的图形项，怎样能一起控制呢？在图形视图框架中提供了`advance()`槽函数，这个函数在QGraphicsScene和QGraphicsItem中都有，在图形项类中它的原型是 advance(int phase)。它的实现流程是，我们利用QGraphicsScene类的对象调用QGraphicsScene的advance()函数，这时就会执行两次该场景中所有图形项的advance(int phase)函数，第一次phase为0，告诉所有图形项即将要移动；第二次phase的值为1，这时执行移动。



#####绘图相关类：

* 场景(QGraphicsScene)：
QGraphicsScene提供了图形视图框架的场景，它有以下功能： 
1. 提供了一个管理大量图形项的快速接口 
2. 向每个图形项传播事件 
3. 管理图形项的状态，比如选择和焦点处理 

4. 提供无转换的渲染功能，主要用于打印 

**一个场景分为三个层：图形项层（ItemLayer）、前景层（ForegroundLayer）和背景层（BackgroundLayer）**。场景的绘制总是从背景层开始，然后是图形项层，最后是前景层。

* 项： 



* 视图： 

QGraphicsView 提供了视图窗口部件，它使场景的内容可视化。你可以给一个场景关联多个视图，从而给一个数据集提供多个视口。视图部件是一个滚动区域，就是说，它可以提供 一个滚动条来显示大型的场景。如果要使用OpenGL，你可以使用`QGraphicsView：：setViewport()`函数来添加 QGLWidget 

**在图形视图框架中，鼠标键盘等事件是从视图进入的，视图将它们传递给场景，场景再将事件传递给该点的图形项，如果该点有多个图形项，那么就传给最上面的图形项**

如果场景的背景需要大量耗时的渲染，可以利用**CacheBackground**来缓存背景，当下次需要渲染背景时，可以快速进行渲染。它的原理就是，把整个视口先绘制到一个pixmap上。但是这个只适合较小的视口，也就是说，**如果视图窗口很大，而且有滚动条，那么就不再适合缓存背景**。我们可以使用`setCacheMode(QGraphicsView::CacheBackground);`来设置背景缓存。默认设置是没有缓存`QGraphicsView::CacheNon `


**Qt控制台工程不能调试问题：**

<http://blog.chinaunix.net/uid-26019596-id-3479941.html>



#####MySql: 

<http://www.yesky.com/187/1754687.shtml>

**默认用户名为root，这个root和Linux的root无关 **

**修改密码： **

mysqladmin -u用户名 -p旧密码 password 新密码 

**登陆: **

mysql -u 用户名 -p ，然后输入密码 

**启动： **

`/etc/init.d/mysql start `

**停止: **
`/usr/bin/mysqladmin -u root -p shutdown `

**自动启动 **
1. 察看mysql是否在自动启动列表中 
`[root@test1 local]#　/sbin/chkconfig –list `
2. 把MySQL添加到你系统的启动服务组里面去 
`[root@test1 local]#　/sbin/chkconfig　– add　mysql `
3. 把MySQL从启动服务组里面删除。 
`[root@test1 local]#　/sbin/chkconfig　– del　mysql `



**ubuntu linux 下使用Qt连接MySQL数据库：**

<http://www.cnblogs.com/qianyuming/archive/2011/08/13/2137402.html>



**安装Qt的MySql驱动:
`sudo apt-get install libqt4-sql-mysql `
其他驱动类似 



**为MySql添加用户：**

`http://www.linuxidc.com/Linux/2008-01/10699.htm`

如：grant all privileges on *.* to xp@localhost identified by '123'; 



**MySql常用命令:**

`http://www.jb51.net/os/Ubuntu/38725.html `



**在linux下使用sqlite：**

<http://www.cnblogs.com/gzggyy/archive/2012/07/19/2599645.html>



**内存数据库：**内存数据库在程序结束后就会销毁 

```

//添加数据库驱动 
    QSqlDatabase db = QSqlDatabase::addDatabase("QSQLITE"); 
//数据库连接命名 

    db.setDatabaseName(":memory:"); 

```

需要特别注意，刚执行完query.exec("select *from student");这行代码时，** query是指向结果集以外的**，我们可以利用`query.next()`使得 query指向结果集的第一条记录。当然我们也可以利用`seek(0)`函数或者`first()`函数使query指向结果集的第一条记录。但是为了**节省内存开销**，推荐的方法是，在`query.exec("select * from student");`这行代码前加上` query.setForwardOnly(true);`这条代码，此后只能使用next()和seek()函数,也就是说只能向前读数据。 



利用 `QVariant(QVariant::String)`来输入**空值NULL **



**linux项目转到windows:**

1. moc_xxx.cpp文件保留在linux下编译好的。 

2. 除了moc_xxx.cpp外，其他的.h,.cpp文件全部转为unicode编码，方法如下： 

使用VS2010打开文件，然后文件->高级保存选项->编码选Unicode-代码页 1200->确定->保存文件 

3. 在xxx.cpp添加#include "moc_xxx.cpp " 



**发送信号:**

emit 信号xxx(参数1，参数2......)



**用户不能调整大小，布局在隐藏或显示窗口时自动调整大小**

`layout()->setSizeConstraint(QLayout::SetFixedSize);`



**强制类型转换：**

`QWidget *w = qobject_cast<QWidget *>(child);`



**遍历控件并找到所有类型为QPushButton的控件：**

```
void MainWindow::getChilds(const QObjectList &list) 

{ 
    foreach(QObject *child,list) 
    { 
        if(!child->children().empty()) 
        { 
            getChilds(child->children()); 
        } 
        else 
        { 
            QString name1 = child->metaObject()->className(); 
            QString name2 = QPushButton::staticMetaObject.className(); 
            if(child->metaObject()->className() == QPushButton::staticMetaObject.className()) 
            { 
                QPushButton *btn = qobject_cast<QPushButton *>(child); 
                if (btn) 
                    qDebug() << tr("%1: %2").arg(btn->objectName()).arg(btn->text()); 
            } 
//            qDebug() << child->objectName(); 
        } 
    } 
}

```



**处于其他窗口之上，并处于激活状态：**

```
findDialog->raise(); 
findDialog->activateWindow();

```



**关闭时删除 **

```

setAttribute(Qt::WA_DeleteOnClose); 

```



**设置光标（整个应用程序）： **

```

QApplication::setOverrideCursor(Qt::WaitCursor); 

...... 

QApplication::restoreOverrideCursor();//恢复

```

某个Widget： 

```

setCursor(Qt::CrossCursor); 
...... 

unsetCursor(); 

```





#####容器类：

1. `QVector<T>`:把项存储到内存中相邻的位置。在末尾添加额外的项非常快，而在向量前面或中间插入项则是比较耗时的(数组类似？)

2. `QLinkedList<T>`：把项存储到内 存中不相邻的位置。不支持快速的随机访问，但提供了“常量时间”的插入和删除。 (链表？)

3. `QList<T>`: **结合了单一类中QVector<T>和QLinkedList<T>最重要的优点**。支持随机访问，在任意一端插入或者移除项都是非常快的，对含有1000项以上的列表来说，在中间插入也是很快的，除非想在一个极大的列表中执行插入或者要求列表中的元素都必须占据连续的内存地址，否则QList<T>通常是最合适采用的多用途容器类。 连续内存+链表?占用空间大?

4. `QStack<T>`:提供push(),pop(),top() 

5. `QQueue<T>:`提供enqueue(),dequeue(),head() 



值类型T也可以是一个容器，在这种情况下，必须记得**用空格分开连续的尖括号**：QList<QVector<double> > list;



Q提供的两类迭代器用于遍历存储在容器中的项：Java风格的迭代器和STL风格的迭代器。**Java风格的迭代器易用于使用，STL风格的迭代器可以结合Qt和STL的一般算法而具有更加强大的功能。**



**对于每个容器类，都有两种 Java风格的迭代器类型：**

1. 只读迭代器 QVectorIterat or<T>,QLinkedIterator<T>,QListIterator<T> 

2. 读－写迭代器 QMutableVectorIterator<T>,QMutableLinkedIterator<T>,QMutableListIterator<T> 



**java风格的迭代器，本身并不是直接指向项的，而是能够定位在第一项之前，最后一项之后或者是两项之间。 **

一个典型的迭代循环如下： 

```
//顺序 

QList<int> list; 
QListIterator<int> i(list); 
    while(i.hasNext()) 
    { 
        qDebug() <<i.next(); 

    } 

... 
//倒序 

QList<int> list; 

QListIterator<int> i(list); 

i.toBack(); 
    while(i.hasPrevious()) 
    { 
        qDebug() << i.previous(); 
    } 

```



**STL风格迭代器：

两种风格STL迭代器： ** 

1. C<T>::interator 

2. C<T>::const_iterator 

例：

``` 

QList<int> list; 
...... 

//读写 
    QList<int>::iterator stli = list.begin();
    while(stli != list.end()) 
    { 
        *stli += 10;//每个变量增加10 
        stli++; 
    } 
    //只读 
    QList<int>::const_iterator stli_const = list.begin();
    while(stli_const != list.end()) 
    { 
        qDebug() << *stli_const; 
        stli_const++; 

    } 



    //修改

    



    QMutableListIterator<CCustomWidget *> l(m_wList);
    while(l.hasNext())
    {
        CCustomWidget *w = l.next();
        if(w == object){
            l.setValue(NULL);
            break;
        }
    }
```

**为了使隐含共享的作用发挥到最大，可以采用两个编程习惯： **

1. java风格的迭代器使用at()而不是[] 

2. STL风格的迭代器尽可能使用const_iterator,constBegin(),constEnd(); 



**关联容器: **

1. QMap<K,T>: 

2. QHash<K,T>:查找速度比QMap<K,T>快 



**QMultiMap，QMultiHash可以一个键对应多个值 **



**QString,QByteArray的相互转换：**

```

QByteArray arr; 
//QString -> QByteArray 

    arr = str.toAscii(); 
    foreach(quint8 i,arr) 
        qDebug() << QString::number(i,16); 
//QByteArray -> QString 
    str = arr.data(); 

    qDebug() << str; 

```




**关于默认构造函数：**

1. 没有提供任何构造函数，由C++自动提供默认构造函数

2. 没有任何参数的构造函数

3. 所有参数有默认值的构造函数。



**拷贝构造函数**：

拷贝构造函数是一种特殊的构造函数，函数的名称必须和类名称一致，它必须的一个参数是本类型的一个引用变量，如：`CExample(const CExample& C)`. 

下面三种对象需要调用拷贝构造函数： 

1. 对象以值传递的方式传入函数参数 

2. 对象以值传递的方式从函数返回 

3. 对象需要通过另外一个对象进行初始化,如: 

```
CExample A(100); 
CExample B = A; 
// CExample B(A); 

```

后两句都会调用拷贝构造函数 

对于一个类X, 如果一个构造函数的第一个参数是下列之一:

1. X&
2. const X&
3. volatile X&
4. const volatile X&

且没有其他参数或其他参数都有默认值,那么这个函数是拷贝构造函数. 

如果一个类中没有定义拷贝构造函数,那么编译器会自动产生一个默认的拷贝构造函数。

这个默认的参数可能为 X::X(const X&)或 X::X(X&),由编译器根据上下文决定选择哪一个。

关于拷贝构造函数参考:<http://blog.csdn.net/lwbeyond/article/details/6202256>



**qPrintable**：将字符串转换为char *,相当于`QString::toLocal8Bit().constData(); `



如果想**一次性读取或者写入一个文件**，可以完全不用QDataStream，而使用QIODevice的write()和readAll()函数. 



用 `qCompress()`和 `qUncompress`函数来**压缩和解压缩**数据。 



可以用 **QtIOCompressor**来压缩它写入的数据流，解压它要读入的数据流，而且不将整个文件存储在内存中。 



`QIODevice::peek()`：不移动设备位置 

`QIODevice::seek()`: 会移动设备位置 



#####Qt中的 Size Hints 和 Size Policies:
<http://www.tuicool.com/articles/uyaYn2>
1. 在 widget 有 layout 的情况下，其 sizeHint() 函数返回的是有效值作为其自身实际尺寸的参考；
2. sizeHint() 返回的值并不一定会作为 widget 的实际尺寸，因为 widget 的尺寸的决定还有其它因素作用；

什么叫有layout？应该是说这个widget用了setLayout就算有layout了，亦或是被layout包含了(layout->addWidget)?



layout 永远也不会把一个 widget 的大小设置到比 `minimumSizeHint() `返回的尺寸还小，除非 widget 设置了最小尺寸或者其 sizePolicy 属性设置了 `QSizePolicy::Ignore`。如果 widget 通过 `setMinimumSize()` 设置了最小尺寸，那么 minimumSizeHint() 的作用就会被忽略掉。我们知道如果在一个 layout 里面添加一些子 widget，然后窗口应用这个 layout 的时候，一般情况下我们是无法缩放到使其中的子 widget 看不见的。

sizePolicy:

这个属性保存了该 widget 的默认布局属性，如果它有一个 layout 来布局其子 widgets，那么这个 layout 的 size policy 将被使用；如果该 widget 没有 layout 来布局其子 widgets，那么它的 size policy 将被使用。默认的 policy 是 Preferred/Preferred



`widget->setWindowFlags(Qt::Window | Qt::WindowTitleHint);` 可以把** min, max 按钮**给去了 



`setBackgroundRole(QPalette::Dark);`//QPalette::Dark设置背景颜色 

`setAutoFillBackground(true);`//在paint event前自动填充背景 


**设置大小 策略 **
`setSizePolicy(QSizePolicy::Expanding,QSizePolicy::Expanding); `



**可以通过鼠标点击，TAB键获得焦点 **

`setFocusPolicy(Qt::StrongFocus); `



** QTableWidget 设置Header**

```

QTableWidget *messageTableWidget; 

...... 

//设置header 
    QStringList headers; 
    headers << tr("主题") << tr("发件人") << tr("时间"); 
    messageTableWidget->setHorizontalHeaderLabels(headers); 
    messageTableWidget->setColumnWidth(2,150); 
    //0，1列自适应大小 
    messageTableWidget->horizontalHeader()->setResizeMode(0,QHeaderView::Stretch); 
    messageTableWidget->horizontalHeader()->setResizeMode(1,QHeaderView::Stretch); 
    //最后一列自适应宽度 
//    messageTableWidget->horizontalHeader()->setStretchLastSection(true); 
    //整行选择 
    messageTableWidget->setSelectionBehavior(QAbstractItemView::SelectRows); 
//    messageTableWidget->setSelectionMode(QAbstractItemView::SingleSelection); 
    //不允许编辑 
    messageTableWidget->setEditTriggers(QAbstractItemView::NoEditTriggers); 

```



**居中显示：**

```
int main(int argc,char * argv[]) 
{ 
    QApplication app(argc,argv); 

    QDesktopWidget *pDesk = QApplication::desktop(); 
    MailClient mailClient(pDesk); 
    mailClient.move((pDesk->width() - mailClient.width()) / 2, (pDesk->height() - mailClient.height()) / 2); 
    mailClient.show(); 

    return app.exec(); 


} 

```



**保存与恢复：**

```
void MailClient::readSettings() 
{ 
    QSettings settings("Software Inc.","Mail Client"); 
    settings.beginGroup("mainWindow"); 
    this->restoreGeometry(settings.value("geometry").toByteArray()); 
    mainSplitter->restoreState(settings.value("mainSplitter").toByteArray()); 
    rightSplitter->restoreState(settings.value("rightSplitter").toByteArray()); 
    settings.endGroup(); 

} 

void MailClient::writeSettings() 
{ 
    QSettings settings("Software Inc.","Mail Client"); 
    settings.beginGroup("mainWindow"); 
    settings.setValue("geometry",saveGeometry()); 
    settings.setValue("mainSplitter",mainSplitter->saveState()); 
    settings.setValue("rightSplitter",rightSplitter->saveState()); 
    settings.endGroup(); 
} 

```



** 使用Splliter来布局(MailClient例子) **

```
    rightSplitter = new QSplitter(Qt::Vertical); 
    rightSplitter->addWidget(messageTableWidget); 
    rightSplitter->addWidget(textEdit); 
    rightSplitter->setStretchFactor(1,1);//窗口大小变化时，右上角的messageTableWidget大小不会变化

    mainSplitter = new QSplitter(Qt::Horizontal); 
    mainSplitter->addWidget(foldersTreeWidget); 
    mainSplitter->addWidget(rightSplitter); 
    mainSplitter->setStretchFactor(1,1);////窗口大小变化时，左边的foldersTreeWidget大小不会变化



    setCentralWidget(mainSplitter); 

```

***

# dock 

```
QDockWidget * dock = new QDockWidget(tr("Customers"),this); 
    //可dock的区域 
    dock->setAllowedAreas(Qt::LeftDockWidgetArea | Qt::RightDockWidgetArea); 
//    dock->setFeatures(QDockWidget::NoDockWidgetFeatures); 
//    qDebug() << dock->features(); 

    customerList = new QListWidget(dock); 

...... 
dock->setWidget(customerList); 
    addDockWidget(Qt::RightDockWidgetArea,dock); 

    viewMenu->addAction(dock->toggleViewAction()); 



...... 

QDockWidget *dock2 = new QDockWidget(tr("Paragraphs"), this); 

paragraphsList = new QListWidget(dock2); 

...... 
dock2->setWidget(paragraphsList); 
    addDockWidget(Qt::RightDockWidgetArea, dock2); 
    //用splitter布局 
//    splitDockWidget(dock,dock2,Qt::Vertical); 
    //使用tab方式来布局 

//    tabifyDockWidget(dock,dock2); 
//    dock->raise();//使用tab方式时，默认第一个dock在前面 

  
    viewMenu->addAction(dock2->toggleViewAction()); 

```

`QDockWidget::DockWidgetFeatures`定义特征，比如是否有close按钮，是否可以移动，是否可以floating

**[相关函数](http://blog.csdn.net/czyt1988/article/details/51209619)**

*  添加dock函数，此函数还有change功能：

```

void QMainWindow::addDockWidget(Qt::DockWidgetArea area, QDockWidget * dockwidget)

void QMainWindow::addDockWidget(Qt::DockWidgetArea area, QDockWidget * dockwidget, Qt::Orientation orientation)

```



* 分割dock窗口函数,此函数的功能是把两个dock进行左右或上下并排布置，做成一个类似QSplit的功能

```

void QMainWindow::splitDockWidget(QDockWidget * first, QDockWidget * second, Qt::Orientation orientation)

```

* tab化窗口函数.

```

void QMainWindow::tabifyDockWidget(QDockWidget * first, QDockWidget * second)

```

* 设置dock嵌套布局 

```

void QMainWindow::setDockNestingEnabled(bool enabled)

```

`setDockNestingEnabled(true);`允许嵌套dock

***

* 从manwindow移除并隐藏dockwidget，但并没有delete

```

void MainWindow::removeDockWidget(QDockWidget *dockwidget);

```

* Sets the given dock widget area to occupy the specified corner.

```

void MainWindow::setCorner(Qt::Corner corner, Qt::DockWidgetArea area);

```

[**设置QDockWidget的初始大小**](https://blog.csdn.net/imxiangzi/article/details/52541482)
如果用setMaximumSize和setFixedSize，的确可以设置初始大小，但也限制了QDockWidget的最大尺寸，不能用鼠标拖动来改变QDockWidget的大小.
解决方案,派生一个QWidget的新类，设置其sizeHint的返回值
```
class MyWidget : public QWidget  
{  
public:  
    QSize sizeHint() const  
    {  
        return QSize(270, 900); /* 在这里定义dock的初始大小 */  
    }  
}; 


QDockWidget *dock = new QDockWidget(&box);  
MyWidget *wi = new MyWidget;  
dock->setWidget(wi); 
```


**排他ACTION**

···

QActionGroup *group = new QActionGroup(this);

group->setExclusive(true);

···



**只执行一次的定时器: **

`QTimer::singleShot(1000);`



`QWidget::setSizePolicy();`设置大小规则 

`QWidget::setAttribute(Qt::WA_TranslucentBackground );`//半透明 

`QWidget::focusNextChild();`获得下一个控件，并让它获得焦点 

`QApplication::processEvents();`处理尚未被处理的事件，在单线程中防止无响应 

`QApplication::processEvents(QEventLoop::ExcludeUserInputEvents);`相对于上面，忽略鼠标和键盘事件。



**qt4自带的例子在/usr/lib/qt4,头文件在/usr/include/qt4 **


**Qt的坐标系**，然后讲解那几个函数，它们分别是： 

1. `translate()`函数，进行平移变换；

2. `scale()`函数，进行比例变换；

3. `rotate()`函数，进行旋转变换；

4. `shear()`函数，进行扭曲变换。 



最后介绍两个有用的函数`save()`和`restore()`，利用它们来保存和弹出坐标系的状态，从而实现快速利用几个变换来绘图 

**坐标转换的计算**<http://blog.sina.com.cn/s/blog_6e80f1390100xidr.html>

**关于window,view的转换和映射的代码： **

```
void Widget::paintEvent(QPaintEvent *) 
{ 
    QPainter painter(this); 
    //我的理解是在windows上绘图，而在view上显示 
    //所有的绘图函数(drawxxx(xxx))都是使用windows坐标 

    //window的-50,-50对应view的0，0 
    //也就是在window的(-50,-50)上绘图,实际显示为view(0,0) 
    //window(-50,50)映射view(0,0),window的单位长度变为100*100,X范围-100,0,Y范围为-100,0 
    painter.save();//保存坐标状态 
    painter.setWindow(-50,-50,100,100); 
    painter.setPen(Qt::red); 
    painter.drawRect(-50,-50,50,50); 

    painter.setPen(Qt::blue); 
    painter.drawRect(0,0,50-1,50-1);//起点在view的中点 

    painter.restore();//恢复坐标状态 
    painter.save();//保存坐标状态 

//    painter.setPen(Qt::yellow); 
//    painter.drawRect(101,0,100-2,100-1); 

    //window(0,0) -> view(0,0) 
    //虽然原点一样，但view区域只有原来的1/16，长宽只有原来的1/4,view长宽: 原来(200,200) -> 现在(100,100) 
    painter.setViewport(0,0,100,100); 
    painter.setPen(Qt::green); 
    // 1/4的一半的一半，面积只有1/16了(长宽1／4)(此时window的长宽还是200个单位,所以100/200也就是一半了) 

    //调整窗口大小此区域会变，因为2,3参数始终为100，而window大小在变。 
    painter.drawRect(0,0,100,100); 
    painter.setPen(Qt::darkYellow); 
    //调整窗口大小此区域不会变,宽度高度始终为view的一半。注意第2，3个参数 
    painter.drawRect(0,0,width()/2,height()/2); 

    painter.restore();//恢复坐标状态 

    //这里需要先恢复默认坐标映射，再用下面的代码 
    painter.save();//保存坐标状态 
    //原点在中间，X向右，Y向上增长 
    painter.setPen(Qt::yellow); 
    painter.setViewport(width()/2,height()/2,width(),-height()); 
    painter.drawRect(1,1,width()/2-2,height()/2-2); 

    painter.restore();//恢复坐标状态 
    painter.save();//保存坐标状态 

//    //这里的效果和上面两行一样 
//    painter.setWindow(-width()/2,height()/2,width(),-height()); 
//    painter.drawRect(0,0,width()/2-1,height()/2-1); 

    painter.restore();//恢复坐标状态 
}

```



**设置项item是否可编辑：**

```

tableWidget->setEditTriggers(QAbstractItemView::NoEditTriggers); 

tableWidget->setEditTriggers(QAbstractItemView::AnyKeyPressed);

```



**QTreeWidget的根节点： **

```

treeWidget-> invisibleRootItem() 

```



**QSettings类型转换： **

```

settings.value("").value<QColor>();

```



**颜色交替显示： **

```

tableView.setAlternatingRowColors(true); 

```



**选择一行**

`ui->tableView->setSelectionBehavior(QAbstractItemView::SelectRows);`



**对于只读的table model,必须要实现三个函数**:`rowCount()`,`columnCount()`,`data()`.



**如果要在程序很多地方使用QSetting**s，用 `QCoreApplication::setOrganizationName() `和 `QCoreApplication::setApplicationName() `然后用QSettings 的默认构造函数。 

这样，公司或组织名，应用程序名只要指定一次，QSettings settings 到处扔就行。 



**QSettings可以读ini文件。 **

**在用QSettings保存类对象时，注意拷贝构造函数一定要处理需要读写的变量**



**遍历控件**，网友提供，未验证:

```

QList<QPushButton*> allPButtons = this->findChildren<QPushButton *>();

```

**窗口最大化:**

```

setWindowState(Qt::WindowMaximized)

```



**为什么在ARM板上qt字体会变小？**

因为QT在ARM板上计算DPI值错误。
解决的方法就是设置好qt的dpi。
qt是根据显示器的物理长度或者宽度于分辨率的关系来计算dpi的。
对于QT5以下的版本设置如下：

```
    export QWS_DISPLAY="LinuxFB:mmWidth95:0" 
    export QWS_SIZE="480x272"

```
对于QT5：

```
    export QT_QPA_PLATFORM=linuxfb:fb=/dev/fb0:size=480x272:mmsize=95x53:offset=0x0

```

size指定屏幕分辨率，mmsize指定屏幕物理尺寸。offset指定偏移量。
这样qt在所有的平台上显示的字体都一样大了 就好了。 



**QPA**：Qt Platform Abstraction



**Plugin的使用(QT4):**

1.需要定义一个interface文件，用于定义Plugin导出的类，并在末尾`Q_DECLARE_INTERFACE(PluginTestInterface,"com.xp.PluginTestInterface")`，如：

//pluginTestInterface.h

```

class PluginTestInterface{
public:
    virtual int add(int a,int b)=0;//一定要是纯函数(=0)
};


Q_DECLARE_INTERFACE(PluginTestInterface,"com.xp.PluginTestInterface")

```

2.定义一个类，用于实现Interface定义的类及其方法，注意`Q_INTERFACES(PluginTestInterface)`：

//plugintest.h

```

#include <QObject>
#include "pluginTestInterface.h"

class PluginTest : public QObject,public PluginTestInterface
{
    Q_OBJECT
    Q_INTERFACES(PluginTestInterface)
public:
    explicit PluginTest(QObject *parent = 0);
    int add(int a, int b);
signals:
    
public slots:
    
};

```

3.实现类，并导出类，注意`Q_EXPORT_PLUGIN2("PluginTest",PluginTest)`：

//plugintest.cpp

```
#include "plugintest.h"
#include <QtCore>

PluginTest::PluginTest(QObject *parent) :
    QObject(parent)
{
}

int PluginTest::add(int a, int b)
{
    return a + b;
}

Q_EXPORT_PLUGIN2("PluginTest",PluginTest)

```



用这种方法进入指定目录:
```

QDir dirPlugin = QDir(app.applicationDirPath());
    dirPlugin.cd("..");
    dirPlugin.cd("PluginTest");
```



4.调用plugin
```

        QPluginLoader loader(strPlugin);

        QObject *plugin = loader.instance();
        qDebug() << plugin;
        if(plugin)
        {
            PluginTestInterface *iPluginTest = qobject_cast<PluginTestInterface *>(plugin);
            if(iPluginTest)
            {
                int rst = iPluginTest->add(1,2);
                qDebug() << "1+2="<<rst;
            }
            plugin = 0;
        }
        loader.unload();
```



另外还要注意plugin的pro文件：
```
TEMPLATE = lib

CONFIG +=plugin

#PluginTest要和Q_EXPORT_PLUGIN2的第一个参数一样

TARGET += PluginTest  #仅仅决定了生成dll的文件名，可以不用和项目名称一样
QT += declarative

```

**Plugin的使用(QT5):**
1. 定义接口
2. 使用`Q_DECLARE_INTERFACE()`告诉Qt的meta-object system有关接口的信息
3. 声明一个插件类，该类继承自QObject和插件想要提供的接口。
4. 使用`Q_INTERFACES（）`宏告诉Qt的meta-object system有关接口的信息。
5. 使用`Q_PLUGIN_METADATA()`导出插件
3. 使用`QPluginLoader`在应用中加载Plugin
4. 使用`qobject_cast（）`来测试插件是否实现给定的接口。
5. 使用合适的pro文件build插件（和qt4一样）

**qmake**
$$获取普通变量的值
$$()用于获取环境变量的值，如$$(PWD)
$()
$$[]访问qmake属性，如$$[QT_VERSION]


**qmldir文件:**

用于说明当前目录的文件。

比如某个目录为dir1,并且这个目录里有一个qmldir文件，文件内容为plugin qmlimageproviderplugin，则说明dir1目录里还有一个plugin文件，名字为libqmlimageproviderplugin.so



`Q_UNUSED(xx)`：意思是xx没用，在函数的某个参数没使用时可以让警告不出现。



另外一个终端：`xterm -e`



**QAbastractListModel**的子类必须实现`rowCount()`和`data()`,更好的情况也实现`headerData()`。如果要编辑列表，则需要实现`setData()`和`flags()`

**QFormLayout**是一个方便的布局类，它将上面的控件分成两列布局。左栏包括标签，右列则是那些值控件（QLineEdit，QSpinBox等）。传统上，这样的两栏式布局形式采用QGridLayout实现。 QFormLayout是更高级别的替代方案，提供了以下优点：

<http://blog.163.com/qimo601@126/blog/static/1582209320143293018744/>

 

**QML_DECLARE_TYPE()**等同于**Q_DECLARE_METATYPE(TYPE *) **and **Q_DECLARE_METATYPE(QDeclarativeListProperty<TYPE>)**

详见：<http://blog.chinaunix.net/uid-22235012-id-340913.html>



**Q_DECLARE_METATYPE**

如果要使自定义类型或其他非QMetaType内置类型在QVariant中使用，必须使用该宏。

* 该类型必须有公有的 构造、析构、复制构造 函数

* qRegisterMetaType 必须使用该函数的两种情况

* 如果非QMetaType内置类型要在 Qt 的属性系统中使用

* 如果非QMetaType内置类型要在 queued 信号与槽 中使用 


 ```

struct MyStruct
 {
     int i;
     ...
 };

 Q_DECLARE_METATYPE(MyStruct)

......

 MyStruct s;
 QVariant var;
 var.setValue(s); // copy s into the variant      var= QVariant::fromValue?

 ...

 // retrieve the value
 MyStruct s2 = var.value<MyStruct>();

 ```



**Q_DECLARE_METATYPE() **如果要使自定义类型或其他非QMetaType内置类型在QVaiant中使用，必须使用该宏。。该类型必须有公有的 构造、析构、复制构造 函数.

<http://www.360doc.com/content/13/0313/13/9200790_271226432.shtml>

<http://blog.chinaunix.net/uid-22235012-id-340913.html>

**qRegisterMetaType() **如果非QMetaType内置类型要在 Qt 的属性系统中使用如果非QMetaType内置类型要在 queued 信号与槽 中使用.

**Q_DECLARE_FLAGS ( Flags, Enum )**：定义一个名为Flags，类型为Enum组合的新类型，Enum枚举类型须已经定义。和delphi中的set of Txx类似.



一个**事件过滤器**的安装需要下面2个步骤： 

1. 调用`installEventFilter（）`注册需要管理的对象。 
2. 在`eventFilter() `里处理需要管理的对象的事件。 
<http://blog.csdn.net/xj178926426/article/details/6461586>
 
**Qt提供5个级别的事件处理和过滤:**

1. 重新实现事件函数。 比如： mousePressEvent(), keyPress-Event(),   paintEvent() 。 这是最常规的事件处理方法。 

2. 重新实现QObject::event(). 这一般用在Qt没有提供该事件的处理函数时。也就是，我们增加新的事件时。 
3. 安装事件过滤器 
4. 在 QApplication 上安装事件过滤器。 这之所以被单独列出来是因为： QApplication 上的事件过滤器将捕获应用程序的所有事件，而且第一个获得该事件。也就是说事件在发送给其它任何一个event filter之前发送给QApplication的event filter。 
5. 重新实现QApplication 的 notify()方法. Qt使用 notify()来分发事件。要想在任何事件处理器捕获事件之前捕获事件，唯一的方法就是重新实现QApplication 的 notify()方法。 



**Qt事件机制:**

<http://qimo601.iteye.com/blog/1407911>

**我们按产生来源把事件分为两类：**

1.  系统产生的;通常是window system把从系统得到的消息,比如鼠标按键,键盘按键等, 放入系统的消息队列中，Qt事件循环的时候读取这些事件,转化为QEvent,再依次处理.

2.  是由Qt应用程序程序自身产生的.程序产生事件有两种方式,:

    * 一种是调用`QApplication::postEvent().` 例如QWidget::update()函数,当需要重新绘制屏幕时,程序调用update()函数,new出来一个paintEvent,调用 QApplication::postEvent(),将其放入**Qt的消息队列中**,等待依次被处理. 

    * 另一种方式是调用`sendEvent()`函数. 这时候事件不会放入队列, 而是**直接被派发和处理**, QWidget::repaint()函数用的就是这种方式。实际上QApplication::sendEvent()是通过调用`QApplication::notify()`, 直接进入了事件的派发和处理环节



件过滤器函数( `eventFilter() `) 返回值是bool型, 如果返回true, 则表示该事件已经被处理完毕, Qt将直接返回, 进行下一事件的处理; 如果返回false, 事件将接着被送往剩下的事件过滤器或是目标对象进行处理. 



1. Qt中,事件的派发是从`QApplication::notify()` 开始的

2. 之后,事件被送到reciver::event() 处理.

(上面都要检查有无事件过滤器，如果有就先处理时间过滤器。)

3. 调用相应的特定事件处理函数，如mousePressEvent,paintEvent......



对于某些类别的事件, 如果在整个事件的派发过程结束后还没有被处理, 那么这个事件将会向上转发给它的父widget, 直到最顶层窗口.



**禁止获得焦点:**



```

m_qmlHeaderBar->setFocusPolicy(Qt::NoFocus);
```



#####qt隐藏鼠标图标：

1. 在运行程序的加上参数-nomouse，这样，当前启动的程序就不会出现鼠标光标。

2. 在编译QT库的时候添加编译选项QT_NO_CURSOR，这样cursor相关的代码就不会被编译进去，自然鼠标光标也不会出现在程序中。具体做法是在编译的时候加上-no-feature-CURSOR。据说在编译的时候加-nomouse也可以，但是这样触摸屏也无法点击。

3. 只希望在某个QWidget下不出现鼠标光标，则只要对这个widget调用`QWidget::setCursor(QCursor(Qt::BlankCursor))`，其它的窗口仍将出现鼠标。

4. 在main函数中，实例化了APPLICATION后，调用`QApplication::setOverrideCursor(Qt::BlankCursor);`

5. 任一控件下显示与关闭鼠标

```

  this->setCursor(Qt::BlankCursor);   //隐藏鼠标
  this->setCursor(Qt::ArrowCursor);  //显示正常鼠标

```
  this改为需要隐藏鼠标的部件，就可以令当鼠标移动到该部件时候，效果生效。 以上的都需要动一下鼠标才会消失，不知道不是我没有搞好，下面一启动就可以隐藏起来

6. 调用下面函数：

`QWSServer::setCursorVisible(false)`;这个方法还有待研究，具体怎么加还不是很明白。



**返回当前系统的语言和国家**

```

QLocale::system().name()

```



#####国际化:

<http://my.oschina.net/shelllife/blog/120678>

<http://blog.163.com/soyo_gogogo/blog/static/171414077201213112640267/><blog.csdn.net/xiao69/article/details/19371699>

**Qt国际化的一般步骤**
运行 lupdate，从应用程序的代码中提取所有界面上的可见字符。      
这些可见字符必须被 tr() 、QCoreApplication::translate()、Qt_TR_NOOP()、Qt_TRANSLATE_NOOP()等来包裹字符串，具体这些函数或者宏是什么功能，我们后面细说。

使用 Qt Linguist 翻译应用程序。
运行 lrelease，生成二进制的 .qm 文件，应用程序可以使用 QTranslator 加载这个文件。
工具:

`linguist`     用来进行语言翻译的辅助图形界面工具，方便地进行语言的翻译，可提高翻译效率但非必须

`lupdate`     用来检查源文件并生成待翻译的TS格式文件的工具，它检查源文件使用了tr函数的地方.

        例'lupdate xx.pro -ts xx.ts',这样会包含项目中的所有h和cpp文件，而不用一一指定

`lconvert`  用来合并ts文件，不是必须，发现合并后的文件会覆盖之前的文件，建议不用。

        例`lconvert app.ts qml.ts -o displayChinese_zh_CN.ts`

`lrelease`    用来将XML格式的TS翻译文件转换成QT使用的二进制格式的文件工具，以TS文件为输入



**如果是qml项目，需要分别处理ts：**

1. 项目文件xxx.pro,得到所有h，cpp文件需要翻译的内容

2. qml文件

3. 手动添加内容



**如何使用中文：**

1. cpp,h文件在需要翻译的地方用'QObject::tr("abc")'，qml使用qsTr("abc")

1. `lupdate *.h *.cpp  qml/*.qml -ts source.ts`

2. `lupdate *.pro -ts pro.ts`

3. `lconvert source.ts pro.ts -o UT285_zh_CN.ts`

4.  用linguist打开UT285_zh_CN.ts，并翻译好内容

5.  点击linguist的文件菜单，选"发布"d

6. 在main函数里：

```

QTextCodec::setCodecForLocale(QTextCodec::codecForName("UTF-8"));//UTF-8 GBK    QTextCodec::setCodecForCStrings(QTextCodec::codecForName("UTF-8"));    QTextCodec::setCodecForTr(QTextCodec::codecForName("UTF-8"));

QTranslator translator;    translator.load("test.qm");    

a.installTranslator(&translator);        

QFont font;

//font.setFamily("wqy-zenhei");//wqy-zenhei    

font.setPointSize(11);   

font.setBold(false);    

a.setFont(font);

```

7. 现实中文要有中文字体才行，用文泉驿，windows的simsun.ttc都可以，将其中一个拷贝到Qt目录的lib/fonts里



备注：

**关于qml listmodel的国际化：**

<http://thierry-xing.iteye.com/blog/1344866>

方法有两种：

1. 在元素中需要翻译的地方使用宏QT_TR_NOOP,在delegate中使用qsTr。 这种方法未成功

```

ListModel{       

    id: model1        

    ListElement{aid:1;name:QT_TR_NOOP("Histogram");icon:"image/1.png"}

    ...

}

...

//在delegate中：

Text{

    text: qsTr(name)   

}

```

2. 使用js实现

```

ListModel{       

     id: model1

    ListElement{aid:1;icon:"image/1.png"}        

    ListElement{aid:2;icon:"image/2.png"}
   function name(index) {            

        if ( name[ "text" ] === undefined) {                

                name.text = [                            

                    qsTr( "Histogram" ) ,                            

                    qsTr( "w" ) ,                        

                ]            

        }            

        return name.text[index]        

    }

//在delegate中：

Text{

    text: container.GridView.view.model.name(index);//container为delegate顶层元素

}

```



**XML的国际化：**

```





XmlListModel{
        id: xmlModel
        source:"qrc:/qml/GridMenu.xml"
        query:"/menus/menu"
        XmlRole{name:"name";query:"name/string()"}
        XmlRole{name:"icon";query:"icon/string()"}
        XmlRole{name:"file";query:"file/string()"}

        function name(index)
        {
            name.text = qsTr(get(index).name);
            return name.text;
        }
    }

```

delegate：

```

Text{





text: container.GridView.view.model.name(index);//
}

```

**qt的中文翻译文件**在安装包的translations目录里。比如：/home/xp/embedded/tool/cross/qt-x86/translations



**长按处理:**

```





ui->btn1->setAutoRepeat(true);
ui->btn1->setAutoRepeatDelay(3000);//首次触发长按的时间
ui->btn1->setAutoRepeatInterval(1000);//之后产生长按的间隔
...
//长按也是发送clicked信号的
void Widget::on_btn1_clicked()
{    
    qDebug() << "on_btn1_clicked";
}

```

**液晶，LCD ，段码：**（demo: digitalclock）



```

QLCDNumber
```



`QWidget::mouseTracking : bool`  

false（默认值）：没有鼠标按下就不会产生mouseMove事件

true：即使没有鼠标按下也不会产生mouseMove事件



**2D绘图:**

<http://blog.csdn.net/zenwanxin/article/details/6524529>

**反锯齿： **`painter.setRenderHint(QPainter::Antialiasing);`



**坐标转换**(图例讲得比较容易理解):

<http://blog.sina.com.cn/s/blog_6e80f1390100xidr.html>



**直接调整宽度：**

```

 QSize size(100, 10);
 size.rwidth() += 20;
//size变成(120,10)
```

这个是啥玩意(demo: tooltips):  默认的边界大小？

```





int margin = style()->pixelMetric(QStyle::PM_DefaultTopLevelMargin);
```



**鼠标没有按键按下，移动鼠标也会产生mouseMove事件**

```

setMouseTracking(true);

```

**使用ToolTip**:

```

bool SortingBox::event(QEvent *event)

{//! [5] //! [6]    

    if (event->type() == QEvent::ToolTip) {        

        QHelpEvent *helpEvent = static_cast<QHelpEvent *>(event);        

        int index = itemAt(helpEvent->pos());        

        if (index != -1) {            

            QToolTip::showText(helpEvent->globalPos(), shapeItems[index].toolTip());        

        } else {            

            QToolTip::hideText();            

            event->ignore();        

        }
       return true;    

    }    

    return QWidget::event(event);

}

```

**根据类名创建对象：**

<http://bbs.csdn.net/topics/340251573>

```

class Parser {
public:
 virtual void parse() = 0;
 virtual ~Parser() {};
};
...

class Parser1 : public Parser {
public:
    Parser1() {
        qDebug() <<"Parser1::Parser1()";
    }    
    void parse() {
        qDebug() << "Parser1::parse()";
    }
    ~Parser1() {
       qDebug() <<"Parser1::~Parser1()";
    }
};
Q_DECLARE_METATYPE(Parser1)
  
class Parser2 : public Parser {
public:
    Parser2() {
        qDebug() <<"Parser2::Parser2()";
    }
    void parse() {
        qDebug() << "Parser2::parse()";
    }
    ~Parser2() {
       qDebug() <<"Parser2::~Parser2()";
    }
};
Q_DECLARE_METATYPE(Parser2)

...

void factory( const char* parserName ) {
     int id = QMetaType::type( parserName );
     if (id != -1) {
        Parser *parser = static_cast< Parser* > 
                         ( QMetaType::construct( id ) );
        parser->parse();
        delete parser;
    }
}
...

int main ( int argc, char* argv[] )
{
    qRegisterMetaType<Parser1>("Parser1");
    qRegisterMetaType<Parser2>("Parser2");
    
    qDebug() << "###### Trying create Parser1";
    factory("Parser1");
    
    qDebug() << "###### Trying create Parser2";
    factory("Parser2");
}

```

**获得一个类的类名：**

`



MyClass::staticMetaObject.className()
`

foreach循环会在进入循环时自动复制一个容器，因此即使在迭代过程中修改了容器类，也不会影响到循环。也就是说不能修改值?







使用Java风格的迭代器修改项时，需要setValue来设定值:

```





    QMutableListIterator<int> i(values);
    while(i.hasNext()){
        int value = i.next();
       value = 3;
        ......

        i.setValue(value);
    }
```



**保留小数位数：**

```





str = QString::number(33.12345,'f',2);//保留两位小数
```



`Q_EXPORT_PLUGIN`已过时，用'Q_EXPORT_PLUGIN2'替代



**使用plugin**？很简单：

1. 定义一个`QDeclarativeExtensionPlugin`的子类

```





class ChartsPlugin : public QDeclarativeExtensionPlugin
{
    ....
}
```

2. 实现虚函数`virtual void registerTypes(const char *uri);`

3. 在第2步的函数里注册类:

```





void ChartsPlugin::registerTypes(const char *uri)
{
    qmlRegisterType<PieSlice>(uri,1,0,"PieSlice");
    qmlRegisterType<PieChart>(uri,1,0,"PieChart");
}
```

4. 使用`Q_EXPORT_PLUGIN2(chartsplugin,ChartsPlugin)`来导出到plugin



完成代码：

h文件

```





#include <QDeclarativeExtensionPlugin>








class ChartsPlugin : public QDeclarativeExtensionPlugin
{
    Q_OBJECT
public:
    explicit ChartsPlugin(QObject *parent = 0);
    
    virtual void registerTypes(const char *uri);
    
};


```

cpp文件：

```





ChartsPlugin::ChartsPlugin(QObject *parent) :
    QDeclarativeExtensionPlugin(parent)
{
}

void ChartsPlugin::registerTypes(const char *uri)
{
    qmlRegisterType<PieSlice>(uri,1,0,"PieSlice");
    qmlRegisterType<PieChart>(uri,1,0,"PieChart");
}

Q_EXPORT_PLUGIN2(chartsplugin,ChartsPlugin)

```

上面这一种貌似只能用于qml



另外也可以使用interface来实现（这种用于C++？），涉及到`Q_DECLARE_INTERFACE`，`Q_INTERFACES`，`Q_EXPORT_PLUGIN2`



**tableview的资料**

<http://blog.sina.com.cn/s/blog_a6fb6cc90101dd5u.html>

<http://blog.sina.com.cn/s/blog_a6fb6cc90101i8it.html>

**mvc:**

帮助文档翻译:<http://blog.csdn.net/leo115/article/details/7532677>

如果model只读，需要实现下面几个函数

1. Flags.其他的组件可以通过这个得知每个Item的信息，在大多数的models中，包含Qt::ItemIsEnable,Qt::ItemIsSelectable

data,被用来提供数据给视图和代理，一般的，models只要提供Qt::DisplayRole和任何程序特殊的角色，也有一些特殊的Qt::ToolTipRole等，详细可以看Qt::ItemDataRole。

2. headerData,为视图的头部提供信息数据。

3. rowCount提供这个model有多少行数据。

4. columnCount(在QAbstractTableModel和QAbstractItemModel中)



除了构造函数，我们仅需要实现两个函数：`rowCount()`返回model中的行数，`data()`返回与特定model index对应的数据项。具有良好行为的model也会实现`headerData()`，它返回tree和table views需要的，在标题中显示的数据。假如model具有**层次结构**，我们也应该实现`index()`与`parent()`函数。



**如果需要编辑：**

1. Flags,必须包含Qt::ItemDataRole。

2. setData，被用来修改和特殊的模型索引相关的项目。修改的数据必须是Qt::EditRole，发送一个dataChanged信号

3. setHeaderData，用来修改水平和垂直的头信息，发出一个headerDataChanged信号。



一个view创建时必不需要model,但在它能显示一些真正有用的信息之前，必须提供一个model。view通过使用`selections`来跟踪用户选择的数据项。每个view可以维护单独使用的selections，也可以在多个views之间共享。有些views,如QTableView和QTreeView,除数据项之外也可显示标题(Headers)，标题部分通过一个view来实现，`QHeaderView`。标题与view一样总是从相同的model中获取数据。从 model中获取数据的函数是`QabstractItemModel::headerDate()`，一般总是以表单的形式中显示标题信息。可以从QHeaderView子类化，以实现更为复杂的定制化需求。



**概念总结：**
1. Model indexes为views与delegages提供model中数据项定位的信息，它与底层的数据结构无关。
2. 通过指定行，列数，父项的model index来引用数据项。
3. 依照别的组件的要求，model indexes被model构建。
4. 使用index()时，如果指定了有效的父项的model index,那么返回得到的model index对应于父项的某个孩子。
5. 使用index()时，如果指定了无效的父项的model index,那么返回得到的model index对应于顶层项的某个孩子。
6. 角色对一个数据项包含的不同类型的数据给出了区分。



view中数据项选择机制由`QItemSelectionModel`类提供。所有标准的view缺省都构建它们自己的选择模型，以标准的方式与它们交互。选择模型可以用selectionModel()函数取得，替代的选择模型也可以通过`setSelectionModel()`来设置。当我们想在一个model上提供多个一致的views时，这种对选择模型的控制能力非常有用。通常来讲，除非你子类化一个model或view,你不必直接操纵selections的内容。

例：`m_listView->setSelectionModel(m_tableView->selectionModel());`



**选择模型：（较重要） **

```

QItemSelectionModel *m_selectionModel;





m_selectionModel = m_listView->selectionModel();
...
//选择指定项
void Widget::onBtnSelectClicked()
{    
    QModelIndex topLeft = m_model->index(0,0);    
    QModelIndex bottomRight = m_model->index(1,0);
    QItemSelection selection(topLeft,bottomRight);
    m_selectionModel->select(selection,QItemSelectionModel::Toggle);
    m_btnEditSelect->setEnabled(m_selectionModel->selectedIndexes().count() > 0);
}
//修改选择项的数据
void Widget::onBtnEditSelectClicked()
{    
    if(m_selectionModel->selectedIndexes().count() == 0)        
        return;
    QModelIndexList indexs = m_selectionModel->selectedIndexes();    
    foreach (QModelIndex index, indexs) { 
        QString text = QString("%1,%2").arg(index.row()).arg(index.column());        
        m_model->setData(index,text);    
    }
}

```
1. 共享选择模型

`m_tableView->setSelectionModel(m_listView->selectionModel()) `

2. 信号`selectionChanged()`和`currentChanged()`

```





//SelectionModel的selectionChanged
void Widget::onSelectionModelselectionChanged(const QItemSelection &selected, const QItemSelection &deselected)
{
    qDebug() << "selectionChanged: " ;
    QModelIndexList indexs = selected.indexes();
    foreach(QModelIndex index,indexs)
    {
        qDebug() << "selected" <<index.row() << "," << index.column()<<": "<< m_model->data(index).toString();
    }

    indexs = deselected.indexes();
    foreach(QModelIndex index,indexs)
    {
        qDebug() << "deselected" <<index.row() << "," << index.column()<<": "<< m_model->data(index).toString();
    }
    qDebug() <<"************************************************************************";
}
//SelectionModel的currentChangedvoid 
Widget::onSelectionModelcurrentChanged(const QModelIndex &current, const QModelIndex &previous){    
    qDebug() << "currentChanged: " ;
    qDebug() << "current" <<current.row() << "," << current.column()<<": "<< m_model->data(current).toString();
    qDebug() << "previous" <<previous.row() << "," << previous.column()<<": "<< m_model->data(previous).toString();
    qDebug() <<"************************************************************************";
}
```



**Delegate:**

与MVC模式不同，model/view结构没有用于与用户交互的完全独立的组件。一般来讲， view负责把数据展示给用户，也处理用户的输入。为了获得更多的灵性性，交互通过delegagte执行。它既提供输入功能又负责渲染view中的每个数据项。 控制delegates的标准接口在QAbstractItemDelegate类中定义。Delegates通过实现paint()和sizeHint()以达到渲染内容的目的。然而，简单的基于widget的delegates,可以从QItemDelegate子类化，而不是QAbstractItemDelegate,这样可以使用它提供的上述函数的缺省实现。delegate可以使用widget来处理编辑过程，也可以直接对事件进行处理。

Qt提供的标准views都使用QItemDelegate的实例来提供编辑功能。它以普通的风格来为每个标准view渲染数据项。这些标准的views包括：QListView,QTableView,QTreeView。所有标准的角色都通过标准views包含的缺省delegate进行处理。一个view使用的delegate可以用itemDelegate()函数取得,而setItemDelegate()函数可以安装一个定制delegate。

设置delegate:

`



m_tableView->setItemDelegate(delegate)
`

也可单独设置行或列的delegate:

```





m_tableView->setItemDelegateForColumn(3,delegate);
m_tableView->setItemDelegateForRow(1,delegate);
```





一般从QItemDelegate继承，并实现下面的函数：

```





//paint就是负责平时是怎么显示的
    void paint(QPainter *painter, const QStyleOptionViewItem &option, const QModelIndex &index) const;
    //下面这个3个函数就负责编辑
    //创建一个编辑控件
    QWidget * createEditor(QWidget *parent, const QStyleOptionViewItem &option,
                           const QModelIndex &index) const;
    //编辑控件怎么显示
    void setEditorData(QWidget *editor, const QModelIndex &index) const;
    //保存值到model
    void setModelData(QWidget *editor, QAbstractItemModel *model, const QModelIndex &index) const;
    //负责编辑控件的几何形状
    void updateEditorGeometry(QWidget *editor, const QStyleOptionViewItem &option,                              const QModelIndex &index) const;
```



`QObject::sender()`返回发射了触发这个槽的信号的对象。



`listView->setEditTriggers()`可设置view是否可编辑，以及触发编辑的条件。



添加并编辑：

```





int row = listView->currentIndex().row();
    model->insertRows(row,1);//添加一行

    QModelIndex index = model->index(row);
    listView->setCurrentIndex(index);
    listView->edit(index);//编辑当前行
```



当用户单击OK或者Cancel按钮时，就会调用done

QDialog::done(int result)



```





treeView->header()->setStretchLastSection(true);//最后一列占用剩下的空间

```



交替颜色:

`



tableView.setAlternatingRowColors(true);
`

**在tableview里嵌入checkbox**

<http://qimo601.iteye.com/blog/1538364>



**QT提供了一些现成的models用于处理数据项：**
QStringListModel 用于存储简单的QString列表。
QStandardItemModel 管理复杂的树型结构数据项，每项都可以包含任意数据。
QDirModel  提供本地文件系统中的文件与目录信息。
QSqlQueryModel, QSqlTableModel,QSqlRelationTableModel用来访问数据库。
假如这些标准Model不满足你的需要，你应该子类化QAbstractItemModel,QAbstractListModel或是QAbstractTableModel来定制。



在model/view架构中，有两种方法进行**排序**，选择哪种方法依赖于你的底层Model。
假如你的model是可排序的，也就是它重新实现了QAbstractItemModel::sort()函数，QTableView与QTreeView都提供了API,允许你以编程的方式对Model数据进行排序。另外，你也可以进行交互方式下的排序（例如，允许用户通过点击view表头的方式对数据进行排序），可以这样做：把QHeaderView::sectionClicked()信号与QTableView::sortByColum()槽或QTreeView::sortByColumn()槽进行联结就好了。
另一种方法是，假如你的model没有提供需要的接口或是你想用list view表示数据，可以用一个代理model在用view表示数据之前对你的model数据结构进行转换。



当前目录:

```





QDir::currentPath();
//或者
qApp->applicationDirPath();
```
当前执行文件：
```
qApp->applicationFilePath();
```

临时的model indexes由QModelIndex提供，而具有持久能力的model indexes则由`QPersistentModelIndex`提供
在获取对应一个数据项的model index时，需要考虑有关于model的三个属性：行数，列数，父项的model index。


**使用Model Indexes**
```
QDirModel *model = new QDirModel;
     QModelIndex parentIndex = model->index(QDir::currentPath());
     int numRows = model->rowCount(parentIndex);
 for (int row = 0; row < numRows; ++row)
 {
         QModelIndex index = model->index(row, 0, parentIndex);
         tring text = model->data(index, Qt::DisplayRole).toString();
         // Display the text in a widget.

     }
```
以上的例子说明了从**model中获取数据的基本原则**：
1. model的尺寸可以从rowCount()与columnCount()中得出。这些函数通常都需要一个表示父项的model index。
2. model indexes用来从model中访问数据项，数据项用行，列，父项model index定位。
3. 为了访问model顶层项，可以使用QModelIndex()指定。
4. 数据项为不同的角色提供不同的数据。为了获取数据，除了model index之外，还要指定角色。

**字符串的宽度和高度：**
```
QFontMetrics fm(painter->font());
QString str = QObject::tr("Count:%1  Total:%2  Min:%3  Max:%4  Avg:%5").arg(count).arg(total).arg(min).arg(max).arg(avg);
int x1 = m_drawRect.left() +(m_drawRect.width() - fm.width(str))/2 ;    
int y1 =  m_drawRect.top() /2 - fm.height();

```

**安装QSerialPort:**
<http://wiki.qt.io/QtSerialPort#cite_note-1>

以下描述适合QT4：
1. 步骤
```
$ git clone git://code.qt.io/qt/qtserialport.git  //执行命令后，会在当前目录产生qtserialport目录
$ cd qtserialport
```

2. 步骤
```
$ git checkout qt4-dev
```
3. 貌似可以不用
```
$ git branch -a
```

4. 使用qtcreator打开qtserialport.pro，并重新编译
5. 在当前目录执行`sudo make install`

**QtSerialPort的使用**
<http://my.oschina.net/CgShare/blog/214926>


**线程Thread:**
<http://blog.csdn.net/dbzhang800/article/details/6554104>
<http://www.cppblog.com/bitdewy/archive/2012/05/28/176553.aspx>
<http://my.oschina.net/CgShare/blog/215057?p=1>

**线程同步：**
<http://blog.csdn.net/michealtx/article/details/6853604>
1. QMutex
2. QMutex + QMutexLocker 
3. QReadWriteLock
4. QReadWriteLock + QReadLocker + QWriteLocker
5. QSemaphore
6. QWaitCondition
QWaitCondition最大的好处，我觉得，是能在一个线程中唤醒一个或多个其它线程，当然前提是，其它线程在等待某个
QWaitCondition，否则不起作用，你唤醒也没用。QWaitCondition必须与QMutex或者QReadwriteLock一起用。

`run`对于线程的作用相当于main函数对于应用程序。它是线程的入口，run的开始和结束意味着线程的开始和结束。

在子线程中使用信号，槽：
<http://blog.csdn.net/c05170519/article/details/6459809>

```
include <QtCore/QCoreApplication>
#include <QtCore/QObject>
#include <QtCore/QThread>
#include <QtCore/QDebug>
class Dummy:public QObject{    
    Q_OBJECT
public:    
    Dummy(QObject* parent=0):QObject(parent){}
public slots:    
    void emitsig()    
    {        
        emit sig();    
    }
signals:    
    void sig();
    };
class Object:public QObject
{
    Q_OBJECT
    public:    Object(){}
public slots:    
    void slot()    
    {        
        qDebug()<<"from thread slot:" <<QThread::currentThreadId();    
    }
};
#include "main.moc"
int main(int argc, char *argv[])
{    
    QCoreApplication a(argc, argv);    
    qDebug()<<"main thread:"<<QThread::currentThreadId();    
    QThread thread;    
    Object obj;    
    Dummy dummy;    
    obj.moveToThread(&thread);    
    QObject::connect(&dummy, SIGNAL(sig()), &obj, SLOT(slot()));    
    thread.start();    
    dummy.emitsig();    
    return a.exec();
}
```
结果：恩，slot确实不在主线程中运行（这么简单不值得欢呼么？）
main thread: 0x1a5c 
from thread slot: 

**关于线程的使用自己总结**
1. 因为发送者所在的线程是无关紧要的，所有在QThread子类中添加信号是安全的。(子线程 -> 别的线程)

```
class Thread : public QThread
{
    Q_OBJECT 
signals:
    void aSignal(); 
protected:
    void run() {
        emit aSignal();
    }
};
 
/* ... */
Thread thread;
Object obj;
QObject::connect(&thread, SIGNAL(aSignal()), &obj, SLOT(aSlot()));
thread.start();
```

2. 如果要向子类发送信号(别的线程 -> 子线程)，则需要这样做：

```
class Worker : public QObject
{
    Q_OBJECT 
public slots:
    void doWork() {
        /* ... */
    }
};
 
/* ... */
QThread *thread = new QThread;
Worker *worker = new Worker;
connect(obj, SIGNAL(workReady()), worker, SLOT(doWork()));
worker->moveToThread(thread);
thread->start();
```

注意：
首先是子线程的使用，就仿上面最后的例子做的。但是有几点说明：
1. 新建的两给类都必须是Qobject的子类。
2.  建立子线程那快代码必须放在主程序里，就是最后要有return exec().QT新建等待文件中，有main.cpp和mianwindows.cpp,千万不能放入后者。当QT应用程序开始时，只有主线成是在运行的，主线成是唯一允许创建QApplication或QCoreApplication对象，并且可以对创建的对象调用exec()的线程。在调用exec()之后，这个线程等待一个事件或者处理一个时间。

**QByteArray**
<http://blog.csdn.net/xgbing/article/details/7771898>
<http://blog.chinaunix.net/uid-23381466-id-3896956.html>

**Qt编码惯例**
<http://blog.csdn.net/qter_wd007/article/details/6557191>

**d指针和q指针:**
<http://blog.csdn.net/mznewfacer/article/details/6976293>
 

**为自定义数据类型提供流操作符有几个好处：**
1. 允许流输出使用自定义类型的容器
2. 可以将这些数据类型的值存储为QVariant的形式，这便于他们在更大的范围内使用.P221


**QDataStream如果仅仅读写基本C++数据类型，甚至都不必调用setVersion()函数。**

**在控制台输出字符：**
```
QTextStream out(stdout);
out << QObject::tr("Total number of ports available: ") << serialPortInfoList.count() << endl;
```
**在控制台获取输入字符**
```
QTextStream standardOutput(stdout);
QFile dataFile;    
if (!dataFile.open(stdin, QIODevice::ReadOnly)) {        
    standardOutput << QObject::tr("Failed to open stdin for reading") << endl;        
    return 1;    
}
QByteArray writeData(dataFile.readAll());    
dataFile.close();
```
**获取参数**
```
QStringList argumentList = QCoreApplication::arguments();
```

**检查串口是不是有错误**
```
if (serialPort.error() == QSerialPort::ReadError) {
...
}
```

**通过调色板改变颜色**
```
QPalette p;    
p.setColor(QPalette::Base,Qt::black);    
p.setColor(QPalette::Text,Qt::white);    
p.setColor(QPalette::Background,Qt::yellow);    
setPalette(p);
```
**调色板的QPalette的使用**
<http://www.tuicool.com/articles/rqIZ7r> 
通过使用调色板可以设置按钮的背景色（可以是图片）
```
ui->toolBt->setFont(QFont("宋体",20,QFont::Bold));
ui->toolBt->setAutoRaise(true);
ui->toolBt->setAutoFillBackground(true);
QPalette pl = ui->toolBt->palette(); 
//设置按钮文字颜色
pl.setColor(QPalette::ButtonText,QColor(Qt::red));
//使用setBrush设置图片
pl.setBrush(QPalette::Button,QBrush(QPixmap(":/new/resources/otherPage/tap_bg.png")));
ui->toolBt->setPalette(pl);
```

**绘图相关资料**
<http://blog.csdn.net/zenwanxin/article/details/6524529>


**Qt 使用`QDialog::exec()`实现应用程序级别的模态对话框，使用`QDialog::open()`实现窗口级别的模态对话框，使用`QDialog::show()`实现非模态对话框。**

**关闭后释放资源**
`dialog->setAttribute(Qt::WA_DeleteOnClose);`

**在资源文件里访问本地文件**
在路径前家`file:`
如要引用"lib"目录:
`import "file:lib"`

**设置背景色**
`setBackgroundRole(QPalette::Base);`

**显示tooltips**
见tooltips例子
```
bool SortingBox::event(QEvent *event){//! [5] //! [6]    
    if (event->type() == QEvent::ToolTip) {        
            QHelpEvent *helpEvent = static_cast<QHelpEvent *>(event);        
            int index = itemAt(helpEvent->pos());        
            if (index != -1) {            
                QToolTip::showText(helpEvent->globalPos(), shapeItems[index].toolTip());        
            } else {            
                QToolTip::hideText();            
                event->ignore();        
            }
        return true;    
     }    
     return QWidget::event(event);
     }
```
**获得边框宽度**
`int margin = style()->pixelMetric(QStyle::PM_DefaultTopLevelMargin);`


**qt可以调用linux的api，只要引用相关头文件即可**
```
int main(int argc, char *argv[])
{
    DIR *dp;
    struct dirent *dirp;

    if(argc != 2)
    {
        printf("usage error \n");
        exit(1);
    }

    if((dp = opendir(argv[1])) == NULL)
        printf("can't open %s",argv[1]);
    while((dirp = readdir(dp)) != NULL)
        printf("%s \n",dirp->d_name);
    closedir(dp);

//    QApplication a(argc, argv);
//    Widget w;
//    w.show();
    
//    return a.exec();
}
```

**QT 做界面，加载c语言自己编译的动态库**
<http://blog.csdn.net/huang_jinjin/article/details/7699942> 

**QT调用库的两种方法**
这里假如需要调用库文件/usr/lib/libhello.so的函数void say();
1. 在pro文件里加入`LIBS += -L/usr/lib/ -lhello`(如果库文件放在/usr/lib ,/lib其实不用加这句);
在头文件里加入：
```
extern "C" {
    void say();
}
```
然后在程序里就可以使用say()函数了    
2. 使用QLibrary类
```
    #include <QLibrary>

    QLibrary lib("libhello.so");
    if(lib.load())
    {
        typedef void (*sayfun)();
        sayfun say = (sayfun)lib.resolve("say");
        if(say)
        {
            say();
        }
        lib.unload();
    }
    else
    {
        qDebug() << "load error.";
    }
```

**QT界面美化**
<http://blog.csdn.net/stoneboy100200/article/details/9356979> 
<http://blog.sina.com.cn/s/blog_618a9b97010112rh.html> 

**颜色收集**
rgb(85, 170, 255);
rgb(167, 205, 255);

**创建一个在qt designer可以用的widget，参考qt例子custom widget plugin example**
**特别注意在plugin里手动make：sudo make**，因为需要将xxxplugin.so拷贝到/usr/lib/i386-linux-gnu/qt4/plugins/designer/,而这里需要管理员权限.
在调用plugin的pro文件里需要加入库目录及需要的库文件:
```
LIBS += -L$$[QT_INSTALL_PLUGINS]/designer -liconEditorPlugin
```

**qt超强精美绘图控件 - QCustomPlot一览  **
<http://blog.163.com/qimo601@126/blog/static/15822093201412642222245/>
<http://blog.sina.com.cn/s/blog_8eac0d020101hd2a.html> 

**使用Plugin开发子窗体**
步骤：
- 项目文件pro:

```
TEMPLATE      = lib
CONFIG       += plugin release
TARGET = formConfigure
DESTDIR = ../../bin/form/

#一定要引用cformcusto.h和cformcustom.cpp
HEADERS += \
    ../FormCustom/iformcustom.h \
    ../FormCustom/cformcustom.h \
    cformconfigure.h

SOURCES += \
    ../FormCustom/cformcustom.cpp \
    cformconfigure.cpp
```
- 建立一个Qt设计师界面类

- 头文件

```
#include "../FormCustom/cformcustom.h"
```
继承CFormCustom
```
class CFormOscillograph : public CFormCustom
```
- 按需求重载基类的方法
- cpp文件

```
#include "qplugin.h"
    ...
    
 Q_EXPORT_PLUGIN2("formConfigure",CFormConfigure)

```


注意：
1. 在转换参数时，需要将const的转为非const，不能用qobject_cast，而是要用static_cast
```
void CFormCustom::setObj(const QObject *o){    
    if(o != m_obj)        
        m_obj = static_cast<UtGlobal *>((QObject *)o);
}
```
2. 不能使用`staticMetaObject.className()`，如：
```
UtGlobal::staticMetaObject.className()；
```
结合上面两点貌似说明在plugin里最好不要用和meta相关的东西。
3. 调用类的方法只能用Meta的方式，如`m_global->property("language")`，`QMetaObject::invokeMethod(m_global,"getLanguage",Q_RETURN_ARG(int,i))`

**捕获键盘事件，其他即使获得焦点的widget也不能处理键盘事件，直到释放捕获**
`grabKeyboard() releaseKeyboard()`
相似的还有鼠标事件

键盘和鼠标时间一般情况下需要在获得焦点时才能处理，但有别的widget使用grabXXXX捕获了键盘或鼠标事件除外。

**设置获取焦点的策略**
`setFocusPolicy()`

**键盘/鼠标事件由子widget优先处理，如果子widget没有处理则交由parent处理**

**判断是否获得了焦点**
`hasFocus()`

在Qt中，事件被封装成一个个对象，所有的事件均继承自抽象类QEvent.  接下来依次谈谈Qt中有谁来产生、分发、接受和处理事件：
1. 谁来产生事件： 最容易想到的是我们的输入设备，比如键盘、鼠标产生的keyPressEvent，keyReleaseEvent，mousePressEvent，mouseReleaseEvent事件（他们被封装成QMouseEvent和QKeyEvent），这些事件来自于底层的操作系统，它们以异步的形式通知Qt事件处理系统，后文会仔细道来。当然Qt自己也会产生很多事件，比如QObject::startTimer()会触发QTimerEvent. 用户的程序可还以自己定制事件。
2. 谁来接受和处理事件：答案是QObject。在Qt的内省机制剖析一文已经介绍QObject 类是整个Qt对象模型的心脏，事件处理机制是QObject三大职责（内存管理、内省(intropection)与事件处理制）之一。任何一个想要接受并处理事件的对象均须继承自QObject，可以选择重载QObject::event()函数或事件的处理权转给父类。
3. 谁来负责分发事件：对于non-GUI的Qt程序，是由QCoreApplication负责将QEvent分发给QObject的子类-Receiver. 对于Qt GUI程序，由QApplication来负责。

**QDataWidgetMapper**将一个数据库记录字段反映到其映射的窗口部件中，同时将窗口部件中所做出的更改反映回数据库，关键是关联一个model和一组widget
**MetaObject**
<http://www.360doc.com/content/13/0313/13/9200790_271228159.shtml>
属性可以通过`Q_OVERRIDE`宏在子类中进行修改。`Q_SETS`宏声明了枚举变量可以进行组合操作，也就是说可以一起读或写。另外一个宏，`Q_CLASSINFO`，用来给类的元对象添加名称/值这样一组数据.

**阻塞窗口，阻止别的窗口获得输入焦点**
`setWindowModality(Qt::ApplicationModal);`

**模版**
<http://www.cnblogs.com/gw811/archive/2012/10/25/2738929.html> 
模板的声明或定义只能在全局，命名空间或类范围内进行。即不能在局部范围，函数内进行，比如不能在main函数中声明或定义一个模板
模板是一种对类型进行参数化的工具；
　　通常有两种形式：函数模板和类模板；
　　函数模板针对仅参数类型不同的函数；
　　类模板针对仅数据成员和成员函数类型不同的类。
　　使用模板的目的就是能够让程序员编写与类型无关的代码。
函数模板的格式：
```
　　　　template <class 形参名，class 形参名，......> 返回类型 函数名(参数列表)
　　　{
　　　　　　函数体
　　　}
```

类模板的格式为：
```
　　　　template<class  形参名，class 形参名，…>   class 类名
　　　　{ ... };
```

**模式窗口**    
`setWindowModality(Qt::ApplicationModal);

**弹出窗口部件**是特殊的顶级窗口部件，它设置了窗口部件标记WType_Popup，例如QPopupMenu窗口部件。当应用程序打开一个弹出窗口部件，所有的事件都被发送给弹出窗口部件。在弹出窗口部件被关闭之前，普通窗口部件和模式对话框都不能被访问。

**closeEvent**
它只对带标题栏(关闭按钮或系统弹出菜单的关闭窗口(Alt+F4))的窗口有效。子窗口（被布局的子窗口，是不会带标题栏的，故重写它是没有意义的）

**重载QDebug()**
```
inline QDebug operator<<(QDebug debug, const Player& player)
{
        debug.nospace() << "Player("
                << player.number << ","
                << player.firstName << ","
                << player.lastName << ")";
        return debug.space();
}
```

**重载操作符<<, >>等需要提供拷贝函数，且拷贝函数里面的赋值变量必须实现重载操作符需要的变量**

**复杂的输入屏蔽和验证**
<http://blog.csdn.net/xgbing/article/details/7776422>
一个很有用的技巧是组合使用`QLineEdit::setInputMask`和`QLineEdit::setValidator`可实现更复杂的输入屏蔽和验证

**QValidator**
抽象类；
两个子类`QIntValidator`和`QDoubleValidator`提供了基本的数字范围检查
另外一个子类`QRegExpValidator`提供了一个使用自定义正则表达式的普通检查。
两个虚函数validate()和fixup()：
子类必须实现validate()
fixup()为提供了可以修改一些用户错误的验证器。默认实现是什么也不做。例如QLineEdit，如果用户按下回车键并且内容并不有效，这种情况下fixup()可以做些事情了。这样就允许一些Invalid字符串也可以被变为Acceptable。


**QcomboBox**
<http://blog.sina.com.cn/s/blog_712038ba0101dgfx.html>
1. 将QcomboBox展开：combox->showPopup();
2. 将QcomboBox收起来：combox->hidePopup();
3. 当QcomboBox展开后焦点位于QcomboBox.view()下
设置行高：
```
    QComboBox combo;
    QPixmap pixmap(1, 50);
    pixmap.fill(Qt::transparent);
    QIcon icon(pixmap);
    combo.setIconSize(QSize(1, 50));
    combo.addItem(icon, "test1");
    combo.addItem(icon, "test2");
    combo.show();
```

获取globalpos以用在move等函数:
```
QPoint p = this->mapToGlobal(this->pos());    
p -= this->pos();
```

**qt隐藏鼠标图标**：

1. 在运行程序的加上参数-nomouse，这样，当前启动的程序就不会出现鼠标光标。
2. 在编译QT库的时候添加编译选项QT_NO_CURSOR，这样cursor相关的代码就不会被编译进去，自然鼠标光标也不会出现在程序中。具体做法是在编译的时候加上-no-feature-CURSOR。据说在编译的时候加-nomouse也可以，但是这样触摸屏也无法点击。
3. 只希望在某个QWidget下不出现鼠标光标，则只要对这个widget调用
  QWidget::setCursor(QCursor(Qt::BlankCursor))，其它的窗口仍将出现鼠标。
4. 在main函数中，实例化了APPLICATION后，调用
  QApplication::setOverrideCursor(Qt::BlankCursor);
5. 任一控件下显示与关闭鼠标
  this->setCursor(Qt::BlankCursor);   //隐藏鼠标
  this->setCursor(Qt::ArrowCursor);  //显示正常鼠标
  this改为需要隐藏鼠标的部件，就可以令当鼠标移动到该部件时候，效果生效。
  以上的都需要动一下鼠标才会消失，不知道不是我没有搞好，下面一启动就可以隐藏起来
6. 调用下面函数：
QWSServer::setCursorVisible(false);这个方法还有待研究，具体怎么加还不是很明白。

**删除容器**
```
QList<QWidget *> list;
qDeleteAll(list);
list.clear;
```

打开外部文件:
```
QDesktopServices ds;
ds.openUrl(QUrl(fileName));

```

打开外部程序:

```
QProcess *p = new Qprocess;
p->start(fileName);

```
**测算程序运行时间**
<http://blog.csdn.net/dreamtdp/article/details/8662377>
 
一般情况下类型要转换为QVariant时需要用`QVariant::fromValue`函数，但是可以在在此类型实现`operator QVariant() const`，此时就不需要用`QVariant::fromValue`函数来转换了：
一般情况:
```
Player player;
object->setProperty("property", QVariant::fromValue(player));
```
现在可以这么做：
```
struct Player{    
    operator QVariant() const    
    {        
        return QVariant::fromValue(*this);    
    }
};

...

Player player;
object->setProperty("property", player);

```

**最后一个一个窗体关闭时不退出应用程序**
`QApplication::setQuitOnLastWindowClosed(false);`

**获得qt的相关路径**
`QLibraryInfo::location(QLibraryInfo::ImportsPath)`
**获取当前语言**
`QLocale::system().name()`


**QListWidget,QStackedWidget的使用**见: config dialog example



*QTableWidget使用**

```

filesTable = new QTableWidget(0, 2);//0行，2列

filesTable->setSelectionBehavior(QAbstractItemView::SelectRows);//选择整行



QStringList labels;

labels << tr("Filename") << tr("Size");

filesTable->setHorizontalHeaderLabels(labels);//设置表头

filesTable->horizontalHeader()->setResizeMode(0, QHeaderView::Stretch);//横向排列方式

filesTable->verticalHeader()->hide();//隐藏列表头

filesTable->setShowGrid(false);//不现实表格线

```

**打开一个存在的目录**

```

QString directory = QFileDialog::getExistingDirectory(this, tr("Find Files"), QDir::currentPath())

```

**显示进度**`QProgressDialog`

**将QStringList的所有项目以指定分隔符返回字符串**`QString QStringList::join ( const QString &separator ) const`，`QString::split()`将以指定分隔符分隔的字符串转换为QStringList

**允许drop事件**`QWidget::setAcceptDrops(true);`

**获取光标位置的控件**

```

void DragWidget::mousePressEvent(QMouseEvent *event) 

{    

    QLabel *child = static_cast<QLabel*>(childAt(event->pos()));

    ...

}

```

**流化读写QIODevice或QByteArray**`QDataStream()`

**初始化随机数**`qsrand(QTime(0,0,0).secsTo(QTime::currentTime()));`

**设置QTableView的高度，宽度策略**

```

tv->setRowHeight(0,50);//行高

tv->setColumnWidth(0,130);//列宽

...

tv->horizontalHeader()->setResizeMode(QHeaderView::Stretch);//宽度填满parent    

tv->verticalHeader()->setResizeMode(QHeaderView::ResizeToContents);//根据内容调整高度

```

**QTableWidget的设置**<http://www.cnblogs.com/zhoug2020/p/3789076.html>

<http://blog.sina.com.cn/s/blog_9d16de8101010myf.html>

**Qt浅谈之三十六仿360设置中心**<http://blog.csdn.net/taiyang1987912/article/details/50249243>

**自动完成**`QCompleter `

**qt 去掉光标显示的方法**<http://blog.sina.com.cn/s/blog_5106eff10100s9l6.html>

**颜色搭配:**<http://blog.voc.com.cn/blog_showone_type_blog_id_746791_p_1.html>

**StyleSheet**



**使用gdb** <http://wenku.baidu.com/link?url=4CsxFpnxZFv9te8cv2cSy43GKTDzSAfQukrCg1th71SDMjNODvWauqGHXgMUXOzUorFAQZODOhzCYcdSDLwmw9uSXC1yZuDgMWgdfj1lKAi>                                                            

```

gcc -g -rdynamic test1.c

gdb a.out

```

按r运行



**stylesheet**

<http://blog.csdn.net/liang890319/article/details/7098439>

<http://no001.blog.51cto.com/1142339/281736/>

<http://no001.blog.51cto.com/1142339/281760/>

<http://www.cnblogs.com/davesla/archive/2011/01/30/1947928.html>

<http://blog.csdn.net/knowledgeapple/article/details/7991833>



**QpushButton上避免焦点虚框的曲折路**

<http://blog.hehehehehe.cn/a/9749.htm>

**Qt异形按钮的创建**

<http://blog.csdn.net/a812073479/article/details/46379333>

**Qt StyleShett 实现 Metro 风格之 - QPushButton**

<http://my.oschina.net/upday7/blog/109597>

**Qt中通过设置位图掩码生成异形控件**

<http://www.linuxidc.com/Linux/2013-04/83225.htm>

**Qt 字体大小的计算**

<http://blog.csdn.net/liuqz2009/article/details/7208931>

**Qt Widgets——抽象按钮及其继承类**

<http://www.cnblogs.com/newstart/p/4476094.html>



**always on top form总是显示在最上面**

```

    OutBoardBox * box = new OutBoardBox;
    Qt::WindowFlags flags = box->windowFlags();
    flags |= Qt::WindowStaysOnTopHint;//always on top
    flags |= Qt::FramelessWindowHint;//not hint
    box->setWindowFlags(flags);
    box->setAttribute(Qt::WA_DeleteOnClose);
    box->show();
```

<https://www.zhihu.com/question/23374078>
**UTF-8和UNICODE，最后简单总结一下：**
1.中国人民通过对 ASCII 编码的中文扩充改造，产生了 GB2312 编码，可以表示6000多个常用汉字。
2.汉字实在是太多了，包括繁体和各种字符，于是产生了 GBK 编码，它包括了 GB2312 中的编码，同时扩充了很多。
3.中国是个多民族国家，各个民族几乎都有自己独立的语言系统，为了表示那些字符，继续把 GBK 编码扩充为 GB18030 编码。
4.每个国家都像中国一样，把自己的语言编码，于是出现了各种各样的编码，如果你不安装相应的编码，就无法解释相应编码想表达的内容。终于，有个叫 ISO 的组织看不下去了。他们一起创造了一种编码 UNICODE ，这种编码非常大，大到可以容纳世界上任何一个文字和标志。所以只要电脑上有 UNICODE 这种编码系统，无论是全球哪种文字，只需要保存文件的时候，保存成 UNICODE 编码就可以被其他电脑正常解释。UNICODE 在网络传输中，出现了两个标准 UTF-8 和 UTF-16，分别每次传输 8个位和 16个位。于是就会有人产生疑问，UTF-8 既然能保存那么多文字、符号，为什么国内还有这么多使用 GBK 等编码的人？因为 UTF-8 等编码体积比较大，占电脑空间比较多，如果面向的使用人群绝大部分都是中国人，用 GBK 等编码也可以。

**发布windows程序注意事项**
1. 在没有安装相关包的情况下，需要将msvcp100.dll和msvcr100.dll拷贝到system32目录(x86)或SysWOW64目录(x64).
2. 将QtCore4.dll和QtGui4.dll拷贝到安装目录
3. 如果出现无法显示图标、图片等情况，解决办法：在安装目录新建文件夹并命名为plugins，然后将C:\Qt\4.8.6_VS2010\plugins\imageformats文件夹拷贝到新建的文件夹里，在main.cpp里添加`QApplication::addLibraryPath(a.applicationDirPath() + "/plugins");`
4. 关于UAC的解决办法之一：在pro文件里添加`QMAKE_LFLAGS += /MANIFESTUAC:"level='requireAdministrator'uiAccess='false'"`

5. 项目文件添加 `LIBS += -luser32`

**添加外部库文件**

<http://blog.csdn.net/z609932088/article/details/50902302>



**Qt4项目升级到Qt5可能遇到的问题**

<http://blog.csdn.net/zhenwo123/article/details/17578579>



**QT5的exe的发布**

<https://www.cnblogs.com/Mysterious/p/5675001.html>

windeployqt



**不规则窗体**

http://blog.csdn.net/xuancailinggan/article/details/50563619



**平滑移动窗体**

```

pa = new QPropertyAnimation(this,"pos");

pa->setDuration(1000);

  pa->setStartValue(QPoint(0,0));

  pa->setEndValue(QPoint(200,0));

  pa->start();

```

**installshared获取安装文件位置**

http://blog.csdn.net/lixiuzhu0/article/details/43421781

```

function InstallUSBDriver(hMSI)

    // To Do:  Declare local variables.      

    STRING driverPath;      

    STRING setupDir[256];  //获取安装程序Setup.exe自身所在的路径存放的变量    

    NUMBER nBuffer; // 数组buffer最大值

begin  

    nBuffer =256;      

    MsiGetProperty(ISMSI_HANDLE,"SETUPEXEDIR",setupDir,nBuffer);//获取SETUPEXEDIR的函数        



    if(SYSINFO.bIsWow64) then                            

        driverPath = setupDir ^ "\\Driver\\x64.exe" ;

    else                    

        driverPath = setupDir ^ "\\Driver\\x86.exe" ;

    endif;      

      

    LaunchAppAndWait(driverPath,"",WAIT);      

end;

```

**阿里巴巴矢量图标库**

http://iconfont.cn



**输入自动完成**

```

    QStringList wordList;

    wordList << "alpha" << "omega" << "omicron" << "zeta";    

    QCompleter *completer = new QCompleter(wordList);

    completer->setCaseSensitivity(Qt::CaseInsensitive);

    ui->lineEdit->setCompleter(completer);

```



**pri文件**

http://blog.csdn.net/ljt350740378/article/details/50484246



**Qt编写自定义控件插件路过的坑及注意事项**

https://www.cnblogs.com/feiyangqingyun/p/6182320.html 

Qt自定义插件注意事项：

1：每个Qt库bin目录的designer可执行文件都是和该库同一个编译器编译的，可用，如果想要集成到Qt Creator中，则需要注意版本，一般在windows上的Qt Creator版本是MSVC的，则需要对应的Qt库也是MSVC编译的，库版本和编译器版本必须保持一致才能是顺利集成到Qt Creator的重要前提。

2：自定义控件的名称不能小写，否则拖过去的控件自动生成的默认名称和类名一样，会编译通不过。这个问题坑了我很久，造成自动生成的UI代码保存，一直没有怀疑，后面才发现自动生成的代码类名和实例名称一样，冲突导致的。

3：自定义控件类头文件引入，Qt5.7以下版本为#include <QtDesigner/QDesignerExportWidget> 以上版本为#include <QtUiPlugin/QDesignerExportWidget>

4：类名前必须加入 QDESIGNER_WIDGET_EXPORT 宏。否则集成到Qt Creator 中编译会报错。不加的话可以在设计器中加载，但是编译会报错。

5：如果将生成好的dll文件放到Qt库目录下的 plugins\designer 下，可以在 designer 中看到。放到Qt Creator下的 bin\plugins\designer 则可以集成到Qt Creator中。

6：将自定义控件的头文件、dll文件、lib（mingw编译器为.a）文件复制出来，放到include（可自己随便命名，我这里习惯用include）目录，将include目录放到项目的源码文件下，在使用了自定义控件的项目的pro文件中，增加两行 INCLUDEPATH += $$PWD/include  LIBS += $$PWD/include/***.lib(mingw编译器为.a) ，这样可以正常编译，但是编译完成后不能运行，还需要将 对应自定义控件的dll文件复制到可执行文件同一目录即可，至此大功告成。

番外话：大部分文章介绍都是将对应的库文件和头文件放到Qt安装目录对应文件夹下，为什么这里要放到一个include目录，随着项目一起呢？个人是这么理解的，随项目一起，每次都可以很方便的将运行库文件复制到可执行文件同一目录，而不会忘记从Qt库对应目录找该运行库。而且发布代码的时候也可以有个很好的参考。

7：官网提供的Qt Creator版本基本上是MSVC版本，如果需要在mingw的Qt库对应的Qt Creator中集成自定义控件，需要自己用对应的Qt库编译Qt Creator源码。



**条件编译**

```

CONFIG(debug, debug|release) {

LIBS += -L../lib1 -lhellod

} else {

LIBS += -L../lib2 -lhello

}

```



**浮点数判断为0或者相等**

http://blog.csdn.net/zhaoforyou/article/details/53748726

float精确到小数点后6位

double精确到小数点后15位

所以，也就是说，如果一个float小于0.000001，我们就不知道是否为有效的了，也可以认为近似为0了。

同理一个double的有效范围为1e-15，小于1e-15的double类型我们就可以认为近似为0

```

if(abs(v) < 1.0e-15){//判断double value是否为0

}



if(fabs(f2-f3) < 1e-6){//判断两个float是否相等

}



```



**枚举类型和字符串的转换**

https://www.cnblogs.com/dongc/p/5630444.html

```

enum PortType{USB,LAN,RS232};

Q_FLAG(PortType)



...



QMetaEnum me = QMetaEnum::fromType<DlgDevChoose::PortType>();

DlgDevChoose::PortType al = ( DlgDevChoose::PortType)me.keyToValue("DlgDevChoose::LAN");

QString s = QString::fromLatin1(me.valueToKey(DlgDevChoose::RS232));

cdebug << al << s;

```



**QTableView中使用代码来选中连续多行、间隔多行并移动后保留选中**

https://blog.csdn.net/xbnlkdbxl/article/details/52411833



**QToolButton菜单立即弹出 QToolBar QToolButton QAction **

```

QToolButton * btn =  qobject_cast<QToolButton *>(ui->mainToolBar->widgetForAction(ui->actionStart));

    if(btn)

        btn->setPopupMode(QToolButton::InstantPopup);

```

**从5.8版本开始，已不再支持Windows XP**

[Deploying Qt on XP and getting “not a valid Win32 application”](http://www.tripleboot.org/?p=423)

[使用Qt5.7.0 VS2015版本生成兼容XP的可执行程序](https://blog.csdn.net/caoshangpa/article/details/53690612)

[Qt 5.8 released](http://blog.qt.io/blog/2017/01/23/qt-5-8-released/)



**Mingw UAC**

https://stackoverflow.com/questions/7744410/how-to-execute-an-app-without-elevation

1. 增加一个manifest.xml文件

```

<?xml version="1.0" encoding="UTF-8" standalone="yes"?>

<assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">

    <trustInfo xmlns="urn:schemas-microsoft-com:asm.v2">

        <security>

            <requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">

                <requestedExecutionLevel level="requireAdministrator" uiAccess="false" />

            </requestedPrivileges>

        </security>

    </trustInfo>

</assembly>

```

2. UT8803.rc文件

```

1 24 DISCARDABLE manifest.xml

IDI_ICON1              ICON    DISCARDABLE    "image/app.ico"



```

3.  pro文件`RC_FILE = UT8803.rc`



[**在qt5中使用中文、Unicode**](https://blog.csdn.net/jh1513/article/details/52331973)

在字符串前加`QStringLiteral`



[**QWaitCondition 的正确使用方法**](https://blog.csdn.net/flyoxs/article/details/54617342)

**为QToolButton提供弹出菜单**
```
QMenu * m = new QMenu;
m->addAction(ui->actionStartSelections);
m->addAction(ui->actionStartWithcurrent);    
m->addAction(ui->actionStartAll);
ui->actionStart->setMenu(m);
QToolButton * btn =  qobject_cast<QToolButton *>(ui->mainToolBar->widgetForAction(ui->actionStart));
    if(btn)
        btn->setPopupMode(QToolButton::InstantPopup);
```

**statusbar添加widget**
```
m_progressBar = new QProgressBar;
ui->statusBar->addPermanentWidget(m_progressBar,1);
m_progressBar->setFormat("%v/%m");
```

**删掉CentralWidget**
```
QWidget * p = takeCentralWidget();
if(p)
  delete p;
//setDockNestingEnabled(true);//允许嵌套dock
```

**退出程序**
`QTimer::singleShot(0,qApp,QApplication::quit);`


[**qmake 乱乱乱谈(一)**](https://blog.csdn.net/dbzhang800/article/details/6758204)


**绘图**
https://blog.csdn.net/guodengh/article/details/7791300

QPaintDevice是所有绘图设备的基类，其子类有QImage,QPixmap等。
QPainter关联到一个绘图设备，可以用来绘制基本图形
QWidget是QObject和QPaintDevice的子类

QPixmap和QImage：
QPixmap主要是用于绘图，针对屏幕显示而最佳化设计，QImage主要是为图像I/O、图片访问和像素修改而设计的。
QPixmap依赖于所在的平台的绘图引擎，故例如反锯齿等一些效果在不同的平台上可能会有不同的显示效果，QImage使用Qt自身的绘图引擎，可在不同平台上具有相同的显示效果
由于QImage是独立于硬件的，也是一种QPaintDevice，因此我们可以在另一个线程中对其进行绘制，而不需要在GUI线程中处理，使用这一方式可以很大幅度提高UI响应速度
QImage可通过setPixpel()和pixel()等方法直接存取指定的像素

当图片较大时，我们可以先通过QImage将图片加载进来，然后把图片缩放成需要的尺寸，最后转换成QPixmap 进行显示。   
```
QImage image; 
image.load( ":/pics/earth.png" );   
QPainter painter(this); 
QPixmap pixmapToShow = QPixmap::fromImage( image.scaled(size(), Qt::KeepAspectRatio) ); 
painter.drawPixmap(0,0, pixmapToShow);
```       
[**QT开发（十四）——QT绘图系统**](http://blog.51cto.com/9291927/1868755)
坐标变换`QMatrix`
获得字体`QFontDatabase`
默认为双缓冲绘图，可以使用`widget->setAttribute(Qt::WA_PaintOnScreen);`关闭双缓冲

**设置qwidget的透明度**`setWindowOpacity(0.5);`
**用来保存临时图像，提高效率**`QPixmapCache`


**QByteArray和double的相互转换**
https://blog.csdn.net/maoxue2008/article/details/78142893
```
QByteArray arry;
double f = 123.456;
arry.append(reinterpret_cast<const char*>(&f),sizeof(double));
double ff = *reinterpret_cast<double*>(arry.data());
cdebug << ff;
```

### Main Window
You create MDI applications in Qt by using a **QMdiArea** as the central widget.
```
QMainWindow *mainWindow = new QMainWindow;
mainWindow->setCentralWidget(mdiArea);
```

Subwindows in QMdiArea are instances of **QMdiSubWindow**.
```
QMdiArea mdiArea;
QMdiSubWindow *subWindow1 = new QMdiSubWindow;
subWindow1->setWidget(internalWidget1);
subWindow1->setAttribute(Qt::WA_DeleteOnClose);
mdiArea.addSubWindow(subWindow1);

QMdiSubWindow *subWindow2 =
	mdiArea.addSubWindow(internalWidget2);
```

### Qt Graphics View Framework
[Qt Graphics View Framework 图形视图框架](https://blog.csdn.net/xuguangsoft/article/details/8578042)
[Qt图形视图框架（The QGraphics View Framework）](https://blog.csdn.net/abcvincent/article/details/71773700)
它包含三个大类：**QGraphicsItem** 项类（或者叫做图元类），**QGraphicsScene** 场景类，和 **QGraphicsView** 视图类。
QGraphicsItem是在场景中的**图形项**，QGraphicsScene相当于**容器**包含和管理QGraphicsItem。项类通过QGraphicsScene::addItem()，（QGraphicsScene::add()）被加入到Scene。QGraphicsView是个**视图窗体部件**。我们可以将scene绑定到view。并且一个scene可以被绑定到**多个**view中。
QGraphicsScene是一个图形项的集合，它包括**三层**：*背景层background layer*, *项层item layer* 和*前景层foreground laye*r。可以通过重新实现`drawBackground()` ,`drawForeground()` 来控制背景层和前景层。
这个体系使用**三种不同**的坐标系统——*项坐标，场景坐标和视口坐标*（Item coordinates, scene coordinates, and view coordinates.）。
`QGraphicsScene::setSceneRect()`设置scene的边界
`QGraphicsScene::render()`将场景的某一部分展示到一个绘画设备中
视图接收来自键盘和鼠标的输入事件，并在发送事件给可视化的场景之前，将它们转化为**场景事件**（将坐标转化为适当的场景坐标）。
`qgraphicsitem_cast`

## Chart
Qt有一套自己的chart系统，称为"**Qt Charts**",构建于"Qt Graphics View Framework"之上.

**一般情况**
```
QSplineSeries *series = new  QSplineSeries;
series->setName("spline");
series->append(10, 5);
*series << QPointF(11, 1) << QPointF(13, 3) << QPointF(17, 6) << QPointF(18, 3) << QPointF(20, 2);
//...
QChart *chart = new QChart();
chart->legend()->hide();
chart->addSeries(series);
chart->setTitle("Simple spline chart example");
//...
chart->createDefaultAxes();
chart->axisY()->setRange(0, 10);
//...
QChartView *chartView = new QChartView(chart);
chartView->setRenderHint(QPainter::Antialiasing);
//...
QMainWindow window;
window.setCentralWidget(chartView);
//...
```

**X轴为时间**
```
QDateTime xValue = QDateTime::currentDateTime();
qreal yValue;
for(int i=0;i<10;i++){
    yValue = qrand()%11;
    qDebug() << yValue;
   series->append(xValue.toMSecsSinceEpoch(), yValue);
   xValue = xValue.addSecs(1);
}
//...
QDateTimeAxis * axisX = new QDateTimeAxis();
axisX->setFormat("yyyy-MM-dd h:mm:ss");
chart->setAxisX(axisX,series);

chart->setAxisY(new QValueAxis);
chart->axisY()->setRange(0, 10);
```

**允许捕获鼠标经过事件**
```
 m_chart->setAcceptHoverEvents(true);
```

**抗锯齿**
```
setRenderHint(QPainter::Antialiasing);
```

**将chart的坐标转换为值**
```
m_chart->mapToValue(event->pos()).x())
```

## GIT

#### Git官方教程
https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80
http://www.runoob.com/git/git-tutorial.html
https://blog.csdn.net/u013510614/article/details/50588446

你的本地仓库由 git 维护的三棵“树”组成。第一个是你的 工作目录，它持有实际文件；第二个是 暂存区（Index），它像个缓存区域，临时保存你的改动；最后是 HEAD，它指向你最后一次提交的结果
![](http://www.runoob.com/manual/git-guide/img/trees.png)
![](http://ww2.sinaimg.cn/mw690/44894cbbgw1euigokxcr8j20ci0ffgo8.jpg)
![](http://ww1.sinaimg.cn/mw690/44894cbbgw1euigc99z8wj20e40bpjsm.jpg)

http://www.360doc.com/content/12/0419/17/1016783_204960412.shtml
https://blog.csdn.net/qq_32452623/article/details/78417609
[git暂存区[重要]](https://blog.csdn.net/daguanjia11/article/details/73065841)

#### Git简单教程:
##### 一般流程
1. 设置身份，只需要设置一次
git config --global user.name "coder-pig" 
git congif --global user.email "779878443@qq.com"
2. 建立本地仓库
    git init
3. 添加文件到暂存区
    git add *.java
4. 排除文件（夹） 
    在.git同一级目录下创建一个名为.gitignore的文件，在.gitignore里添加不需要管理的文件，如/gen/,/bing/,project.properties
5. 提交
    git commit --m " initial project version"
6. 查看提交日志
    git log
7. 版本退回
	- 方法1： 退回到当前版本git reset --hard HEAD，退回到上一个版本 git reset --hard HEAD^，以此类推
	- 方法2： 使用版本号的前7位git reset --hard d9a5e13       

#### 其他
查看操作记录git reflog，在覆盖了新版本时可以查看新版本号

按我的认识，更清楚且通俗的解释就是：git维护的代码分成三部分，“当前工作目录”<->“index file”<->git仓库。git commit会将index file中的改变写到git仓库；git add会将“当前工作目录”的改变写到“index file”；“commit -a”则会直接将“当前工作目录”的改动同时写到“index file”和“git仓库”。

在用cmd时提示"more?"用HEAD~x或"HEAD^ "或HEAD^ ^ 替换HEAD^^。建议不用cmd而用bash

以一行图表方式显示log:`git log --graph --oneline`
`git commit -m` 命令写多行注释：使用bash而不是cmd，`git commit -m '`,在写完注释后以'结束就可以了
`git log --stat 1a410e` 查看sha1为1a410e的commit对象的记录

git reset:
1. `git reset --soft HEAD` 工作区不变，stage不会变，本地仓库回滚到指定提交
2. `git reset --mixed HEAD`	工作区不变，指定提交覆盖stage，本地仓库回滚到指定提交
3. `git reset --hard HEAD` 工作区被指定提交覆盖，stage被指定提交覆盖，本地仓库回滚到指定提交

`git checkout .` 工作区被stage覆盖
`git checkout HEAD .` 工作区被HEAD覆盖,暂存区被HEAD覆盖,但是本地仓库并不回滚，注意和git reset --hard的区别
`git commit -a -m "v3"` 直接将工作目录commit。千万注意，-a不会造成新文件被提交，只能修改。
`git rm --cached x.x` 将文件移除库，变为untracked状态
`git rm -r --cached x.x` 将文件夹移除库，变为untracked状态

[关于 git reset 命令几个常用参数的理解](https://blog.csdn.net/hbwindy/article/details/51519999 )
[git reset的三种模式](https://blog.csdn.net/catchertherye/article/details/49721697)

#### 远程仓库
[Git远程仓库的添加及克隆](https://blog.csdn.net/shufac/article/details/51766104)
##### 建立远程仓库
1. 创建SSH Key.`$ ssh-keygen -t rsa -C"youremail@example.com" `,
2. 登陆github，打开“Account settings”，“SSH Keys”页面：然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：
3. 添加远程仓库。` $ git remote add origin git@github.com/Kevinfa2016/MyGitTest.git `
4. 把本地库的所有内容推送到远程库上：` $ git push -u /f/Git/MyGitTest `
5. 从现在起，只要本地作了提交，就可以通过命令： ` $ git push /f/GitMyWarehouse master `

切换远程仓库 `git remote set-url origin URL`

##### [**远程仓库大致流程是：**](https://www.jianshu.com/p/8d26730386f3)这个完全正确
1. 在github上创建项目
2. 使用git clone https://github.com/xxxxxxx/xxxxx.git克隆到本地
3. 编辑项目
4. git add . （将改动添加到暂存区）
5. git commit -m "提交说明"
6. git push origin master 将本地更改推送到远程master分支。

这样你就完成了向远程仓库的推送。

如果在github的remote上已经有了文件，会出现错误。此时应当先pull一下，即：
git pull origin master
然后再进行：
git push origin master

gitee可以使用private仓库
git branch --set-upstream-to=origin/<branch> dev
再新建立库时，如果合并库的时候试过push或pull失败，尝试用下面的代码:
git pull origin master --allow-unrelated-histories
git push --set-upstream origin master















