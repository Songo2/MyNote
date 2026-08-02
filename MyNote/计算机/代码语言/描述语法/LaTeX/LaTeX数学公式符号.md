
# 字体

正体 \mathrm    $\mathrm{A}$
斜体 \mathit    $\mathit{A}$
粗体 \mathbf    $\mathbf{A}$
花体 \mathcal    $\mathcal{A}$

___
# 希腊字母

## 小写

\alpha    $\alpha$
\beta   $\beta$
\gamma   $\gamma$
\delta    $\delta$
\epsilon    $\epsilon$
\zeta    $\zeta$
\eta    $\eta$
\theta    $\theta$
\iota    $\iota$
\kappa    $\kappa$
\lambda    $\lambda$
\mu    $\mu$
\nu    $\nu$
\xi    $\xi$
\omicron $\omicron$
\pi    $\pi$
\rho    $\rho$
\tau    $\tau$
\upsilon    $\upsilon$
\phi    $\phi$
\chi    $\chi$
\psi    $\psi$
\sigma    $\sigma$
\omega    $\omega$


## 大写

\Gamma   $\Gamma$
\Delta    $\Delta$
\Theta    $\Theta$
\Lambda    $\Lambda$
\Xi    $\Xi$
\Pi    $\Pi$
\Upsilon    $\Upsilon$
\Phi    $\Phi$
\Psi    $\Psi$
\Sigma    $\Sigma$
\Omega    $\Omega$


## 变体

\varepsilon    $\varepsilon$
\vartheta    $\vartheta$
\varpi    $\varpi$
\varrho    $\varrho$
\varsigma    $\varsigma$
\varphi    $\varphi$


# 空格
在LaTeX里普通空格被忽略,需要使用命令
小空格  \\,     $a \, b$
正常空格 \     $a \ b$
大空格 \quad    $a \quad b$
超大空格 \qquad    $a \qquad b$


# 省略号

\dots    $\dots$
\cdots    $\cdots$
\vdots    $\vdots$
\ddots    $\ddots$


# 修饰

长上划线 \overline{}    $\overline{a}$
下划线 \underline{}    $\underline{a}$
短下划线(平均值) \bar    $\bar{a}$
尖帽子(估计值) \hat{}    $\hat{a}$
波浪号 \tilde{}    $\tilde{a}$
一阶导数点 \dot    $\dot{a}$
二阶导数点 \ddot    $\ddot{a}$
上方 \overset{}{}    $\overset{2}{A}$
下方 \underset{}{}    $\underset{2}{A}$

# 自适应括号

在括号两边的前面加上\left和\right

圆括号 $() \quad \left( \int \right)$
方括号 $\{\} \quad \left\{ \int \right]$
花括号 $\{\} \quad \left\{ \int \right\}$


# 逻辑

\forall    $\forall$
\exists    $\exists$
\nexists    $\nexists$
\land    $\land$
\lor    $\lor$
\neg    $\neg$
\iff    $\iff$
\implies    $\implies$
\impliedby    $\impliedby$
\therefore    $\therefore$
\because    $\because$


# 关系

\le或\leq    $\le$
\ge或\geq    $\ge$
\ne或\neq    $\ne$
\approx    $\approx$
\equiv    $\equiv$
\sim    $\sim$
\simeq    $\simeq$
\propto    $\propto$
\ll    $\ll$
\gg    $\gg$
\subset    $\subset$
\supset    $\supset$
\subseteq    $\subseteq$
\supseteq    $\supseteq$
\in    $\in$
\notin    $\notin$
\ni    $\ni$


# 运算

\times    $\times$
\div    $\div$
\cdot    $\cdot$
\pm    $\pm$
\mp    $\mp$
\circ    $\circ$
\ast    $\ast$
\oplus    $\oplus$
\otimes    $\otimes$
\frac{}{}    $\frac{a}{b}$
\tfrac{}{}    $\tfrac{a}{b}$
\dfrac{}{}    $\dfrac{a}{b}$
\sqrt{}    $\sqrt{ a }$
\sqrt\[n]    $\sqrt[n]{ a }$


# 常用函数

\operatorname    $\operatorname{A}$

\sin    $\sin$
\cos    $\cos$
\tan    $\tan$
\cot    $\cot$
\sec    $\sec$
\csc    $\csc$
\arcsin    $\arcsin$
\arccos    $\arccos$
\arctan    $\arctan$

\ln    $\ln$
\log    $\log$

\exp    $\exp$


# 高等数学

\lim    $\lim$
\to    $\to$
\infty    $\infty$
\partial    $\partial$
\mathrm{d}    $\mathrm{d}$
\int    $\int$
\iint    $\iint$
\iiint    $\iiint$
\oint    $\oint$
\sum    $\sum$
\prod    $\prod$


# 集合

\mathbb{R}    $\mathbb{R}$
\mathbb{Z}    $\mathbb{Z}$
\mathbb{N}    $\mathbb{N}$
\mathbb{Q}    $\mathbb{Q}$
\mathbb{C}    $\mathbb{C}$
\varnothing    $\varnothing$
\cup    $\cup$
\cap    $\cap$


# 向量

\vec{a}    $\vec{a}$
\boldsymbol{a}    $\boldsymbol{a}$
\mathbf{a}   $\mathbf{a}$
\overrightarrow{a}   $\overrightarrow{a}$
\nabla    $\nabla$


# 环境

在数学块里,使用
\begin{}
...
\end{}
来使用一些环境

在环境里使用//来换行,使用&分隔

cases 方程组
$$
\begin{cases}
	A \\
	B \\
	C
\end{cases}
$$
align 右对齐
$$
\begin{align}
	AAA \\
	BB \\
	C
\end{align}
$$
gather 居中
$$
\begin{gather}
	AAA \\
	BB \\
	C
\end{gather}
$$
matrix 无括号矩阵
$$
\begin{matrix}
	A & B \\
	C & D
\end{matrix}
$$
pmatrix 圆括号矩阵
$$
\begin{pmatrix}
	A & B \\
	C & D
\end{pmatrix}
$$
bmatrix 方括号矩阵
$$
\begin{bmatrix}
	A & B \\
	C & D
\end{bmatrix}
$$
vmatrix 竖线矩阵(行列式)
$$
\begin{vmatrix}
	A & B \\
	C & D
\end{vmatrix}
$$
array 长矩阵
$$
\begin{array}{ll}
	A & B\\
	C & D
\end{array}
$$
本身有一个花括号用于对齐,但是在Obsidian里没效果c为居中,r为右对齐,l为左对齐

equation 编号
$$
\begin{equation}
	A
\end{equation}
$$
同样在Obsidian中不起作用