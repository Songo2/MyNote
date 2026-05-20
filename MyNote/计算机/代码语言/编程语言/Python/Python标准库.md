#Python 
# builtins(内置库)
## 内置库中包含内置的数据类型
int,float,str,bool,list,tuple,dict,set,NoneType

## 内置的常量
True,False,None

## 内置函数
### 输入输出
print(),input()

### 类型转换
int(),float(),str(),bool(),list(),tuple(),dict(),set()

### 序列操作
len(),max(),min(),sum(),sorted(),range(),enumerate(),zip()

### 数学运算
abs(),pow(),round()

### 判断检测
type(),isinstance(),all(),any()

### 其他
eval(),open(),exit()

# os(操作系统库)
os库包含与操作系统交互,管理文件,路径,文件夹,系统命令,权限的函数

## 文件夹与目录
getcwd() 获取当前工作目录
chdir(路径) 根据路径切换工作目录
listdir(路径) 返回路径下的所有文件和子文件夹,返回一个列表
mkdir(文件夹名) 创建一个文件夹
makedirs(文件夹) 创建多级的嵌套文件夹
rmdir(文件夹) 删除空文件夹
removedirs(多级空文件夹) 递归删除多级空文件夹

## 文件操作
remove(文件名) 删除文件
rename(旧名,新名) 重命名文件或文件夹

## 路径判断
path.exists(路径) 判断文件或文件夹是否存在
path.isfle(路径) 判断是不是文件
path.isdir(路径) 判断是不是文件夹
path.abspath(路径) 输出绝对路径
path.basename(路径) 获取文件名
path.dirname(路径) 获取文件所在目录

## 系统
name 系统类型 (nt是Windows,posix是Linux或Mac)
sep 系统路径分隔符(Windows是反斜杠,Linux或Mac的是正斜杠)
environment 系统环境变量
system(命令) 执行系统命令

# sys(解释器库)
sys库能和解释器进行交互

## 路径与模块
path 模块搜索路径,是一个列表
modules 当前已加载的模块,是个字典
meta_path 底层模块加载机制

## 程序退出与中止
exit([code]) 主动退出程序,code是退出码,0默认正常
(新)raise_exc_info()/(旧)exc_info()获取当前异常信息

## 系统/解释器
version Python版本的完整字符串
version_info 版本元组,可用来判断大版本
platform 运行的平台
implementation 当前Python的实现
byteorder 系统字节序

## 标准输入输出流
stdin 标准输入
stdout 标准输出(print)
stderr 标准错误输出

## 命令行
argv 命令行参数,是个列表

## 内存与对象
getsizeof(obj) 获取对象占用字节数
getrefcount(obj) 获取对象引用次数

## 递归限制
getrecursionlimit() 获取默认递归深度上限
setrecursionlinit(n) 修改最大递归层数

## 垃圾回收
gc_enabled() 是否开启垃圾回收
getgc() 等待gc接口

## 其他
copyright 版权信息
executable Python解释器完整路径
last_type/last_value 上次异常缓存

# string(字符串库)
## 字母类
ascii_letters 所有大小写字母
ascii_lowcase 小写字母
ascii_uppercase 大写字母

## 数字类
digits

## 标点符号
punctuation

## 空白符号
whitecase

## 可打印符号
printable

## 十六进制和八进制
hexdigits octdigits

## 公共函数
capwords(s,sep=None) 每个单词首字母大写,自动清理多余空格
maketrans() 生成替换表

## 模板类
Template 字符串模板
子类有SafeTemplate TemplateError

# re(正则库)
正则库搭配正则表达式进行批量文本处理

## 查找
match(pat,str) 在字符串开头查找
search(pat,str) 全局查找,找第一个
findall(pat,str) 全局查找,返回匹配的列表
finditer(pat,str) 返回迭代器,储存所有匹配对象
fullmatch(pat,str) 整个字符串是否完全匹配
escape(str) 自动转义特殊符号

## 替换
sub(pat,new,str) 批量替换
subn(pat,new,str) 在sub的基础上返回替换次数

## 编译
compile(pat) 编译正则,生成Pattern
purge() 清空正则缓存

## 正则核心类
Pattern 正则模式类,用于存储编译后的对象
Match 匹配结果类,用于存储匹配成功后对象的信息
有以下方法
group() 取匹配的内容
groups() 取分组内容
span() 返回起始和结束下标组成的元组
start() 起始位置
end() 结束位置

## 匹配模式常量
I/IGNORECASE 忽略大小写
M/MULTILINE 多行模式
S/DOTALL 匹配换行符
X/VERBOSE 正则里允许加空格和注释
A/ASCII 只匹配ASCII码
U/UNICODE 支持Unicode
L/LOCALE 本地化
# json(js对象表示库)

# datetime(日期库)

# time(时间库)

# calendar(日历库)

# math(数学库)

# random(随机库)

# statistics(统计库)

# pathlib(新路径库)

# csv(csv表格库)

# pickle(二进制化库)

# urlib(网络库)

# threading(线程库)

# multiprocessing(多线程库)

# queue(队列库)

# collections(容器库)

# itertools(迭代器库)

# bisect(二分查找库)

# logging(日志库)

# traceback(捕获库)

# configparser(配置库)

# subprocess(外部调用库)

# shutil(文件库)

