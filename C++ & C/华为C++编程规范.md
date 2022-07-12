### 目录
- [命名风格](#命名风格)

##### 命名风格
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
