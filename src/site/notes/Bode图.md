---
{"dg-publish":true,"dg-path":"自动控制原理/Bode图.md","permalink":"/自动控制原理/Bode图/","dgPassFrontmatter":true,"noteIcon":"","created":"2024-05-21T15:20:27.724+08:00","updated":"2024-05-26T19:19:42.777+08:00"}
---

#图像 
***对数频率特性图：***
- **横坐标：**
	频率的[[对数分度\|对数分度]]   $\lg \omega$
- **纵坐标：**
	- 幅频特性：$L(\omega)=20\lg |G(j\omega)|$    单位： [[分贝\|dB]]
	- 相频特性：$\phi(\omega)=\angle G(j\omega)$           单位：$度^{\circ}$

### 基本画法

线性叠加

$$\begin{align}
G(s)&=\dfrac{K\prod\limits_{i=1}^{m}(\tau_{i}s+1)}{s^{v}\prod\limits_{i=1}^{n-v}(T_{i}s+1)} \\
G(j\omega )&=\dfrac{K\prod\limits_{i=1}^{m}(j\tau_{i}\omega +1)}{(j\omega )^{v}\prod\limits_{i=1}^{n-v}(jT_{i}\omega +1)}
\end{align}$$
关键求： 
$L(\omega)=20\lg |G(j\omega)|$
$\phi(\omega)=\angle G(j\omega)$

开环传函分解成各典型环节相串联
定转折频率，从小到大排列

了解[[经典环节的传递函数\|经典环节的传递函数]]的特性

dB/dec
（分贝每十倍）是一种用来描述增益或衰减随频率变化的单位
### Bode 图的增补
一般补画**对数相频特性**曲线
#### 起始点
在 [[Nyquist图\|Nyquist图]]中：
>从 $G(0^{+})$ 逆时针开始补画 $v\times 90^{\circ}$ ，半径为 $\infty$ 的顺时针圆弧

对应于 Bode 图中：
从 $\omega$ 较小，且 $L(\omega)>0$ 的点向上补画 $v\times 90^{\circ}$ 的一条虚直线


>[!tip] 注意
>而实际上，应该是由上往下移动，即沿着虚直线，$\phi(\omega)$ 辐角减小

#### 不连续的点 $\omega_{n}$
在 [[Nyquist图\|Nyquist图]]中：
>从 $G(j\omega_{n}^{-})$ 以半径为无穷大顺时针作 $v\times 180^{\circ}$ 的圆弧至 $G(j\omega_{n}^{+})$

对应于 Bode 图中：
从 $\phi(\omega^{-})$ 点向上/或下（取决于突变的方向）补作 $v\times 180^{\circ}$ 的虚直线至 $\phi(\omega^{+})$ 处



