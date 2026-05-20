# Rust 语法全面笔记

创建时间：2026-05-13 14:13

# Rust 语法笔记

Rust 是一门系统级编程语言，注重安全、并发和性能。其语法深受 C++ 和函数式语言影响，核心概念包括所有权、借用和生命周期。以下从基础到高级，系统梳理 Rust 语法。

## 1. 变量与数据类型
- **变量绑定**：`let x = 5;`，默认不可变。可变变量需 `let mut x = 5;`。
- **常量**：`const MAX: u32 = 100_000;`，类型必须显式标注，值必须为编译期常量。
- **隐藏**：可以用 `let` 重复声明同名变量，覆盖前一个。
- **标量类型**：
  - 整数：`i8`, `u8`, `i16`, `u16`, `i32`, `u32`, `i64`, `u64`, `i128`, `u128`, `isize`, `usize`。
  - 浮点数：`f32`, `f64`。
  - 布尔：`bool`，值为 `true` 或 `false`。
  - 字符：`char`，占 4 字节，支持 Unicode。
- **复合类型**：
  - 元组：`let tup: (i32, f64, u8) = (500, 6.4, 1);`，可用模式解构 `let (x, y, z) = tup;` 或 `.0`, `.1` 访问。
  - 数组：`let arr = [1, 2, 3];`，长度固定，类型相同。访问越界会导致 `panic`。

## 2. 函数与控制流
- 函数定义：`fn function_name(param: Type) -> ReturnType { ... }`
- 表达式与语句：Rust 基于表达式，函数体最后一个表达式即为返回值，无需 `return`（也可使用 `return` 提前返回）。
- `if` 表达式：
  ```rust
  let number = if condition { 5 } else { 6 };
  ```
  条件必须为 `bool`，各分支返回类型必须一致。
- 循环：
  - `loop { ... }`：无限循环，`break` 可返回值。
  - `while condition { ... }`
  - `for elem in iterable { ... }`：遍历集合，安全高效。使用 `(0..n)` 生成范围。

## 3. 所有权与借用
- **所有权规则**：
  1. Rust 中每一个值都有一个所有者。
  2. 一次只能有一个所有者。
  3. 当所有者离开作用域，值将被丢弃。
- **移动**：赋值或传参时，对于非 `Copy` 类型，所有权转移（原变量失效）。
- **Copy trait**：简单标量类型实现 `Copy`，赋值时拷贝而非移动。
- **引用与借用**：
  - 不可变引用：`&T`，允许多个。
  - 可变引用：`&mut T`，同一时间只能有一个可变引用，且不能与不可变引用共存。
  - 引用必须始终有效（生命周期保证）。
- **切片**：`&[T]` 或 `&str`，是对集合部分数据的引用，不拥有所有权。

## 4. 结构体、枚举与模式匹配
### 结构体
- 定义：
  ```rust
  struct User {
      username: String,
      email: String,
      sign_in_count: u64,
      active: bool,
  }
  ```
- 实例化：`let user1 = User { ... };`，字段初始化简写、结构体更新语法 `..user1`。
- 元组结构体：`struct Color(i32, i32, i32);`
- 单元结构体：`struct Unit;`
- 方法：使用 `impl` 块定义，第一个参数为 `self`、`&self` 或 `&mut self`。

### 枚举
- 定义变体，可关联数据：
  ```rust
  enum Message {
      Quit,
      Move { x: i32, y: i32 },
      Write(String),
      ChangeColor(i32, i32, i32),
  }
  ```
- `Option<T>`：标准库定义的枚举，表示可能存在值 `Some(T)` 或无值 `None`，处理空值安全。

### 模式匹配
- `match` 表达式：
  ```rust
  match value {
      pattern1 => expr1,
      pattern2 if condition => expr2,
      _ => default_expr,
  }
  ```
  必须穷尽所有可能。
- `if let`：只匹配一种模式，简化代码：
  ```rust
  if let Some(x) = optional { ... } else { ... }
  ```
- `while let`：循环匹配。

## 5. 集合数据类型
- **Vector**：`Vec<T>`，动态数组。
  ```rust
  let mut v: Vec<i32> = Vec::new();
  v.push(1);
  let v2 = vec![1, 2, 3];
  // 访问：v[2] 或 v.get(2)，get 返回 Option
  ```
- **String**：UTF-8 编码的可增长字符串，`String` 类型。
  ```rust
  let mut s = String::from("hello");
  s.push_str(", world");
  // 拼接：使用 + 或 format!
  ```
  索引访问会返回字节或字符切片，需注意 UTF-8 边界。
- **HashMap**：`HashMap<K, V>`。
  ```rust
  use std::collections::HashMap;
  let mut scores = HashMap::new();
  scores.insert(String::from("Blue"), 10);
  // 获取：scores.get(&key)
  // 遍历：for (k, v) in &scores { ... }
  // 更新：entry(key).or_insert(value)
  ```

