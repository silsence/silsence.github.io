# C++知识点

## 知识点一

### 数据类型
    
    
    整型:	    int
    浮点型:	    float
    双浮点型:   double
    字符型:	    char
    布尔型:	    bool
    无类型:	    void

    c++四种初始化的方式:

    int x=0;
    int x={0};//{}列表初始化方式可能会丢失数据
    int x{0};
    int x(0);

45.
46. 如果使用"="初始化，那么执行的就是拷贝初始化
    string s=(10,'c')等价于:
    string temp(10,'c')；
    string s=trmp;


### 存储类

    auto:自动推断被声明的变量的类型
        用auto声明的变量必须初始化(auto是根据后面的值来推测这个变量的类型，如果后面没有值，自然会报错)
            auto f=3.14;//推断为double类型

    static:指示编译器在程序的生命周期内保持局部变量的存在
        修饰局部变量:
            使用 static 修饰局部变量可以在函数调用之间保持局部变量的值
        
        修饰全局变量:
            使用 static 修饰全局变量时，会使变量的作用域限制在声明它的文件内
        
        修饰类变量:
            使用 static 用在类数据成员上时，会导致仅有一个该成员的副本被类的所有对象共享
    
    extern:声明一个变量加上关键字extern
        是声明和定义的结合,它告诉编译器变量x已经在别的地方定义过,并且初始值为 5
            extern int x=5; 


    typeid().name()和decltype的区别
        typeid().name(): 返回操作数的类型
            int x = 0;
                typeid(x).name();   输出 "i"

        decltype: 是一个关键字,用于推导表达式的类型,它返回一个类型，表示表达式的类型。
            int x = 0;
                decltype(x) y=x;    输出的类型为int


### 字符串
    C++ 标准库<string>提供了 string 类类型
    定义:
        定义一个名字为abc的string类字符串
            std::string abc;

#### string函数
1.  string的函数
    |函数名|功能|
    | --- | --- |
    | insert(插入位置,插入子字符串) | 字符串的插入 |
    | erase(起始位置,删除的长度) | 字符串的删除 |
    | replace(起始位置,长度,替换的字符串) | 字符串替换 |
    | swap(字符串1,字符串2)|字符串的交换 |
    | .substr(提取的起始位置,长度) | 提取字符串的子串 |
    | .append(str) | 在字符串的末尾添加字符串str |
    | .find(char,pos) | 查找pos起始位置开始的字符串,默认为0 |
    | .length() | 返回字符串的长度 |
    | .size() | 返回string对象的长度 |
    | .empty() | 根据string对象是否为空返回一个对应的布尔值 |

#### string类字符串的区别

    字符串字面量和string类字符串不是同一种类型
    
    string的下标必须大于等于0,小于s.size()

    strlen()
        strlen()是函数,返回字符串实际的长度
            strlen("123");  返回3

    sizeof()
        sizeof()是操作数,返回字符串的内存大小,不受字符数组实际存储数据的影响
            sizeof("123");    返回4
    
    size()
        返回字符串的长度
            string s = "123";
            cout<<s.size()<<endl;   返回3

### 引用

    引用: &

    声明方法:
        类型标识符 &引用名=目标变量名

    引用与指针的区别:
        不存在空引用,引用必须连接到一块合法的内存。

        一旦引用被初始化为一个对象,就不能被指向到另一个对象,指针可以在任何时候指向到另一个对象,

        引用必须在创建时被初始化,指针可以在任何时间被初始化

    创建:
        引用r是一个初始化为i的整形引用
            int i = 17;
            int &r = i;

