
circuitikz 是一个在 LaTeX 中的Tikz的用代码直接绘制电气和电子电路图的专用宏包

在Obsidian里安装TikZJax插件后能在代码块中写
___
# 开始

## 格式

在代码块右上角写tikz
```
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[european]
	
\end{circuitikz}
\end{document}
```
用这个格式包裹

## 备注

在
```
\begin{circuitikz}
```
后面可以加一个方括号,里面可以填两个可选参数,scale表示画布大小

- scale=1

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[scale=1,european]
	\draw (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```
- scale=2
```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[scale=2,european]
	\draw (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

此外可选的另一个参数是符号标准,european表示欧式,american表示美式

- european
欧式电阻
```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[european]
	\draw (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

- american
美式电阻
```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```




___
# 绘制

绘制的代码以\draw开头,在后面可以加方括号,里面可选参数

circuitikz将常用的电路元件抽象为边和点,其中电容电阻等两端元件是边

## 颜色 color

默认为白色,在方括号里写color=...

### 基础颜色

可以直接写的基础颜色有

- `black`
- `white`
- `red`
- `green`
- `blue`
- `cyan`
- `magenta`
- `yellow`
- `gray`


我们以这个画电阻的命令为例
```
\draw (0,0) to[R] (2,0);
```

蓝色 blue

```
\draw[color=blue] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=blue] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

红色 red

```
\draw[color=red] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=red] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

绿色 green

```
\draw[color=green] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=green] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

青色 white

```
\draw[color=cyan] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=cyan] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

黄色 yellow

```
\draw[color=yellow] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=yellow] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

洋红 magenta

```
\draw[color=magenta] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=magenta] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

灰色 gray

```
\draw[color=gray] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=gray] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

深灰色

```
\draw[color=darkgray] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=darkgray] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

浅灰色

```
\draw[color=lightgray] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=lightgray] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

___
### xcolor拓展(自然颜色)

这个在Tikz里面需要使用xcolor的宏包
\usepackage{xcolor}
在circuitikz里默认开启

- `brown`
- `lime`
- `orange`
- `pink`
- `violet`
- `purple`
- `teal`
- `olive`

棕色 brown

```
\draw[color=brown] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=brown] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

柠檬绿 lime

```
\draw[color=lime] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=lime] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

橙色 orange

```
\draw[color=orange] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=orange] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

粉色 pink

```
\draw[color=pink] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=pink] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

紫罗兰 violet

```
\draw[color=violet] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=violet] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

紫色 purple

```
\draw[color=purple] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=purple] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

蓝绿色 teal

```
\draw[color=teal] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=teal] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

橄榄绿

```
\draw[color=olive] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=olive] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

___
### 特定名称颜色(dvipsnames)

给xcolor包的dvipsnames打开能有一系列特定名称的经典颜色,基于CMYK,是印刷行业的标准
\usepackage[dvipsnames]{xcolor}
这在circuitikz也是默认开启的

它会在xcolor的基础上加入49种颜色
___
#### 颜色列表

- Apricot
    
- Aquamarine
    
- Bittersweet
    
- BlueGreen
    
- BlueViolet
    
- BrickRed
    
- BurntOrange
    
- CadetBlue
    
- CarnationPink
    
- Cerulean
    
- CornflowerBlue
    
- Dandelion
    
- DarkOrchid
    
- Emerald
    
- ForestGreen
    
- Fuchsia
    
- Goldenrod
    
- GreenYellow
    
- JungleGreen
    
- Lavender
    
- LimeGreen
    
- Magenta
    
- Mahogany
    
- Maroon
    
- Melon
    
- MidnightBlue
    
- Mulberry
    
- NavyBlue
    
- OrangeRed
    
- Orchid
    
- Peach
    
- Periwinkle
    
- PineGreen
    
- Plum
    
- ProcessBlue
    
- RawSienna
    
- RedOrange
    
- RedViolet
    
- Rhodamine
    
- RoyalBlue
    
- RoyalPurple
    
- RubineRed
    
- Salmon
    
- SeaGreen
    
- Sepia
    
- SkyBlue
    
- SpringGreen
    
- Tan
    
- TealBlue
    
- Thistle
    
- Turquoise
    
- VioletRed
    
- WildStrawberry
    
- YellowGreen
    
- YellowOrange
___
#### 颜色展示

##### 蓝紫色

天蓝 SkyBlue

```
\draw[color=SkyBlue] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=SkyBlue] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

BlueViolet

```
\draw[color=BlueViolet] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=BlueViolet] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

CadetBlue 军蓝

