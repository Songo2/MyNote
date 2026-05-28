# Java语言学习笔记

创建时间：2026-05-24 01:03

编写:DEEPSEEK_API
标签:# Java语言学习笔记

## 1. Java概述

Java 是由 Sun Microsystems 公司于 1995 年推出的一种**面向对象**、**跨平台**、**健壮安全**的高级编程语言。  
核心特征：

- **简单性**：语法基于 C/C++，但移除了指针、多继承等复杂特性。
- **面向对象**：一切皆对象，支持封装、继承、多态。
- **跨平台性**：通过 JVM（Java Virtual Machine）实现 “Write Once, Run Anywhere”。
- **自动垃圾回收（GC）**：无需手动管理内存。
- **丰富的类库**：网络、IO、集合、多线程等。

三个技术平台：

- Java SE（Standard Edition）：桌面应用开发基础。
- Java EE（Enterprise Edition）：企业级分布式网络应用。
- Java ME（Micro Edition）：移动、嵌入式设备开发。

## 2. 开发环境搭建

### 2.1 JDK 安装与配置

1. 下载 JDK（建议 OpenJDK 17 及以上）。
2. 安装后配置环境变量：
   - `JAVA_HOME` → JDK 安装目录
   - `Path` → 追加 `%JAVA_HOME%\bin`
3. 验证安装：
   ```bash
   java -version
   javac -version
   ```

### 2.2 第一个程序 HelloWorld

```java
package com.example;

public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Java!");
    }
}
```

编译与运行：
```bash
javac HelloWorld.java    # 生成 HelloWorld.class
java HelloWorld          # JVM 执行
```

`main` 方法是程序入口，固定写法：`public static void main(String[] args)`。

## 3. 基础语法

### 3.1 关键字与标识符
- 关键字如 `class`, `public`, `static`, `void`, `int` 等，不能用作标识符。
- 标识符规则：字母、数字、下划线、$ 组成，不能以数字开头，区分大小写。

### 3.2 数据类型
分为 **基本类型** 和 **引用类型**。

#### 基本数据类型（8 种）
| 类型     | 大小    | 范围                           | 默认值   |
|----------|---------|--------------------------------|----------|
| byte     | 1 byte  | -128 ~ 127                     | 0        |
| short    | 2 bytes | -2^15 ~ 2^15-1                 | 0        |
| int      | 4 bytes | -2^31 ~ 2^31-1                 | 0        |
| long     | 8 bytes | -2^63 ~ 2^63-1                 | 0L       |
| float    | 4 bytes | 单精度科学计算                 | 0.0f     |
| double   | 8 bytes | 双精度科学计算                 | 0.0d     |
| char     | 2 bytes | 0 ~ 65535，Unicode 编码       | '\u0000' |
| boolean  | 1 bit   | true / false                   | false    |

#### 引用类型
- 类（class）
- 接口（interface）
- 数组（array）
- 枚举（enum）

### 3.3 变量与常量
```java
int age = 25;                // 变量
final double PI = 3.14159;   // 常量，不可修改
```

### 3.4 运算符
- 算术：`+ - * / % ++ --`
- 赋值：`\= += -= *= /= %=`
- 比较：`\== != > < >= <= instanceof`
- 逻辑：`&& || !`
- 位运算：`& | ^ ~ << >> >>>`
- 三元：`条件 ? 表达式1 : 表达式2`

### 3.5 流程控制
```java
// 条件判断
if (x > 0) { ... } else if (x == 0) { ... } else { ... }
switch (key) { case 1: ... break; default: ... }

// 循环
for (int i = 0; i < 10; i++) { ... }
while (condition) { ... }
do { ... } while (condition);

// 增强 for（遍历数组/集合）
for (Type item : iterable) { ... }
```

### 3.6 数组
```java
int[] arr = new int[5];               // 动态初始化
int[] arr2 = {1, 2, 3, 4};           // 静态初始化
Arrays.sort(arr);                     // 排序工具类
System.out.println(arr.length);       // 长度
// 多维数组
int[][] matrix = new int[3][4];
```

## 4. 面向对象编程

三大特征：**封装、继承、多态**

### 4.1 类与对象
```java
public class Person {
    // 属性（成员变量）
    private String name;
    private int age;

    // 构造方法（支持重载）
    public Person() {}
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // 方法
    public void setName(String name) { this.name = name; }
    public String getName() { return name; }
}
```
创建对象：`Person p = new Person("Alice", 30);`

### 4.2 封装
使用 `private` 隐藏内部状态，通过 `getter/setter` 控制访问。

### 4.3 继承
- 使用 `extends` 关键字，单继承（一个子类只能有一个直接父类）。
- 所有类默认继承 `Object`。
```java
public class Student extends Person {
    private String school;
    public Student(String name, int age, String school) {
        super(name, age);       // 调用父类构造
        this.school = school;
    }
    // 重写父类方法（可加 @Override 注解）
    @Override
    public String toString() {
        return "Student: " + getName();
    }
}
```
`super` 调用父类构造、方法或属性。