### 标准输入输出
    标准库<iostrem>包含标准输入输出cin,cout

    1. 输入:
        cin >> a:
            读取a到cin,cin和scanf()一样使用空白(空格、制表符和换行符)来确定字符串的结束位置

        cin.get(ch):
            成员函数cin.get(ch)读取输入中的下一个字符(即使它是空格)，并将其赋给变量ch

        getline(is,line,ch):
            getline有3个参数:
                1. 读取的对象(标准输入,文件流对象,字符串流对象)
                2. 存储读取到的一行文本的字符串
                3. 分隔符,表示在哪个字符处停止读取,默认为换行符 '\n'。

            getline会在读取一整行,结束后舍弃换行符,读取换行符但是不存进数组中,直接丢弃

            每次调用 getline() 函数后,输入流的指针会自动移动到下一行的开头(如果是默认的分割符'\n')

        gets():从输入流中读取一个字符，同时该字符会从输入流中消失

    2. 输出:
        cout:
            << 符号表示该语句把这个字符串发送给cout,可以用<<符号拼接输出
            cout << "hello" << "world" <<endl;
            
        auto:
            对单个字符的输出可以通过for(auto a : sss)每次输出一个a


    3. endl刷新了缓存区并换行，或者用flush
    4. 清空缓冲区fflush(stdin)
    5.输出的时候默认保存6位小数

    输入输出流
    - istream：常用于接收从键盘输入的数据
    - ostream：常用于将数据输出到屏幕上
    - ifstream：用于读取文件中的数据
    - ofstream：用于向文件中写入数据
    - iostream：继承自istream和ostream类,因为该类的功能兼两者于一身,既能用于输入,也能用于输出
    - fstream：兼ifstream和ofstream类功能于一身,既能读取文件中的数据,又能向文件中写入数据。

2. <iomanip>是 C++ 标准库中的一个头文件，它包含了一些用于控制输入/输出流格式的函数和对象
    |名称|功能|
    | --- | --- |
    |setw(int n)|设置输入/输出宽度为 n 个字符。std::setw(5)|
    |setfill(char c)|设置填充字符为 c。|
    |setprecision(int n)|设置浮点数精度为 n 位。|
    |fixed|设置浮点数按固定小数点表示。|
    |scientific|设置浮点数按科学计数法表示。|
    |left|设置左对齐。|
    |right|设置右对齐。|
    |internal|设置内部对齐。|
    |dec|设置十进制数表示。|
    |hex|设置十六进制数表示。|
    |oct|设置八进制数表示。|
    |boolalpha|将布尔值输出为 "true" 或 "false"。|
    |showbase|在输出数字时显示基数（例如，十六进制）。|
    |showpoint|在浮点数中显示小数点。|
    |showpos|在正数前显示符号（+）。|
    |skipws|跳过空白字符。|
    |unitbuf|禁用缓冲区以提高速度。|
    |flush|刷新输出缓冲区。|

### 文件输入输出
    <fstream>标准库函数包含文件的输入输出
    fstream：文件输入输出流，用于文件输入输出。

    ifstream:
        从文件读入数据

            1. 打开文件
                std::ifstream ifs("in.txt");
    
                if(!ifs.is_open()){
                    std::cerr << "打开文件失败" << std::endl;
                    return 1;
                }
            
            2. 按\n读取
                std::string s;
                    while(std::getline(ifs, s))
                    std::cout << s << std::endl;
                
            3. 按空白字符读取
                std::string s;
                    while(ifs >> s)
                    std::cout << s << std::endl;
    
            4. 移动文件指针
                移动到文件开头
                    ifs.seekg(0, std::ios::beg);

            5. 关闭文件
                ifs.close();

    ofstream
        输出数据到文件
            1. 打开文件
                std::ofstream ofs("out.txt");
            
            2. 写入文件
                ofs << "hello" << std::endl;
                
            3. 关闭文件
                ofs.close();


    .is_open()是<fstream>库中的一个成员函数,检查文件流是否打开成功，如果成功返回true，否则返回false

### lambda

    lambda一种函数对象，它可以方便地定义一个匿名函数，从而简化代码的编写。
    Lambda表达式的本质是一个可调用对象，可以像函数一样被调用，也可以作为函数参数或返回值。


    [捕获列表](参数列表) mutable(可选) 异常属性 -> 返回类型 {
	    // 函数体
    }

    捕获参数:
        []：不捕获任何外部变量
        [&]：以引用方式捕获所有外部变量
        [=]：以值方式捕获所有外部变量
        [var1, var2, ...]：指定捕获特定的外部变量
        [&, var1, var2, ...]：以引用方式捕获所有外部变量，并指定捕获特定的外部变量
        [=, &var1, &var2, ...]：以值方式捕获所有外部变量，并以引用方式捕获特定的外部变量

#### 值捕获:
    与参数传值类似，值捕获的前提是变量可以拷贝，不同之处则在于，被捕获的变量在 Lambda表达式被创建时拷贝，而非调用时才拷贝
        void lambda_value_capture() {
            int value = 1;
            auto copy_value = [value] {
            return value;
            };

            value = 100;
            auto stored_value = copy_value();
            std::cout << "stored_value = " << stored_value << std::endl;
        }

    这时, stored_value == 1, 而 value == 100,因为 copy_value 在创建时就保存了一份 value 的拷贝

