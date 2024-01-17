# QT知识点

## 知识点一/控件

###
    信号槽的写法:
        1.写法1
            connect(button, &QPushButton::clicked, this, &MyWidget::showMessage);

        2. 写法2,lambda写法
            connect(button, &QPushButton::clicked, [=](){ 
            QMessageBox::information(nullptr, "消息", "按钮被点击了！"); 
        });

### 窗口布局
1.  窗口布局
    |名称|使用方法|
    |------|------|
    |QLayout      |所有布局管理器的基类,提供了布局管理器的基本功能|
    |QHBoxLayout  |水平布局|
    |QVBoxLayout  |垂直布局|
    |QGridLayout  |网格布局|

2.  基础控件
    |名称|使用方法|
    |-----|------|
    |QWidget      |所有窗口部件的基类，提供了窗口部件的基本功能（尺寸、位置、标题...）|
    |QMainWindow  |主窗口类，提供了主窗口的基本功能（菜单栏、工具栏、状态栏...）|
    |QLabel       |标签类，用于显示文本或图像|
    |QPushButton  |按钮类，用于响应用户的点击|
    |QLineEdit    |单行文本输入框|
    |QTextEdit    |多行文本输入框|
    |QMessageBox  |消息框|
    |QComboBox    |下拉列表类，用于从列表中选择一个选项|
    |QCheckBox    |复选框类，用于从多个选项中选择一个或多个|
    |QRadioButton |单选按钮类，用于从多个选项中选择一个|
    |QSlider      |滑块类，用于从一个范围中选择一个值|
    |QProgressBar |进度条类，用于显示任务的进度|
    |QMenuBar     |菜单栏|
    |QMenu        |菜单项|
    |QAction      |菜单子选项|
    |QScrollArea  |滑动窗口|
    |QStackedWidget|堆叠窗口|
    |QPainter     |绘图|
    |QTimer       |定时器|
    |QTransform   |图形变换的一个类|

### 一些Qt函数

    1. toUpper(),小写转换大写
    
    2. toInt(),将字符串数字转换为整型数字
   
    3. QString的字符串截取:
        QString QString::mid(int position, int n = -1)
        position：指定截取字符串的起始位置(postion超出字符串长度时，返回null字符 )
        n：指定截取字符串长度(自postion开始的可用字符串小于n，or n == -1，返回自position开始的全部字符串)

    4. isEmpty(),判断QString是否为空
    

### 一些QT的方法

    _input.setText(text);用来设置文本框内容


    QString类提供了两个计算字符串长度的方法,分别是 length() 和 size();
        1.length() 方法
            length() 方法返回 QString 中字符的数量,这个方法的时间复杂度是 O(n),其中 n 是字符串的长度,

        2.size() 方法
            size() 方法返回 QString 所占用的字节总数,由于 QString 中可能包含 Unicode 字符,因此它可能占用多个字节
    

    单行文本QLineEdit,获得方式text.text()

    多行文本QTextEdit,获得方式text.toPlainText()

    arg(i) 是 QString 类的一个方法，它会把括号内的参数 i 替换到格式化字符串中的 %1 处。

### String 和 QString 的互相转换

#### 类型的转换
    QString 转换为 String
        QString qstr;
        String str = qstr.toStdString(); 

    String 转换为 QString
        String str;
        QString qstr = QString::fromStdString(str);

    int 转换为 QString类型
        QString str = QString::number(123);
    
    
#### 事件
    _button_up.setAutoRepeat(true); //启用长按
    _button_up.setAutoRepeatDelay(400);//触发长按的时间
    _button_up.setAutoRepeatInterval(50);//长按时click信号间隔

