# C++基础语法笔记

创建时间：2026-05-07 13:04

# C++ 基础语法

C++ 是一种通用的编程语言，广泛用于系统/应用软件开发。本笔记将从基础语法开始，逐步介绍C++的核心概念。

---

## 1. Hello World 程序
```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
```
- `#include <iostream>`：包含标准输入输出库
- `using namespace std;`：使用标准命名空间
- `cout`：标准输出流对象
- `endl`：插入换行符

---

## 2. 基本数据类型

| 类型        | 说明           | 示例         |
|-------------|----------------|--------------|
| `int`       | 整数           | `int a = 10;`|
| `double`    | 双精度浮点数    | `double b = 3.14;`|
| `char`      | 字符           | `char c = 'A';`|
| `bool`      | 布尔型         | `bool flag = true;`|
| `string`    | 字符串         | `string str = "Hello";`|

---

## 3. 变量与常量
- 变量声明：
  ```cpp
  int x;
  double y;
  char c;
  ```
- 变量初始化：
  ```cpp
  int a = 10;
  double b(3.14);
  ```
- 常量定义：
  ```cpp
  const int MAX = 100;
  constexpr int MAX2 = 100; // C++11 引入，更优选择
  ```

---

## 4. 运算符
- 算术运算符：`+`, `-`, `*`, `/`, `%`
- 比较运算符：`==`, `!=`, `>`, `<`, `>=`, `<=`
- 逻辑运算符：`&&`, `||`, `!`
- 赋值运算符：`=`, `+=`, `-=`, `*=`, `/=`, `%=`

---

## 5. 控制流

### 条件语句
```cpp
if (a > b) {
    cout << "a > b" << endl;
} else if (a == b) {
    cout << "a == b" << endl;
} else {
    cout << "a < b" << endl;
}
```

### 循环语句
- `for` 循环：
  ```cpp
  for (int i = 0; i < 10; i++) {
      cout << i << endl;
  }
  ```
- `while` 循环：
  ```cpp
  int i = 0;
  while (i < 10) {
      cout << i << endl;
      i++;
  }
  ```

---

## 6. 函数

### 函数定义
```cpp
int add(int a, int b) {
    return a + b;
}
```

### 函数调用
```cpp
int result = add(3, 5);
cout << result << endl;
```

---

## 7. 指针与引用
- 指针：
  ```cpp
  int a = 10;
  int *p = &a; // p 指向 a 的地址
  cout << *p << endl; // 输出 10
  ```
- 引用：
  ```cpp
  int b = 20;
  int &ref = b; // ref 是 b 的别名
  cout << ref << endl; // 输出 20
  ```

---

## 8. 数组与字符串
- 数组声明：
  ```cpp
  int arr[5] = {1, 2, 3, 4, 5};
  ```
- 字符串处理（使用 `string` 类型）：
  ```cpp
  string str = "Hello";
  cout << str.length() << endl; // 输出字符串长度
  ```

---

## 9. 结构体与类
### 结构体
```cpp
struct Point {
    int x;
    int y;
};

Point p;
p.x = 10;
p.y = 20;
```

### 类
```cpp
class Person {
private:
    string name;
    int age;
public:
    void setName(string n) { name = n; }
    string getName() { return name; }
};
```

---

## 10. 面向对象编程
- 封装：通过访问控制（`private`, `public`）实现
- 继承：派生类继承基类属性
- 多态：通过虚函数实现

---

## 11. 标准库与头文件
- 常用头文件：
  - `<iostream>`：输入输出流
  - `<string>`：字符串处理
  - `<vector>`：动态数组
  - `<cmath>`：数学函数
  - `<algorithm>`：算法库

---

## 12. 学习建议
1. 从简单的控制台程序开始练习
2. 熟练掌握基本数据类型与运算符
3. 多练习条件语句与循环
4. 逐步学习函数、指针与类
5. 参考优质教材或在线课程（如《C++ Primer》）

---

> 注：本笔记仅涵盖C++基础语法，实际开发中需结合项目需求深入学习模板、STL、异常处理等内容。> 