```
\draw[color=CadetBlue] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=CadetBlue] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

Cerulean 蔚蓝(未实现)

CornflowerBlue 矢车菊

```
\draw[color=CornflowerBlue] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=CornflowerBlue] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

MidnightBlue 午夜蓝

```
\draw[color=teal] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=MidnightBlue] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

NavyBlue 藏青色

```
\draw[color=NavyBlue] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=NavyBlue] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

Periwinkle 长春花(未实现)

ProcessBlue 印刷蓝(未实现)

RoyalBlue 皇家蓝

```
\draw[color=RoyalBlue] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=RoyalBlue] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

TealBlue (未实现)

RoyalPurple 皇家紫(未实现)

Turquoise 绿松石

```
\draw[color=Turquoise] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=Turquoise] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

BlueGreen(未实现)
___
##### 绿色

Aquamarine 海蓝宝

```
\draw[color=Aquamarine] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=Aquamarine] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

Emerald 祖母绿(未实现)

ForestGreen 森林绿

```
\draw[color=ForestGreen] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=ForestGreen] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

GreenYellow

```
\draw[color=GreenYellow] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=GreenYellow] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

JungleGreen 丛林绿(未实现)

LimeGreen

```
\draw[color=LimeGreen] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=LimeGreen] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

PineGreen 松绿

SeaGreen 海绿色

```
\draw[color=SeaGreen] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=SeaGreen] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

SpringGreen 春绿

```
\draw[color=SpringGreen] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=SpringGreen] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

___
##### 橙黄色

Apricot 杏黄色(未实现)

Bittersweet 苦与甜(未实现)

BurntOrange 焦橙色(未实现)

Dandelion 蒲公英(未实现)

Goldenrod 一枝黄

```
\draw[color=Goldenrod] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=Goldenrod] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

Melon 哈密瓜(未实现)

OrangeRed

```
\draw[color=OrangeRed] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=OrangeRed] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

Peach 桃色(未实现)

RawSienna 生赭色(未实现)

Sepia 棕褐色(未实现)

YellowGreen

```
\draw[color=YellowGreen] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=YellowGreen] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

YellowOrange(未实现)
___
##### 红粉色

BrickRed 砖红色(未实现)

CarnationPink 康乃馨(未实现)

Fuchsia 紫红色

```
\draw[color=Fuchsia] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=Fuchsia] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

Mahogany 红褐色(未实现)

Maroon 板栗色

```
\draw[color=Maroon] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=Maroon] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

RedViolet(未实现)

Rhodamine 罗丹红(未实现)

RubineRed 红宝石(未实现)

Salmon  鲑鱼粉

```
\draw[color=SkyBlue] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=Salmon] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

WildStrawberry 野草莓(未实现)

Mulberry 桑葚紫(未实现)

Orchid 兰花紫

```
\draw[color=Orchid] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=Orchid] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

Plum 梅子紫

```
\draw[color=Plum] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=Plum] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

Thistle 蓟花紫

```
\draw[color=Thistle] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=Thistle] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

Lavender 薰衣草(显示为白色)

```
\draw[color=Lavender] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=Lavender] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

___
##### 棕色

Tan 单宁棕