## 6. 错误处理
- **`panic!`**：不可恢复错误，栈展开或直接终止。
- **`Result<T, E>`**：可恢复错误，必须处理。
  ```rust
  enum Result<T, E> {
      Ok(T),
      Err(E),
  }
  ```
  常用 `match`、`unwrap`（`Err` 时 panic）、`expect`（带信息 panic）、`?` 运算符（传播错误）。
- **`?` 运算符**：在返回 `Result` 的函数中，用于自动解包或提前返回错误。

## 7. 泛型、Trait 与生命周期
### 泛型
- 函数、结构体、枚举均支持泛型：
  ```rust
  fn largest<T: PartialOrd>(list: &[T]) -> &T { ... }
  struct Point<T> { x: T, y: T }
  enum Option<T> { Some(T), None }
  ```
  编译时单态化生成具体代码，无运行时开销。

### Trait
- 定义共享行为：
  ```rust
  trait Summary {
      fn summarize(&self) -> String;
      // 默认实现
      fn default_method(&self) { ... }
  }
  ```
- 为类型实现 trait：`impl Summary for NewsArticle { ... }`（孤儿规则限制）。
- Trait 作为参数：
  - `fn notify(item: &impl Summary)`
  - `fn notify<T: Summary>(item: &T)`
  - 多重约束：`+`，`where` 子句。
- 返回实现了 trait 的类型：`fn returns_summarizable() -> impl Summary`，适用于闭包等具体类型不具名情况。
- 泛型通过 trait 约束保证功能，即 trait bound。
- 常用标准 trait：`Debug`, `Clone`, `Copy`, `PartialEq`, `Hash`, `Drop`, `Default`。

### 生命周期
- 核心目的：确保引用始终有效，防止悬垂指针。
- 标注语法：`'a`，放在 `&` 后面、类型之前，`&'a T`。
- 函数签名：
  ```rust
  fn longest<'a>(x: &'a str, y: &'a str) -> &'a str { ... }
  ```
  表示返回的引用生命与参数中较短者一致。
- 结构体包含引用时需标注：
  ```rust
  struct Excerpt<'a> {
      part: &'a str,
  }
  ```
- 生命周期省略规则：编译器在大部分常见情况可自动推导，每个引用参数都有各自生命周期，只有一个输入生命周期时赋予输出，多个输入且一个是 `&self`/`&mut self` 则赋予 `self` 的生命周期。
- 静态生命周期：`'static`，存活于整个程序期间，如字符串字面量。

## 8. 闭包与迭代器
- **闭包**：匿名函数，可捕获环境变量。
  ```rust
  let closure = |param| { body };
  // 自动推断参数、返回类型，可强制使用 `Fn` trait
  ```
  三种捕获方式：`FnOnce`（夺所有权）、`FnMut`（可变借用）、`Fn`（不可变借用）。
- **迭代器**：实现 `Iterator` trait 的类型，惰性求值。
  ```rust
  let v = vec![1, 2, 3];
  let v1: Vec<_> = v.iter().map(|x| x + 1).collect();
  ```
  常用方法：`map`, `filter`, `fold`, `zip`, `enumerate`, `chain` 等。

## 9. 代码组织与模块
- **包**：Cargo 管理的项目，Cargo.toml 配置文件。
- **crate**：库或二进制项目，根文件 `src/lib.rs` 或 `src/main.rs`。
- **模块**：使用 `mod` 定义，控制隐私（默认私有，`pub` 公开）。
  ```rust
  mod my_module {
      pub fn public_fn() {}
  }
  ```
- **路径**：绝对路径 `crate::front_of_house::...`，相对路径 `self::` 或 `super::`。
- **use**：将路径引入作用域 `use std::collections::HashMap;`，`as` 重命名，`*` 引入所有公开项。
- 多文件拆分：模块可对应目录下的 `mod.rs` 或同名文件。

## 10. 常用标准宏与属性
- **宏**：`println!`, `format!`, `vec!`, `println!`, `dbg!`, `assert!`, `assert_eq!`, `panic!` 等。
- **属性**：`#[derive(Debug)]` 自动实现 `Debug`，`#[allow(unused)]`，`#[test]` 标记测试函数。
- **测试**：`#[cfg(test)]` 模块，`#[test]` 函数，`assert!`，`assert_eq!`，`cargo test` 运行。

## 11. 并发语法（简略）
- **线程**：`std::thread::spawn`，闭包传递，`await` 等待（需 `JoinHandle`）。
- **消息传递**：`std::sync::mpsc`，`send` / `recv`。
- **共享状态**：`Arc<Mutex<T>>`，原子引用计数和互斥锁。
- Send / Sync trait 保证线程安全。

以上覆盖 Rust 主要语法范畴，深入理解所有权、生命周期和 trait 系统是掌握 Rust 的关键。建议在实际项目中多编写练习，以熟悉编译器的规则和错误信息。