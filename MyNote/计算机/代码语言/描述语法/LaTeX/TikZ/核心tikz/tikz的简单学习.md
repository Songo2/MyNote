
内容来自minimaltikz

tikz默认使用笛卡尔坐标系
# 绘制直线和曲线

如果你想要画些什么,你应该使用
```
\draw xxx;
```
使用这个命令来绘制图形

## 直线

绘制一条直线可用下面这个命令
```
\draw (,) -- (,);
```

演示下面这个命令绘制的直线
```
\draw (0,0)--(1,2);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (0,0)--(1,2);
\end{circuitikz}
\end{document}
```

我们可以用链式的声明点来绘制一系列直线(折线)

```
\draw (0,0)--(1,2)-- (2,3)-- (1,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (0,0)--(1,2)-- (2,3)-- (1,0);
\end{circuitikz}
\end{document}
```

___
## 缩放

在环境
```
\begin{xxx}
	xxx
\end{xxx}
```
的begin后面有一个选项scale可以缩放图片,使用方法如下

```
\begin{xxx}[scale=?]
	xxx
\end{xxx}
```

我们以这条直线为示例图形
```
\draw (0,0)--(1,2);
```
默认是scale=1

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (0,0)--(1,2);
\end{circuitikz}
\end{document}
```

scale=2

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american,scale=2]
	\draw (0,0)--(1,2);
\end{circuitikz}
\end{document}
```

scale=3

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american,scale=3]
	\draw (0,0)--(1,2);
\end{circuitikz}
\end{document}
```

___
## 箭头

对于直线,我们可以对其两端进行修饰,产生箭头等,命令如下,前面的方括号是可选选项的集合

```
\draw[?-?] (,) -- (,);
```

两端可以是`<`,`>`,`|`

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw[->] (0,0)--(2,0);
	\draw[<-] (0,-2)--(2,-2);
	\draw[|->] (0,-4)--(2,-4);
\end{circuitikz}
\end{document}
```

___
## 粗细

这也是一个可选选项,直接写在方括号里,和其他的选项用逗号分隔,可选的粗细程度有

- ultra thin
- very thin
- thin
- semithick
- thick
- very thick
- ultra thick

前两个在笔记里直接看不见,从thin开始展示

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw[thin] (0,0) -- (2,0);
	\draw[semithick] (0,-2) -- (2,-2);
	\draw[thick] (0,-4) -- (2,-4);
	\draw[very thick] (0,-6) -- (2,-6);
	\draw[ultra thick] (0,-8) -- (2,-8);
\end{circuitikz}
\end{document}
```

我们也可以使用line width=?这个选项进行自定义

line width=12

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw[line width=12] (0,0)--(2,0);
\end{circuitikz}
\end{document}
```

___
## 点划线

对直线的线型,默认是实线,我们也可以改成点线或者划线(虚线),这也是个可选选项,分别是dotted和dashed

普通粗细的点线看不清,我放大成ultra thick

点线

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw[dotted,ultra thick] (0,0) to (2,0);
\end{circuitikz}
\end{document}
```


划线

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw[dashed,ultra thick] (0,0) -- (2,0);
\end{circuitikz}
\end{document}
```

___
## 颜色

在可选选项里面有颜色,可以直接写颜色比如red,或者写color=red


```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw[red] (0,0) -- (2,0);
\end{circuitikz}
\end{document}
```

可选的颜色有很多,这里暂不介绍
___
## 图形

我们可以直接画图形,命令如下

```
\draw (,) 图形 参数
```

比如circle(圆),前面的坐标是圆心,后面加方括号,里面写半径(radius)

```
\draw (1,1) circle [radius=1];
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (1,1) circle [radius=1];
\end{circuitikz}
\end{document}
```

rectangle(矩形),前面的坐标是一个顶点,后面再加一个坐标构成对角线

```
\draw (0,0) rectangle (4,3);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (0,0) rectangle (4,3);
\end{circuitikz}
\end{document}
```

图形有很多,这里暂不列举
___
## 出入角度

我们绘制的直线其实本质也是曲线,它有两个可选选项,出射角度(out)和入射角度(in),默认为0

要使用它的可选选项,需要使用另外一种语法to

```
\draw (,) to[] (,);
```

to在普通情况下和--一样,但是当需要使用特殊功能时需要使用to,to后面的方括号填入内容

```
\draw (0,0) to[out=45,in=120] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (0,0) to[out=45,in=120] (2,0);
\end{circuitikz}
\end{document}
```

```
\draw (0,0) to[out=90,in=-90] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (0,0) to[out=90,in=-90] (2,0);
\end{circuitikz}
\end{document}
```

___
## 函数

我们可以绘制函数图像

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american,xscale=9,yscale=4]
	\draw [<->] (0,0.8)-- (0,0)-- (0.5,0);
	\draw[green, ultra thick, domain=0:0.5] plot (\x, {0.025+\x+\x*\x});
\end{circuitikz}
\end{document}
```

我们先说一下缩放,缩放有细致的选项,xscale和yscale,是两个方向上的缩放

同时我们先利用之前的内容画一个坐标系

```
\draw [<->] (0,)-- (0,0)-- (,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw [<->] (0,2)-- (0,0)-- (2,0);
\end{circuitikz}
\end{document}
```

绘制函数需要使用数学引擎,使用plot来绘制函数,命令如下

```
\draw plot(自变量,{表达式})
```

自变量需要加上反斜杠转义如\x,

```
\draw plot(\x, {\x+\x*\x});
```
上面表示的就是$0.025+x+x^2$

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american,scale=0.2]
	\draw plot(\x, {\x+\x*\x});
\end{circuitikz}
\end{document}
```

效果如上,(scale=0.2)

对于函数,我们有可选选项定义域(domian),写在draw后面的方括号里,默认为(domain=-5:4.6)

我们不使用特殊函数的话只能写出多项式,特殊函数需要使用像Python里的函数如

- 三角函数 sin(\x),cos(\x),tan(\x)
- 阶乘:factorial(\x)
- 平方根:sqrt(\x)

等等

```
\draw plot(\x, {sin(\x r)});
```
(正常写是角度制,在后面加个r才是弧度制)

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw plot(\x, {sin(\x r)});
\end{circuitikz}
\end{document}
```

___
# 填充

前面我们使用color=xxx或者直接写颜色的可选选项是对图形的边界上色,如果我们需要对整个图形填充颜色需要使用fill=xxx这个选项

```
\draw [fill=yellow] (0,0) rectangle (4,3);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw [fill=yellow] (0,0) rectangle (4,3);
\end{circuitikz}
\end{document}
```

但是这两个选项是不能同时存在的,如果想同时使用两个选项需要两个图形

如果我们用线绘制了闭合图形,也可以使用fill=xxx来填充这个区域

```
\draw [ultra thick, fill=purple] (2,0) to [out=87,in=150] (3,1)-- (2.85,.15)-- (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american,scale=2]
	\draw [ultra thick, fill=purple] (2,0) to [out=87,in=150] (3,1)-- (2.85,.15)-- (2,0);
\end{circuitikz}
\end{document}
```

___



