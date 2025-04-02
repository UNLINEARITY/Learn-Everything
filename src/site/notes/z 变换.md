---
{"dg-publish":true,"dg-path":"变换/z 变换.md","tags":["Transform","Discrete"],"permalink":"/变换/z 变换/","dgPassFrontmatter":true,"noteIcon":"","created":"2024-05-21T15:20:27.000+08:00","updated":"2025-03-31T23:33:43.085+08:00"}
---


(terminology::**Z-Transform**)
**离散时间信号处理**中的一个重要数学工具，在[[信号采样\|信号采样]]的基础上，由连续时间信号处理中的[[拉普拉斯变换\|拉普拉斯变换]]引申出来的变换方法。（将 $s$ 的超越函数转化为 $z$ 的[[幂级数\|幂级数]]或 $z$ 的有理分式）

### 一、z 变换定义
1. 采样信号 $e^{*}(t)$ 的时域表达：
$$\begin{align}
e^{*}(t)&= e(t)\delta _{T}(t)=\sum\limits_{n=0}^{\infty} e(nT)\delta(t-nT)
\end{align}$$
2. 采样信号的拉普拉斯变换为：
$$\begin{align}
E^{*}(s)&=\mathscr{L}[e^{*}(t)]=\sum\limits_{k=0}^{\infty} e(nT)e^{ -ksT }
\end{align}$$
3. 令 $\large z=e^{ sT }$，得到 z 变换：
$$\begin{align}
E(z)=\mathscr{Z}[e(t)] =\mathscr{Z}[e^{*}(t)]=\sum\limits_{k=0}^{\infty} e(nT)z^{-k}
\end{align}$$
$\mathscr{Z}$ 表示取 z 变换，习惯上称 $E(z)$ 是采样信号的 z 变换。


### 二、常见函数的 z 变换


|    时间函数     |        拉普拉斯变换         |           z 变换           |
| :---------: | :-------------------: | :----------------------: |
| $\delta(t)$ |          $1$          |           $1$            |
|   $1(t)$    |    $\dfrac{1}{s}$     |     $\dfrac{z}{z-1}$     |
|     $t$     |  $\dfrac{1}{s^{2}}$   | $\dfrac{Tz}{(z-1)^{2}}$  |
| $e^{ -at }$ |   $\dfrac{1}{s+a}$    | $\dfrac{z}{z-e^{ -aT }}$ |
|  $b^{t/T}$  | $\dfrac{T}{Ts-\ln b}$ |     $\dfrac{z}{z-b}$     |


$$\begin{align}
\mathscr{Z}[\delta(t)] & =\sum\limits_{k=0}^{\infty} \delta(kT)z^{-k}=1 \\
\mathscr{Z}(1) & = \sum\limits_{k=0}^{\infty} 1\cdot z^{-n}=  1+ z^{-1}+z^{-2}+\cdots =\dfrac{1}{1-z^{-1}} = \dfrac{z}{z-1} \\
\mathscr{Z}[t] &  =\sum\limits_{k=0}^{\infty} (kT)z^{-k}=   0+Tz^{-1}+2Tz^{-2}+ \cdots =\dfrac{Tz^{-1}}{(1-z^{-1})^{2}}\\
 \mathscr{Z}[e^{-at}] & =\sum\limits_{k=0}^{\infty} e^{ -akT }z^{-k}= 1+e^{ -aT }z^{-1}+ e^{  -2aT}z^{-2}+\cdots =  \dfrac{1}{1-e^{ -aT }z^{-1}} \\
\mathscr{Z}[b^{t/T}] & =\sum\limits_{k=0}^{\infty} b^{k}z^{-k}=1 + bz^{-1}+b^{2}z^{-2}+\cdots = \dfrac{1}{1-bz^{-1}}
\end{align}$$


