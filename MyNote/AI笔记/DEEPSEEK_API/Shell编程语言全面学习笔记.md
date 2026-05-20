# Shell编程语言全面学习笔记

创建时间：2026-05-13 16:26

编写:DEEPSEEK_API# Shell编程语言笔记

## 1. 什么是Shell
Shell是用户与操作系统内核之间的命令解释器，它接收用户输入的命令，翻译后交给内核执行，并将结果返回给用户。同时，Shell也是一种脚本编程语言，通过编写Shell脚本可以实现任务自动化、系统管理、程序调度等功能。

常见的操作系统Shell：
- Linux/Unix：bash、zsh、sh、csh、ksh、fish
- Windows：cmd.exe、PowerShell

本笔记主要关注Linux环境中使用最广泛的Bash（Bourne Again SHell）。

## 2. Shell脚本基础
### 2.1 创建和执行脚本
1. 脚本文件通常以`.sh`为后缀（非强制）。
2. 第一行指定解释器：`#!/bin/bash` 或 `#!/usr/bin/env bash`。
3. 赋予执行权限：`chmod +x script.sh`
4. 执行方式：
   - `./script.sh` （需要执行权限）
   - `bash script.sh` （显式调用解释器）
   - `source script.sh` 或 `. script.sh`（在当前Shell中执行，影响当前环境）

### 2.2 基本输出
```bash
#!/bin/bash
echo "Hello, Shell!"
```
使用`echo`输出文本，`-e`选项可以启用转义字符，如`\n`换行，`\t`制表符。

### 2.3 注释
```bash
# 这是单行注释
: '
这是多行注释
也可以这样
'
<<'COMMENT'
这也是多行注释的方式
COMMENT
```

## 3. 变量
### 3.1 变量定义与使用
```bash
name="Alice"
age=25
```
注意：等号两边不能有空格。使用变量时需加`$`：
```bash
echo $name
echo ${name} # 严格边界，推荐写法
```

### 3.2 只读变量
```bash
readonly PI=3.14
PI=3.1415  # 报错
```

### 3.3 删除变量
```bash
unset name
```
不能删除只读变量。

### 3.4 变量作用域
- 默认在脚本内为全局变量。
- 使用`local`关键字在函数内声明局部变量。

### 3.5 环境变量
常见环境变量：`$HOME`, `$PATH`, `$USER`, `$SHELL`, `$PWD`等。
导出变量为环境变量：`export MYVAR=value`，子进程可以继承。

### 3.6 特殊变量
| 变量 | 含义 |
|------|------|
| `$0` | 脚本名称 |
| `$1`-`$9` | 第1到第9个参数 |
| `$#` | 参数个数 |
| `$*` | 所有参数（视为单个字符串） |
| `$@` | 所有参数（每个独立，推荐用`"$@"`） |
| `$?` | 上一条命令的退出状态（0成功） |
| `$$` | 当前Shell进程ID |
| `$!` | 最后一个后台进程的PID |

## 4. 字符串操作
### 4.1 字符串定义
```bash
str1=hello
str2='world'
str3="Hello, ${name}"  # 双引号内变量解析
```
单引号内原样输出，双引号内支持变量和转义。

### 4.2 常用操作
- 获取长度：`${#str}`
- 提取子串：`${str:2:4}` 从索引2开始取4个字符
- 替换：`${str/old/new}` 替换第一个匹配；`${str//old/new}` 替换所有匹配
- 删除前缀：`${str#pattern}` 最短匹配；`${str##pattern}` 最长匹配
- 删除后缀：`${str%pattern}` 最短匹配；`${str%%pattern}` 最长匹配
- 默认值：`${var:-default}` var为空或未定义时返回default；`${var:=default}` 还会赋值。

## 5. 数组（Bash）
### 5.1 定义数组
```bash
arr=(apple banana cherry)
arr[3]="date"
```

### 5.2 访问数组
- 所有元素：`${arr[@]}` 或 `${arr[*]}`
- 特定索引：`${arr[1]}`
- 数组长度：`${#arr[@]}`
- 元素长度：`${#arr[0]}`

## 6. 运算
### 6.1 算术运算
- 使用`$(( ))`：`sum=$((a + b))`
- 使用`let`：`let sum=a+b`
- 使用`expr`（较旧）：`` sum=`expr $a + $b` ``
支持运算符：`+ - * / % **`。注意乘法`*`需要转义或使用`$(())`。

