
# 特定名称颜色(dvipsnames)

给xcolor包的dvipsnames打开能有一系列特定名称的经典颜色,基于CMYK,是印刷行业的标准
\usepackage[dvipsnames]{xcolor}
这在circuitikz也是默认开启的

它会在xcolor的基础上加入49种颜色
___
## 颜色列表

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
## 颜色展示

### 蓝紫色

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
### 绿色

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
### 橙黄色

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
### 红粉色

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
### 棕色

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
