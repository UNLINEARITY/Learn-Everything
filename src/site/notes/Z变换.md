---
{"dg-publish":true,"dg-path":"变换/Z变换.md","tags":["Transform","Discrete"],"permalink":"/变换/Z变换/","dgPassFrontmatter":true,"noteIcon":"","created":"2024-05-21T15:20:27.861+08:00","updated":"2025-03-03T12:15:01.996+08:00"}
---

(terminology::**Z-Transform**)
**离散时间信号处理**中的一个重要数学工具，由连续时间信号处理中的[[拉普拉斯变换\|拉普拉斯变换]]引申出来的变换方法
对于[[信号采样\|采样信号]]  $e^{*}(t)$
$$\begin{align}
e^{*}(t)&=\sum\limits_{n=0}^{\infty} e(nT)\delta(t-nT) \\
E^{*}(s)&=\mathscr{L}[e^{*}(t)]=\sum\limits_{n=0}^{\infty} e(nT)e^{ -nsT }
\end{align}$$

令 $z=e^{ sT }$，将 $s$ 的超越函数转化为 $z$ 的[[幂级数\|幂级数]]或 $z$ 的有理分式
$$\begin{align}
\large z=e^{ sT }
\end{align}$$

$$\begin{align}
E(z)=\mathscr{Z}[e^{*}(t)]=\sum\limits_{n=0}^{\infty} e(nT)z^{-n}
\end{align}$$

### z 变换方法
#### 1.级数求和法
根据定义写为[[级数\|级数]]展开形式

$$\begin{align}
E(z)=e(0)+e(T)z^{-1}+e(2T)z^{-2}+\cdots+e(nT)z^{-n}
\end{align}$$

若 $e(t)=1(t)$
$e^{*}(t)=\sum\limits_{n=0}^{\infty} \delta(t-nT)$
$E^{*}(s)=\sum\limits_{n=0}^{\infty} e^{-nTs}\to E(z)=\sum\limits_{n=0}^{\infty}z^{-n}$
$$\begin{align}
\sum\limits_{n=0}^{\infty}z^{-n}= \dfrac{1}{1-z^{-1}}= \dfrac{z}{z-1}
\end{align}$$

#### 2. 部分分式法
先求**已知连续函数的拉氏变换**  $E(s)$
将有理分式 $E(s)$ 展开为**部分分式之和**的形式
### z 变换的性质
#### 1. 线性定理
z 变换是一种[[线性变换\|线性变换]]，满足齐次性与均匀性
$$\begin{align}
\mathscr{Z}[ae(t)]&=aE(z) \\
\mathscr{Z}[e_{1}(t)\pm e_{2}(t)]&=E_{1}(z)\pm E_{2}(z)
\end{align}$$

#### 2. 实数位移定理
==**实数位移:**==
整个采样序列在时间轴上左右平移若干个采样序列
- 向左平移为**超前**
- 向右平移为**滞后**

$$\begin{align}
\mathscr{Z}[e(t-kT)]&=z^{-k}E(z) \\
\mathscr{Z}[e(t+kT)]&=z^{k}\left[E(z)-\sum\limits_{n=0}^{k-1}e(nT)z^{-n}\right]
\end{align}$$

实数位移定理相当于[[拉普拉斯变换\|拉普拉斯变换]]的微分与积分定理
可将[[差分方程\|差分方程]]转换为 z 域的代数方程
#### 3. 复数位移定理
$$\begin{align}
\mathscr{Z}[e^{ \mp at }e(t)]=E(ze^{ \pm aT })
\end{align}$$
#### 4. 终值定理

$$\begin{align}
\lim\limits_{ n \to \infty } e(nT)=\lim\limits_{ z \to 1 } (z-1)E(z)
\end{align}$$

#### 5. 卷积定理
[[卷积\|卷积]]

$$\begin{align}
x(nT)*y(nT)=\sum\limits_{k=0}^{\infty}x(kT)y\left[(n-k)T\right]
\end{align}$$

$$\begin{align}
g(nT)&=x(nT)*y(nT) \\
G(z)&=X(z)Y(z)
\end{align}$$

### z 变换的应用
Z 变换将一个离散时间信号（或系统）从时域转换到 Z 域，即复频域
在 Z 域中，可以更容易地分析系统的稳定性和频率特性，也可以用来求解线性时不变（LTI）系统的差分方程。

Z 变换有一些重要的性质和定理，例如线性性质、时移性质、尺度变换性质、初值定理和终值定理等。利用这些性质，可以简化对离散时间信号和系统的分析。

Z 变换在数字信号处理中有着广泛的应用，如系统设计、滤波器设计、信号谱分析等。通过 Z 变换，可以将复杂的差分方程转换为简单的代数方程来求解，从而大大简化了计算过程。