```
\draw[color=Tan] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=Tan] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

___
### 混合颜色

使用`!`可以混合颜色
```
color1!percentage!color2
```

比如`blue!30!cyan`表示30%蓝色和70%青色混合

```
\draw[color=blue!30!cyan] (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw[color=blue!30!cyan] (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

___
## 边

绘制边的命令是
```
\draw 起始点 to[对象类型=对象标签] 终止点;
```

如果仅使用to则绘制出一条导线

```
\draw (0,0) to (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[european]
	\draw (0,0) to (2,0);
\end{circuitikz}
\end{document}
```

方框里面也可以写short(短路)
表示一条导线

```
\draw (0,0) to[short] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw (0,0) to[short] (2,0);
\end{circuitikz}
\end{document}
```

还有open(开路)

```
\draw (0,0) to[open] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw (0,0) to[open,*-*] (2,0);
\end{circuitikz}
\end{document}
```

为了方便观察我先加了两个端点
___
### 端点

在绘制边的命令里面的方框可以加上这条边的端点设置

端点有

- 无端点(none)
- 方形端点:s,插件未实装
- 菱形端点:d
- 空心圆点:o
- 实心圆点:*

中间用`-`连接,可以混接,不能单独使用

```
\draw (0,0) to[R,o-o] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw (0,0) to[R,o-o] (2,0);
\end{circuitikz}
\end{document}
```

```
\draw (0,0) to[R,*-*] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw (0,0) to[R,*-*] (2,0);
\end{circuitikz}
\end{document}
```

```
\draw (0,0) to[R,d-d] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw (0,0) to[R,d-d] (2,0);
\end{circuitikz}
\end{document}
```


___
### 元件

常用的边对象有

电阻

```
\draw (0,0) to[R] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[european]
	\draw (0,0) to[R] (2,0);
\end{circuitikz}
\end{document}
```

___
电感

```
\draw (0,0) to[L] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}
	\draw (0,0) to[L] (2,0);
\end{circuitikz}
\end{document}
```

___
电容

```
\draw (0,0) to[C] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}
	\draw (0,0) to[C] (2,0);
\end{circuitikz}
\end{document}
```

___
电压源

```
\draw (0,0) to[V] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[european]
	\draw (0,0) to[V] (2,0);
\end{circuitikz}
\end{document}
```

___
电流源

```
\draw (0,0) to[I] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[european]
	\draw (0,0) to[I] (2,0);
\end{circuitikz}
\end{document}
```

___
干电池

这是单个干电池
```
\draw (0,0) to[battery1] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw (0,0) to[battery1] (2,0);
\end{circuitikz}
\end{document}
```

电池组
```
\draw (0,0) to[battery] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw (0,0) to[battery] (2,0);
\end{circuitikz}
\end{document}
```

还有另外一个电池
```
\draw (0,0) to[battery2] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw (0,0) to[battery2] (2,0);
\end{circuitikz}
\end{document}
```


___
受控电压源

```
\draw (0,0) to[cV] (2,0);
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
\ctikzset{voltage=european,current=european}
	\draw (0,0) to[cV] (2,0);
\end{circuitikz}
\end{document}
```

___
受控电流源

```
\draw (0,0) to[cI] (2,0);
```


```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
\ctikzset{voltage=european,current=european}
	\draw (0,0) to[cI] (2,0);
\end{circuitikz}
\end{document}
```

___
### 箭头

在边的绘制里面有箭头这种元素



___
## 点

绘制点的命令是
```
\draw node[对象类型](实例名称){标签} 点坐标
```

节点的类型和上面边的类型其实相同

- 无端点:none
- 实心圆点:circ
- 空心圆点:ocirc
- 实心菱形:diamondpole
- 空心菱形:odiamondpole
- 实心方框:squarepole
- 空心方框:osquarepole

```
\draw (0,0) node[circ]{};
\draw (1,0) node[ocirc]{};
\draw (0,0) node[diamondpole]{};
\draw (0,0) node[odiamondpole]{};
\draw (0,0) node[squarepole]{};
\draw (0,0) node[osquarepole]{};
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
\ctikzset{resistor=european}
	\draw (0,0) node[circ]{};
	\draw (1,0) node[ocirc]{};
	\draw (2,0) node[diamondpole]{};
	\draw (3,0) node[odiamondpole]{};
	\draw (4,0) node[squarepole]{};
	\draw (5,0) node[osquarepole]{};
\end{circuitikz}
\end{document}
```

___
### 元件

有些特殊的元件,它是以节点的形式绘制的


### 接地符号

接地符号也是以节点形式绘制的,关键词是ground,有多种接地符号

```
\draw (0,0) node[ground]{};
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (0,0) node[ground]{};
\end{circuitikz}
\end{document}
```

```
\draw (0,0) node[tlground]{};
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (0,0) node[tlground]{};
\end{circuitikz}
\end{document}
```

```
\draw (0,0) node[rground]{};
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (0,0) node[rground]{};
\end{circuitikz}
\end{document}
```

```
\draw (0,0) node[sground]{};
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (0,0) node[sground]{};
\end{circuitikz}
\end{document}
```

```
\draw (0,0) node[tground]{};
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (0,0) node[tground]{};
\end{circuitikz}
\end{document}
```

```
\draw (0,0) node[nground]{};
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (0,0) node[nground]{};	
\end{circuitikz}
\end{document}
```

```
\draw (0,0) node[pground]{};
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (0,0) node[pground]{};
\end{circuitikz}
\end{document}
```

```
\draw (0,0) node[cground]{};
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (0,0) node[cground]{};	
\end{circuitikz}
\end{document}
```

```
\draw (0,0) node[eground]{};
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (0,0) node[eground]{};
\end{circuitikz}
\end{document}
```

```
\draw (0,0) node[eground2]{};
```

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
	\draw (0,0) node[eground2]{};
\end{circuitikz}
\end{document}
```