### 4.4 多态
同一接口，不同实现。
- 向上转型：`Person p = new Student(...);`
- 运行时根据实际对象调用重写方法（动态绑定）。
```java
Person[] people = {new Student(...), new Teacher(...)};
for (Person person : people) {
    person.introduce();   // 调用各自重写的方法
}
```
多态的必要条件：继承、重写、父类引用指向子类对象。

### 4.5 抽象类与接口
**抽象类**：用 `abstract` 修饰，不能被实例化，可包含抽象方法和具体方法。
```java
public abstract class Animal {
    public abstract void sound();
    public void breathe() { System.out.println("Breathing..."); }
}
```
**接口**：用 `interface` 定义，只包含方法声明（Java 8+ 可以有默认/静态方法）。
```java
public interface Flyable {
    void fly();
    default void land() { System.out.println("Landing..."); }
}
```
一个类可实现多个接口：`class Bird extends Animal implements Flyable {}`

### 4.6 内部类
- 成员内部类
- 静态内部类（`static` 修饰）
- 局部内部类（方法内定义）
- 匿名内部类（常配合接口/抽象类）

### 4.7 常用修饰符
- 访问控制：`public`、`protected`、`默认`（包级私有）、`private`
- `static`：属于类级别，共享
- `final`：类不可继承、方法不可重写、变量不可修改
- `abstract`：抽象类或抽象方法

## 5. 常用核心类

### 5.1 String
不可变字符序列。
```java
String s = "hello";
s.length();                 // 长度
s.charAt(1);                // 指定字符
s.substring(1, 3);          // 子串 [1,3)
s.indexOf('l');             // 查找
s.equals("Hello");          // 忽略大小写比较: equalsIgnoreCase()
s.toUpperCase();
s.trim();
s.split(",");               // 分割
s.replace('l', 'L');
// StringBuffer (线程安全) / StringBuilder (非线程更高效)，可变字符序列。
```

### 5.2 包装类
基本类型 ↔ 包装类，自动装箱/拆箱。
```java
Integer i = 10;             // 装箱
int j = i;                  // 拆箱
Integer.parseInt("123");
String.valueOf(123);
```

### 5.3 Math & Random
```java
Math.abs(-5);
Math.max(3, 5);
Math.pow(2, 3);
Math.random();              // [0.0, 1.0)
Random rand = new Random();
rand.nextInt(100);          // [0, 100)
```

### 5.4 日期时间（Java 8+）
```java
LocalDate date = LocalDate.now();
LocalTime time = LocalTime.of(14, 30);
LocalDateTime dt = LocalDateTime.of(date, time);
DateTimeFormatter fmt = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
String str = dt.format(fmt);
LocalDateTime parsed = LocalDateTime.parse("2025-01-01 10:20:30", fmt);
Duration / Period   // 时间间隔计算
```

## 6. 集合框架
存储对象的容器，位于 `java.util` 包。

| 接口        | 特点                     | 实现类示例                   |
|-------------|--------------------------|------------------------------|
| Collection  | 单列集合根接口           |                              |
| List        | 有序、可重复             | ArrayList, LinkedList, Vector |
| Set         | 无序、不可重复           | HashSet, TreeSet, LinkedHashSet |
| Queue       | 队列（FIFO）             | LinkedList, PriorityQueue, ArrayDeque |
| Map         | 键值对存储               | HashMap, TreeMap, LinkedHashMap |

常用方法：
```java
List<String> list = new ArrayList<>();
list.add("a");
list.get(0);
list.remove(1);
list.size();
list.contains("a");

Set<Integer> set = new HashSet<>();
set.add(10);
set.contains(10);

Map<String, Integer> map = new HashMap<>();
map.put("apple", 5);
map.get("apple");
map.containsKey("apple");
for (Map.Entry<String, Integer> e : map.entrySet()) { }
```

Comparable 与 Comparator 用于排序。

## 7. 异常处理
`Throwable` 是所有异常和错误的父类。
- `Error`：严重问题，通常不处理（如 `OutOfMemoryError`）。
- `Exception`：可处理的异常。
  - 受检异常（checked）：必须显式处理（try-catch 或 throws），如 `IOException`。
  - 运行时异常（unchecked）：`RuntimeException` 及其子类，可处理可不处理。

```java
try {
    // 可能异常代码
} catch (具体异常 e) {
    // 处理
} catch (异常1 | 异常2 e) {  // 多异常捕获
} finally {
    // 必定执行（资源释放）
}
// try-with-resources（自动关闭资源）
try (FileReader fr = new FileReader("file.txt")) {
    // ...
}
```

`throw` 手动抛出异常，`throws` 声明方法可能抛出的异常。

## 8. 泛型
参数化类型，提供编译时类型安全。
```java
// 泛型类
class Box<T> {
    private T item;
    public void setItem(T item) { this.item = item; }
    public T getItem() { return item; }
}
Box<String> strBox = new Box<>();

// 泛型方法
public static <T> T getMid(T[] arr) { return arr[arr.length/2]; }

// 通配符
void printList(List<?> list) { ... }    // 无界通配符
void addNumber(List<? super Integer> list) { ... } // 下界
void readNumber(List<? extends Number> list) { ... } // 上界
```

