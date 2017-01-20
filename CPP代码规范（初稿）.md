# 1. 说明

- 参考来源：Google C++ Style Guide
- https://google.github.io/styleguide/cppguide.html
- 此文档未尽内容，可参考上述文档做规范处理


# 2. 规范细节

## 2.1 特举说明的编码规范

1. 善于使用C++11的新特性（大部分原先boost实现的功能）

    智能指针：`std::shared_ptr, std::make_shared`
    
    多线程和同步：`std::thread, std::mutex, std::atomic`
    
    时间: `std::chrono`
    
    `auto, move, override, final`
    
    匿名函数
    
    其他标准模板库：`deuqe, sort, map, set, list, pair, tuple`

2. 命名空间的优雅使用
```
using namespace std;            // bad

using std::string;              // good
string my_str = "hello";

std::string my_str2 = "hello";  // very good

namespace my_space {
class Abc;                      // 命名空间里面的定义，尽量顶格开始写
}
```

3. 前向声明配合智能指针
```
// 在头文件中，如下定义，不再需要包含对应的头文件
class Abc;
std::shared< Abc > my_abc;
```

4. 尽量避免使用单例，static和全局变量

5. 优雅地log
```
// bad，一旦错误，成堆的error log输出
while(true)
{
    if(error)
        cout << “task error”;
    else
        cout << “task is running”;
}
```
```
// nice
while(true)
{
    static Timer timer;
    static int warn_delay_count = 1;
    static int warn_time_base = 100; // ms
    if(error)
    {
        if(timer.isStarted())
        {
            double pass_ms = timer.getMs();
            if(pass_ms >  warn_time_base*warn_delay_count)
            {
                cout << “task error”;
                warn_delay_count *= 2;
            }
        }
        else
            timer.start();
    }
    else
    {
        if(warn_delay_count > 1)
        {
            warn_delay_count = 1;
            cout << “task rerun”;
        }
        timer.start();
    }
}
```

6. 让错误处理更加完备

    使用`try...catch`
    
    将异常返回给调用者
    
7. 引入循环周期计数

    复杂的周期性计算的进程，引入循环周期的概念，这样的log信息和调试会更加有效

## 2.2 命名规范

#### 工程/库/可执行目标命名

全部小写，可用下划线。如：
```
my_project
my_library.lib
my_app.exe
```

#### 文件命名

全部小写，可用下划线；文件名应对应的反应文件中类的定义。如：
```
my_class.h
my_class.cpp
```

#### 类型命名

每个单独的单词的首字母大写，其他小写，不使用下划线。如：
```
// classes and structs
class UrlTable { ...
class UrlTableTester { ...
struct UrlTableProperties { ...

// typedefs
typedef hash_map<UrlTableProperties *, string> PropertiesMap;

// using aliases
using PropertiesMap = hash_map<UrlTableProperties *, string>;

// enums
enum UrlTableErrors { ...
```

#### 变量命名

全部使用小写，适度使用下划线。

- 一般的变量
```
string table_name;  // OK - uses underscore.
string tablename;   // OK - all lowercase.
```

- 类的成员变量
```
class TableInfo {
public:
  string table_name;    // public variables

private:
  string _table_name;   // private variables
  string _tablename;
  static Pool<TableInfo>* _pool;
};
```

#### 常量命名

用小写k作为前缀，后续每个单独的单词的首字母大写，其余小写，不使用下划线。如：
```
const int kDaysInAWeek = 7;
```

#### 函数命名

- 一般函数命名（每个单独的单词的首字母大写，其余小写，不使用下划线）
```
AddTableEntry()
DeleteUrl()
OpenFileOrDie()
```

- 轻量函数命名（遵循普通变量命名的方法）
```
class MyClass {
 public:
  ...
  bool is_empty() const { return _num_entries == 0; }   // 轻量函数：非常简单的函数，如一些内联

 private:
  int _num_entries;
};
```

#### 命名空间命名

全部使用小写，适度使用下划线。
```
namespace my_space {
    
}
```

#### 宏定义命名

全部大写，适度使用下划线。
```
#define ROUND(x) ...
#define PI_ROUNDED 3.0
```

#### 枚举命名

类型：每个单独的单词的首字母大写，其余小写，不使用下划线
常量：全部大写，适度使用下划线。
```
enum UrlTableErrors {
  OK = 0,
  OUT_OF_MEMORY = 1,
  MALFORMED_INPUT = 2,
};
```

