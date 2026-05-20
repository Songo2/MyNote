streamlit可以让我们用Python代码做出AI网页界面
```python
import streamlit as st
```

# 页面基础

## title
```python
st.title("body")
```
显示应用标题

## header
```python
st.header("body")
```
显示主标题

## subheader
```python
st.subheader("body")
```
显示副标题

## write
```python
st.write(*args,**kwargs)
```
通用显示方法,支持多种格式

## text
```python
st.text("body")
```
显示文本

## set_page_config
```python
st.set_page_config(
    page_title="Ex-stream-ly Cool App",
    page_icon="🧊",
    layout="wide",
    initial_sidebar_state="expanded",
    menu_items={
        'Get Help': 'https://www.extremelycoolapp.com/help',
        'Report a bug': "https://www.extremelycoolapp.com/bug",
        'About': "# This is a header. This is an *extremely* cool app!"
    }
)
```
配置页面的默认设置

### page_title
页面标题,显示在浏览器标签页

### page_icon
页面图标

### layout 
页面布局位置,centered是居中,wide是铺满,None默认居中

### initial_sidebar_state
侧边栏的初始状态,auto让侧边栏隐藏在小组件上,expanded侧边栏展示,collasped侧边栏隐藏,int和auto差不多,但宽度有限制,None继承上次的状态,没有的话使用auto

### menu_items
配置右上角的菜单,这是个字典,键表示要配置的菜单项,有三个特殊的项可以是空值
#### "Get help"
指向一个URL网站
#### "Report a Bug"
指向一个URL网站
#### "About"
一个markdown

## badge
```python
st.badge("label","icon","color","width","help")
```
显示徽章
### label
显示在徽章上的文字

### icon
在徽章标签旁显示的表情或者图标,默认为None

### color
徽章颜色,默认为蓝色,支持红橙黄绿青蓝紫灰和主题颜色

### width
徽章的宽度
#### content
和内容宽度匹配

#### stretch
匹配父容器宽度

#### int
可以用整数规定宽度,但是不能超过父容器的宽度

### help
鼠标悬停在徽章上显示的文字

## success
```python
st.success("body","icon","width")
```
显示一个绿色的成功提示
### body
显示的文字

### icon
在左边的图标

### width
#### stretch
匹配父容器的宽度

#### int
用一个整数规定宽度

## info
```python
st.info("body","icon","width")
```
同success,但是是蓝色的

## error
```python
st.error("body","icon","width")
```
同success,但是是红色的

## warning
```python
st.warning("body","icon","width")
```
同success,但是是黄色的

# 交互组件

## button
```python
st.botton("label",key,"help",on_click,args,kwargs,"type","icon","icon_position",disable,width,shortcut)
```
一个按钮,返回布尔值,按下后会返回True
### label
按钮上的文字

### key
一个标识,可以访问对应key的小组件的数据

### help
鼠标悬停在按钮上显示的文字

### on_click
点击可以传递回调

### args
一个元组或列表,可以回调

### kwargs
一个字典,可以回调

### type
表示按钮的状态
#### primary
初级阶段,第一个阶段,未点击的状态

#### secondary
第二个阶段,点击了一次的状态

#### tertiary
最终阶段

### icon
按钮的图标

### icon_position
按钮的位置,left是左right是右

### diable
按钮是否禁用,True的时候禁用

### width
同之前条目,有stretch和int

### shortcut
按钮的快捷方式

## text_input
```python
st.text_input("label","value",max_char,"key","type","help",autocomplete,on_charge,args,kwargs,placeholder,disabled,label_visibility,"icon","width",bind)
```

### label
输入框的提示文本

### value
最初渲染时的文本

### max_char
最大字符数

### key
同上

### type
可以是default,password,password时会不能直接查看输入内容

### help
在输入框旁边的提示文本

### autocomplete
自动补全

### on_charge
文本输入变化时会调用一个可选回调

### args
同上

### kwargs
同上

### placeholder
占位符,输入框为空时显示的文本

### disabled
失效,为True时不能输入

### label_visibility
可见性有visable,hidden,collosped

### icon
图标

### width
同上

### bind
绑定输入框与URL查找的模式

## 