### 三、z 变换方法
#### 1.级数求和法
根据定义写为级数展开形式，根据级数知识得到最终表达式
$$\begin{align}
E(z)=  \sum\limits_{k=0}^{\infty} e(kT)z^{-k} =e(0)+e(T)z^{-1}+e(2T)z^{-2}+\cdots+e(kT)z^{-k}+\cdots 
\end{align}$$
#### 2. 部分分式法
先求**已知连续函数的拉氏变换**  $E(s)$ ，将有理分式 $E(s)$ 展开为**部分分式之和**的形式，对每个部分分式进行 z 变换。（展开为部分分式重要的是用[[留数\|留数]]来求系数 $c_{i}$）
$$\begin{align}
F(s)= \sum\limits_{i=1}^{n} \dfrac{c_{i}}{s-p_{i}}\quad \Rightarrow \quad F(z)=\sum\limits_{i=1}^{n} \dfrac{c_{i}}{1-e^{ p_{i}T }z^{-1}}
\end{align}$$

### 四、z 变换的性质
#### 1. 线性定理
z 变换是一种[[线性变换\|线性变换]]，满足齐次性与均匀性
$$\begin{align}
\mathscr{Z}[ae(t)]&=aE(z) \\
\mathscr{Z}[e_{1}(t)\pm e_{2}(t)]&=E_{1}(z)\pm E_{2}(z)
\end{align}$$

#### 2. 实数位移定理
**实数位移**：整个采样序列在时间轴上左右平移若干个采样序列（**左加右减**）
实数位移定理相当于[[拉普拉斯变换\|拉普拉斯变换]]的微分与积分定理，可将[[差分方程\|差分方程]]转换为 z 域的代数方程
- 向右平移为**滞后**
$$\begin{align}
\mathscr{Z}[f(kT-mT)]&=z^{-m}F(z) \; {\color{red}\Rightarrow} \; \mathscr{Z}[f(k-m)]=z^{-m}F(z)
\end{align}$$

根据 $k-m=n \quad \quad n<0,f(t)=0 \quad \Rightarrow \quad f(nT)=0$，有：
$$\begin{align}
\mathscr{Z}[f(kT-mT)] & =\sum\limits_{k=0}^{\infty} f(kT-mT)z^{-k}  = \sum\limits_{n=-m}^{\infty} f(nT)z^{-(n+m)} \\
 & =z^{-m}\left(\sum\limits_{n=0}^{\infty}f(nT)z^{-n}+ \sum\limits_{n=-m}^{-1}f(nT)z^{-n}\right) \\
 & =z^{-m}F(z)
\end{align}$$


- 向左平移为**超前**
$$\begin{align}
\mathscr{Z}[f(kT+mT)]&=z^{m}\left[F(z)-\sum\limits_{n=0}^{m-1}f(nT)z^{-n}\right]
\end{align}$$
令 $k+m=n$，得到：
$$\begin{align}
\mathscr{Z}[f(kT+mT)] & =\sum\limits_{k=0}^{\infty} f(kT+mT)z^{-k}  =\sum\limits_{n=m}^{\infty} f(nT)z^{-(n-m)} \\
 & = z^{m} \left(\sum\limits_{n=0}^{\infty} f(nT)z^{-n} -\sum\limits_{n=0}^{m-1}f(nT)z^{-n}\right) \\
 & = z^{m}\left( F(z)- \sum\limits_{n=0}^{m-1}f(nT)z^{-n} \right)
\end{align}$$


#### 3. 复数位移定理
$$\begin{align}
\mathscr{Z}[e^{ \mp at }e(t)]=E(ze^{ \pm aT })
\end{align}$$


#### 4. 极限定理
初值定理：
$$\begin{align}
f(0)= \lim\limits_{ n \to 0 } e(nT)= \lim\limits_{ z \to \infty } E(z) 
\end{align}$$

终值定理：
$$\begin{align}
f(\infty)=\lim\limits_{ n \to \infty } e(nT)=\lim\limits_{ z \to 1 } (z-1)E(z)
\end{align}$$

> **注意终值定理的使用条件： 如果不稳定，不能直接使用**
 
#### 5. 卷积定理
[[卷积\|卷积]]
$$\begin{align}
x(nT)*y(nT)=\sum\limits_{k=0}^{\infty}x(kT)y\left[(n-k)T\right]
\end{align}$$

$$\begin{align}
g(nT)&=x(nT)*y(nT) \\
G(z)&=X(z)Y(z)
\end{align}$$