### 使用QT的一些y用法
    1. 设置中央部件
        setCentralWidget();
    2. 应用布局到QWidget,只设置一次
        setLayout();
    2. 添加控件
        addWidget();
    3. 添加布局
        addLayout();
    4. 设置文本内容
        setText("hello");
    5. 设置图片
        setPixmap(QPixmap("img/racoon.png"));
    6. 设置居中方式
        setAlignment(Qt::AlignCenter);
    7. 设置对象为只读
        setReadOnly(true);
    8. 设置拉伸因子
        addStretch(1);
    9. 弹出消息框
        information(this, "警告", "密码超过8位");
    10. 绑定加入到组
        addButton(&_button1);
    11. 关闭多选组的排它性
        setExclusive(false);
    12. 设置菜单栏
        setMenuBar(_menubar);
    13. 添加菜单项到菜单栏
        addMenu(_file);
    14. 添加菜单子选项到菜单项
        addAction(_new);
    15. 添加快捷键
        setShortcut(QKeySequence("Ctrl+N"));
    16. 弹出对话框
        QString qstr = QInputDialog::getText(this, "文件名", "新建文件名");
    17. 弹出选择文件框
        QString runPath = QCoreApplication::applicationDirPath();//获取项目的根路径
        QString file_name = QFileDialog::getOpenFileName(
            this,QStringLiteral("选择文件"),runPath,"Text Files(*.txt)",
            nullptr,QFileDialog::DontResolveSymlinks);
    18. 添加列表项
        addItem("1");
    19. 设置下拉列表文本
        currentText();
    20. 设置下拉框
        setEditable(true);
    21. 设置下拉框模糊搜索
        setCompleter(new QCompleter(_comboBox.model()));
    22. 自动补全器,关联输入框的自动补全功能
        QCompleter();
    23. 设置进度条范围
        setRange(0,100);
    24. 设置进度条值
        setValue(50);
    25. 获取进度条的当前值
        _p.value();
    26. 设置滑动条的滑动方向
        setOrientation(Qt::Horizontal);
    27. 设置控件的具体位置
        setGeometry(x,y,whigedt,hight);
    28. 添加的父对象
        setParent(&_centralWidget);
    29. 图片等比例缩放
        pixmap = pixmap.scaled(QSize(200, 200), Qt::KeepAspectRatio, Qt::SmoothTransformation);
    30. 标签的移动距离
        move(x,y);
    31. 设置当前堆叠窗口页面
        setCurrentIndex(1);
    32. 设置窗口宽高,不可调整
        setFixedSize(960, 540);
    33. 设置窗口宽高,可动态调整
        resize(400, 300);
    34. 画笔属性
        QPainter::setPen(
            QPen(const QColor &color,                   //颜色
            qreal width,                                //粗细
            Qt::PenStyle style,                         //样式
            Qt::PenCapStyle capStyle = Qt::SquareCap,   //线条末端形状
            Qt::PenJoinStyle joinStyle = Qt::BevelJoin, //两条线段相交时连接处的形状,默认为斜接
            qreal miterLimit = 0.0))                    //斜接限值,仅当joinStyle为Qt::MiterJoin时有效
    35. 笔刷属性
        setBrush(QColor(_color_B_str), Qt::SolidPattern);
            QBrush(const QColor &color);使用颜色构造：创建一个纯色的画刷。
            QBrush(Qt::BrushStyle style);使用样式构造
            QBrush(const QPixmap &pixmap);创建一个预定义样式的画刷，如斜线、点状、网格等
            QBrush(const QImage &image);使用图片或图像构造
            QBrush(const QBrush &other);创建基于像素图或者图像的纹理画刷
    36. 绘制A端点到B端点的一条线
        drawLine(QPoint(A_X, A_Y), QPoint(B_X, B_Y));
    37. 绘制矩形
        painter.drawRect(100, 100, 400, 400);
    38. 绘制椭圆
        painter.drawEllipse(100, 100, 400, 400);
    39. 绘制多边形
        五角星
            points.push_back(QPoint(200, 50));
            points.push_back(QPoint(250, 200));
            points.push_back(QPoint(400, 200));
            points.push_back(QPoint(300, 300));
            points.push_back(QPoint(350, 450));
            points.push_back(QPoint(200, 350));
            points.push_back(QPoint(50, 450));
            points.push_back(QPoint(100, 300));
            points.push_back(QPoint(0, 200));
            points.push_back(QPoint(150, 200));
            painter.drawPolygon(points);
    40. 定时器触发时间，ms为单位
        start(5);
    41. 创建一个对象,调用QWidget或其派生类的rect()方法,返回当前控件的有效绘制区域(即整个控件的边界框),并填充颜色
        painter.fillRect(rect(), Qt::gray);
    42. QTransform创建一个矩形变换类对象,提供矩阵变换操作
        QTransform transform1;
            translate(dx, dy)：沿x和y轴平移指定的距离。
            rotate(angle)：以原点为中心顺时针旋转指定角度。
            scale(sx, sy)：在x和y方向上分别按比例缩放。
            shear(shx, shy)：沿x轴和y轴进行斜切变换。
	43. 重载的事件处理函数，可以通过定时器和变量的改变触发，也可以显式的调用update()刷新屏幕
		paintEvent();
	44. mousePressEvent(QMouseEvent *event)是Qt中的一个鼠标事件处理函数