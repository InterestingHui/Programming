### 目录
- [命名风格](#命名风格)
- [文件命名](#文件命名)
- [注释](#注释)
- [大括号与换行](#大括号与换行)
- [空格](#空格)
- [其他](#空格)
- [函数](#函数)
- [类](#类)
- [常量](#常量)

#### 命名风格
- 如果项目组有特定的编程风格要根据项目组的统一来
- 常见的命名风格
  - 大驼峰:UpperCamelCase
  - 小驼峰:lowerCamelCase
  - 蛇形:snake_case
  - 匈牙利(以驼峰为基础，再加上特定的前缀来表示类型):uiUpperCamelCase
- 类型(class)名称大驼峰
- 函数名称大驼峰，函数传入参数小驼峰
- 局部变量小驼峰，类成员变量小驼峰
- 全局变量采用g_+小驼峰的匈牙利风格
- 举例：
```C++
Class SomeType{ // 类型大驼峰
public:
  int Fun(int a, int b) // 函数名大驼峰，参数小驼峰
  {
    int blockCount; // 局部变量小驼峰
  }
private:
  int objCount; // 成员变量小驼峰
};
SomeType g_fileCount; // 全局变量g_+小驼峰的匈牙利风格
```

#### 文件命名
- C++源文件采用.cpp后缀，头文件采用.h后缀
- 如果文件是一个类，则文件名和类名一致

#### 注释
- 只有在需要的时候注释，过多的注释反而会弱化有效注释
- 注释符和注释内容之间有一个空格: //[空格]内容
- 注释位于代码的上方或者右方均可
  - 如果是在右方，代码与注释符号之间也需要一个空格:int nowCount = 3; // 计数

#### 大括号与换行
- 3种换行风格
  - K&R 风格：函数大括号放到下一行开头，其他大括号放到该行结尾
  - 1TBS 风格：所有的大括号都放到该行结尾
  - Allman 风格：所有的大括号放到下一行开头
- 默认推荐K&R风格

#### 空格
- 行末不能加空格
- 运算符两遍加空格包括双目运算符
- if,switch,case,do,while,for等关键字后要加空格
- 逗号、句中分号后要加空格

#### 其他
- 行宽不超过120个字符，超过则要换行，优先在低运算符后换行，从可读性角度出发换行
- C++17之前不允许重载','、'&&'、'||'这三个操作符（因为会影响对象的求知顺序）；但是C++17之后明确定义了这些操作符的求值顺序与内置操作符一直，所以C++17之后可以重载这三个操作符。

#### 函数
- 函数输入数据校验
  - 函数接收源数据，需要校验
  - 进程间通信，需要校验
  - 应用层和内核层之间通信，需要校验
  - 可执行环境改变，需要校验
  - 同一函数（模块）下子函数的通信（数据传输），不需要校验
- 函数传参
  - 对于传入参数拷贝代价小的类型，传值；拷贝代价大的类型，传const引用
  - 对于要被移动的传入参数，应使用右值引用，并在函数内使用std::move
  - 对于要被转发的传入参数，应使用转发引用，并在函数内使用std::forward
  - 同时作为输入和输出的传入参数，不能使用const关键字
  - 尽量避免使用void*
  - 不能有未被使用的参数，实在不得已，如果由于某种原因要保留的话，就注释掉
- 函数出参
  - 返回多个值时，优先使用struct或者std::tuple进行封装
  - 不要使用std::move返回函数内的局部变量 
  - 优先返回值而不是参数，这样使得函数更简洁
  - 只有当传入/返回值可能无效的时候，才使用指针(也开业使用std::optional)，其他情况不推荐使用指针;

#### 类
- 需要保证类的封装性，成员变量声明为private，常量可以声明为public
- friend关键推荐使用在操作符重载的场景，其他情况要避免使用
- 当成员变量可以独立进行变化的时候，可以使用struct，否则使用class
- 类的public成员函数应尽量避免返回私有数据地址
- 类的构造函数应遵循完整性、可用性，例如要有对类的对象构造失败时的处理，推荐使用异常处理（如果项目允许出现异常处理的话）
- 单参数的构造函数应使用explicit关键字
- 类的成员变量**必须显式初始化**，除了以下情况
  - 如果类的成员变量具有默认构造函数，那么可以不做显式初始化 
- 类的所有构造函数都要保证所有成员变量被正确的初始化
- 优先使用**初始化列表**或者**类内初始化**来初始化成员
- 三之法则（Rule of three）
  - 如果类需要构建析构函数、拷贝构造函数或者拷贝赋值函数，那么该类需要同时构建这三个函数
- 五之法则（Rule of five）：适用于C11之后
  - 如果定义了析构函数、拷贝构造函数或拷贝赋值操作符，会阻止移动构造函数和移动赋值操作符的隐式定义，所以任何想要移动语义的类必须声明全部五个特殊成员函数。
- 零之法则（Rule of zero）
  - 如果类不需要专门处理资源的所有权，那么就不应该有自定义的析构函数、拷贝/移动构造函数或拷贝/移动赋值操作符
- 多态基类中的特殊函数
  - 如果多态基类声明了拷贝构造/拷贝赋值操作符，可能会发生切片，所以经常会将基类中的拷贝构造/拷贝赋值操作符显式定义为delete，并将移动构造/移动赋值操作符也显式定义为delete
- 类的继承
  - public继承必须遵循里氏替换原则（即基类出现的地方，换成派生类也能正常工作）
- 需要注意的罕见的UB（undefined behavior）错误
  - 如果构造函数和析构函数调用纯虚函数就会出现UB错误    
- 构造函数和析构函数中调用当前对象的虚函数，是不会有多态行为的
  - 只有基类析构函数是虚函数时，才能保证通过多态调用时，调用到派生类的析构函数
  - 所以通常情况下，基类的析构函数都应该是虚函数
- 基类的虚函数和派生类的虚函数的参数类型应该是一致的
- 重写虚函数时需要明确是override或final（这样有助于编译器检查）
- 禁止派生类覆盖/重写非虚函数，因为这既不能产生多态也会带来隐藏的问题，所以禁止

#### 常量
- 使用常量尽量采用const语义
- 需要使用const关键字的场景
  - 初始化后不会在修改的变量，用const修改，一方面表明变量属性；另一方面可以防止无意间修改变量而出现意外
  - 对于指针和引用类型的参数，如果不需要修改其引用的对象，应使用const修饰，明确表明在函数内部不会修改这个参数
  - 在类中，对于不会修改成员变量的成员函数，要用使用const修饰，
    - 注意，实例化为const的对象，也只允许调用其const修饰的成员函数；反之，如果该函数没有正确地使用const修饰，会导致const对象无法调用该函数
  - 在C11后的版本，应优先使用constexpr来定义在编译时就可以被计算出的值/函数 