### 6.2 关系运算（用于条件判断）
支持数值比较：`-eq`, `-ne`, `-gt`, `-lt`, `-ge`, `-le`。
字符串比较：`=`, `!=`, `-z`（长度为零），`-n`（长度非零），`<`, `>`（需双中括号内使用）。

### 6.3 文件测试运算
| 操作符 | 说明 |
|--------|------|
| `-e file` | 文件是否存在 |
| `-f file` | 是否为普通文件 |
| `-d file` | 是否为目录 |
| `-r/-w/-x file` | 是否可读/写/执行 |
| `-s file` | 文件是否非空 |

## 7. 条件判断
### 7.1 if语句
```bash
if [ condition ]; then
    commands
elif [ condition2 ]; then
    commands
else
    commands
fi
```
注意`[ ]`两边必须有空格。多条件可用`&&`和`||`。
现代推荐使用`[[ ]]`（Bash扩展），支持正则和更安全。

### 7.2 case语句
```bash
case $var in
    pattern1)
        commands;;
    pattern2|pattern3)
        commands;;
    *)
        default commands;;
esac
```

## 8. 循环
### 8.1 for循环
```bash
for var in item1 item2 ...; do
    commands
done

# C风格
for ((i=0; i<10; i++)); do
    commands
done
```

### 8.2 while循环
```bash
while [ condition ]; do
    commands
done
```

### 8.3 until循环（条件为假时执行）
```bash
until [ condition ]; do
    commands
done
```

### 8.4 循环控制
- `break`：跳出循环
- `continue`：跳过本次迭代

## 9. 函数
### 9.1 定义与调用
```bash
function myfunc() {
    local local_var="only inside"
    echo "第一个参数: $1"
    return 42  # 0~255，失败状态可非0
}
myfunc arg1 arg2
echo "返回值: $?"  # 42
```

函数参数通过`$1,$2...`访问，函数内可使用`$?`获取返回值。

### 9.2 使用命令输出作为返回值
```bash
get_date() {
    date "+%Y-%m-%d"
}
today=$(get_date)
```

## 10. 输入输出重定向
- `command > file`：覆盖输出到文件
- `command >> file`：追加输出到文件
- `command 2> file`：错误重定向
- `command &> file`：标准输出和错误合并
- `command < file`：从文件输入
- 管道：`command1 | command2`，将前一个命令的标准输出作为后一个命令的标准输入。
- Here Document：
```bash
cat <<EOF
多行文本
$变量可解析
EOF
```

## 11. 常用实用命令
Shell脚本经常结合系统命令完成复杂任务，常用命令：
- 文本处理：`grep`, `sed`, `awk`, `cut`, `sort`, `uniq`, `wc`, `tr`
- 文件查找：`find`, `locate`
- 进程管理：`ps`, `top`, `kill`, `jobs`, `bg`, `fg`
- 网络相关：`curl`, `wget`, `ping`, `ss`
- 定时任务：`crontab` （配合脚本）
- 权限：`chmod`, `chown`, `sudo`
- 压缩：`tar`, `gzip`

## 12. 调试方法
- `bash -x script.sh`：执行时打印每条命令
- 脚本内局部开启：`set -x` 开启，`set +x` 关闭
- 使用`trap`捕获信号进行清理
- 检查退出码：`$?`

## 13. 实战小示例：备份脚本
```bash
#!/bin/bash
# 备份指定目录到目标位置，带时间戳
SRC_DIR="/home/user/data"
BACKUP_DIR="/backup"
TIMESTAMP=$(date "+%Y%m%d_%H%M%S")
BACKUP_FILE="${BACKUP_DIR}/data_backup_${TIMESTAMP}.tar.gz"

if [ ! -d "$SRC_DIR" ]; then
    echo "源目录不存在: $SRC_DIR"
    exit 1
fi

mkdir -p "$BACKUP_DIR"
tar -czf "$BACKUP_FILE" "$SRC_DIR"
if [ $? -eq 0 ]; then
    echo "备份成功: $BACKUP_FILE"
else
    echo "备份失败"
    exit 2
fi
```

## 14. 最佳实践建议
1. 使用有意义的变量名，适当注释。
2. 脚本添加错误处理（`set -e` 遇到错误退出，`set -u` 未定义变量报错）。
3. 引用变量时加双引号防止路径含空格出错。
4. 复杂脚本分拆为函数，模块化。
5. 使用`main`函数作为入口：
```bash
main() {
    # 主逻辑
}
main "$@"
```

掌握Shell编程能极大提高日常运维和开发的效率，是每个后端工程师和运维工程师的必备技能。