类型擦除：泛型仅存在于编译阶段，运行时类型信息被擦除为原生类型。

## 9. IO 流
输入输出流分类：

- 按流向：输入流 / 输出流
- 按单位：字节流（`InputStream` / `OutputStream`），字符流（`Reader` / `Writer`）

常用类：
```java
// 字节流
FileInputStream fis = new FileInputStream("in.dat");
FileOutputStream fos = new FileOutputStream("out.dat");
// 字符流
FileReader fr = new FileReader("text.txt");
FileWriter fw = new FileWriter("text.txt");
// 缓冲流
BufferedReader br = new BufferedReader(new FileReader("file"));
String line;
while ((line = br.readLine()) != null) { ... }
BufferedWriter bw = new BufferedWriter(new FileWriter("file"));
bw.write("data");
bw.newLine();
// 转换流（字节转字符）
InputStreamReader isr = new InputStreamReader(new FileInputStream("file"), "UTF-8");
```

对象序列化：`ObjectOutputStream` / `ObjectInputStream`，实现 `Serializable` 接口。

## 10. 多线程
### 10.1 创建线程
1. 继承 `Thread` 类，重写 `run()`。
2. 实现 `Runnable` 接口，作为 `Thread` 构造参数。
3. 实现 `Callable` 接口，配合 `FutureTask` 可获得返回值。

```java
class MyThread extends Thread {
    public void run() { ... }
}
new MyThread().start();

class MyRun implements Runnable {
    public void run() { ... }
}
new Thread(new MyRun()).start();
```

### 10.2 线程状态与生命周期
`NEW → RUNNABLE → BLOCKED/WAITING/TIMED_WAITING → TERMINATED`

### 10.3 常用方法
- `Thread.sleep(millis)`：休眠
- `join()`：等待线程结束
- `yield()`：放弃当前CPU时间片
- `setPriority(1-10)`

### 10.4 同步与锁
解决线程安全问题：
- `synchronized`：同步代码块 / 同步方法
- `Lock` 接口：`ReentrantLock`，更灵活
- `volatile` 关键字：保证变量可见性，禁止指令重排
- `wait()/notify()/notifyAll()`：线程通信（必须在同步块内）

### 10.5 高级工具
`java.util.concurrent` 包：
- 线程池：`Executors` 工厂，`ExecutorService`
- 并发集合：`ConcurrentHashMap`, `CopyOnWriteArrayList`
- `CountDownLatch`, `CyclicBarrier`, `Semaphore`

## 11. 反射
动态获取类信息、操作对象。
```java
Class<?> clazz = Class.forName("com.example.Person");
// 或 Person.class 或 obj.getClass()
Constructor[] cons = clazz.getConstructors();
Method[] methods = clazz.getMethods();
Field[] fields = clazz.getDeclaredFields();

// 创建实例
Object obj = clazz.getDeclaredConstructor().newInstance();
// 调用方法
Method m = clazz.getMethod("setName", String.class);
m.invoke(obj, "name");
// 访问私有属性
Field f = clazz.getDeclaredField("age");
f.setAccessible(true);
f.set(obj, 30);
```

## 12. 注解
给代码添加元数据。
- 内置注解：`@Override`, `@Deprecated`, `@SuppressWarnings`
- 元注解：`@Target`, `@Retention`, `@Inherited`, `@Documented`
- 自定义注解：
```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface MyAnnotation {
    String value() default "";
    int num() default 0;
}
```

## 13. Lambda 表达式与 Stream API (Java 8+)
函数式编程风格。
- 函数式接口：只有一个抽象方法的接口。
```java
// Lambda 语法
(parameters) -> expression
(parameters) -> { statements; }
// 示例
Runnable r = () -> System.out.println("Run");
List<String> list = Arrays.asList("a", "b");
list.forEach(s -> System.out.println(s));
```

- Stream API：处理集合数据。
```java
list.stream()
    .filter(s -> s.startsWith("a"))
    .map(String::toUpperCase)
    .sorted()
    .collect(Collectors.toList());
```

## 14. 实用工具与最佳实践
- 工具库：Apache Commons, Google Guava, Jackson/Gson（JSON）
- 单元测试：JUnit 5
- 构建工具：Maven / Gradle
- 版本控制：Git
- 代码规范：遵循阿里巴巴Java手册等，使用驼峰命名。
- 设计模式：单例、工厂、代理等在Java中的常见实现。

## 15. 总结
本笔记从 Java 语言基础到面向对象、集合、IO、多线程、反射等核心内容进行了系统梳理。掌握这些知识，配合大量实践项目，能够为 Java 开发打下坚实基础。持续深入建议研究：JVM 内存模型、类加载机制、JUC 并发编程、网络编程（Socket/NIO）、主流框架（Spring Boot, MyBatis）等。