#### 引用捕获
    与引用传参类似，引用捕获保存的是引用，值会发生变化。
        void lambda_reference_capture() {
            int value = 1;
            auto copy_value = [&value] {
            return value;
        };

        value = 100;
        auto stored_value = copy_value();
        std::cout << "stored_value = " << stored_value << std::endl;
    }

    这时, stored_value == 100, value == 100,因为 copy_value 保存的是引用

### 动态内存管理
    在C++中,可以使用new来申请堆区内存空间,采用delete释放堆区内存空间
    
    new的使用语法为：
        申请单块内存空间不初始化：数据类型 *ptr = new 数据类型
        申请数组空间不初始化：数据类型 *ptr = new 数据类型[数据量]
        申请单块内存空间并初始化：数据类型 *ptr = new 数据类型(初始化值)
        申请数组空间并初始化：数据类型 *ptr = new 数据类型{初始化值1, 初始化值2, ...... }

    delete的使用语法为:
        释放单个内存空间：delete 指向动态开辟的内存区域的指针
        释放数组空间：delete[] 指向动态开辟的内存区域的指针 -- 其中[]就表示数组

#### malloc和new的区别
    malloc需要手动计算申请空间的大小，new只需要在数据类型后面的[]内输入所要申请类型空间的个数即可

    malloc的返回值类型为void*，需要强制类型转换，而new在使用时会显示说明申请空间的类型，无需强制类型转换

    malloc/free是函数，new/delete是操作符

    malloc申请空间失败返回NULL，需要判空，而new申请空间失败会抛异常，需要使用catch捕获异常

    如果申请了动态内存空间却不手动释放，就会造成内存泄漏

#### 智能指针


### 类

#### 构造的多种方法
    - name p1;//默认构造
    - name p2(20);//有参构造
    - name p3(p2);//拷贝构造
    - name p2 = 20;//等价于 name p2 = name(20),会认为是有参构造
    - name(999);//匿名构造,当前行结束，立即释放匿名对象
    - name p2();//不能这么写，会被认为是函数声明
    - name(p2);//不要利用拷贝构造，初始化匿名对象,编译器会认为是对象声明:name p2;
    

    浅拷贝会将内存地址同时拷贝过去，深拷贝需要自己开辟一块新的地址,如果属性有在堆区开辟的,要自己构造一个拷贝函数

    返回值不作为重载条件,重载条件是:同一个作用域,同一个函数名,同样的参数列表

    在继承中使用自身的成员变量和成员函数可以直接调用，如果要使用父类的要加上父类的作用域

    如果子类的成员函数和父类的成员函数同名,就会隐藏父类的成员函数,如果需要访问,

    virtual虚继承解决菱形继承带来的问题,多个同样的数据指向的是同一个数据

    函数模板如果用自动类型推导不能进行隐式类型转换，但是可以用显示类型转换

    静态成员变量可以通过类或者类名访问,在类内声明,在类外初始化

    每个空的对象都占有一个字节的地址空间，用来区分空对象占用的内存位置

    this本质是指针常量

    在函数后面加上const就是常函数,加上mutable的变量,即使在常函数和常对象里也是可是修改的

    在对象前面加上const就变成了常对象

    常对象只能调用常函数，不能调用普通成员函数，因为普通成员函数可以修改属性

    类外写成员函数，要在类的里面先写函数声明

### 哈希集
1. 哈希集set的使用
    |名称|使用方法|
    | --- | --- |
    |#include <unordered_set>|头⽂件|
    |unordered_set<int> hashset|定义|
    |hashset.insert(123)| 插⼊元素|
    |hashset.erase(123)|删除元素|
    |hashset.count(123)|返回的是被查找元素的个数。如果有,返回1,否则,返回0
    |hashset.find()|返回的是被查找元素的位置,没有则返回map.end()|
    |hashset.size()|获取哈希集元素个数|
    |hashset.clear()|清空哈希集|
    |hashset.empty()|判断哈希集是否为空|

    遍历哈希集合for(const auto& element : hashSet){ // 遍历哈希集合中的每个元素 // element 为集合中的一个元素 }

2. 计算最大公约数数
    int gcg(int a,int b) return b ? gcd(b,a%b) : a;

3. 匿名