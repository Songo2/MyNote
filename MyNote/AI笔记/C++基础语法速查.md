# C++基础语法速查

创建时间：2026-05-07 13:14

```cpp
// 1. 基本语法结构
#include <iostream>
using namespace std;

// 2. 数据类型
int age = 25;          // 整型
double salary = 10000.5; // 浮点型
char grade = 'A';      // 字符型
bool is_valid = true;  // 布尔型

// 3. 运算符
// 算术运算符
int a = 10 + 5;        // 加法
int b = 10 - 5;        // 减法
int c = 10 * 5;        // 乘法
int d = 10 / 5;        // 除法
int e = 10 % 3;        // 取模

// 4. 控制结构
// if语句
if (age >= 18) {
    cout << "成年人";
} else {
    cout << "未成年人";
}

// 循环
for (int i = 0; i < 5; i++) {
    cout << i << " ";
}

int count = 0;
while (count < 5) {
    cout << count << " ";
    count++;
}

// switch-case
int day = 3;
switch (day) {
    case 1: cout << "周一"; break;
    case 2: cout << "周二"; break;
    default: cout << "其他";
}

// 5. 函数
void greet() {
    cout << "Hello, World!";
}

int add(int x, int y) {
    return x + y;
}

// 6. 数组
int numbers[5] = {1,2,3,4,5};
for (int i=0; i<5; i++) {
    cout << numbers[i] << " ";
}

// 7. 指针与引用
int* ptr = &age;
cout << *ptr; // 输出25

int& ref = age;
ref = 30; // age变为30

// 8. 字符串
char str1[] = "Hello";
string str2 = "World";

// 9. 标准库
#include <vector>
#include <string>
#include <cmath>
#include <iostream>
#include <iomanip>
#include <fstream>
#include <sstream>
#include <algorithm>
#include <stdexcept>
#include <memory>
#include <utility>
#include <functional>
#include <numeric>
#include <complex>
#include <locale>
#include <chrono>
#include <thread>
#include <atomic>
#include <mutex>
#include <condition_variable>
#include <future>
#include <system_error>
#include <filesystem>
```

> ⚠️ 注意事项：
> 1. 使用`#include`引入头文件
> 2. 用`using namespace std;`或限定作用域（推荐）
> 3. 变量命名建议使用英文小写+下划线
> 4. 代码块需用`//`注释说明
> 5. 标准库头文件按功能分类整理