[TOC]
## Graphics Note

### Microfacet model

这里假设macrosurface的面积为$dA$，法向量为$\textbf{n}，$microsurface的面积为$dA^m$，法向量为$\textbf{m}$。入射方向为$\textbf{i}$，出射方向为$\textbf{o}$。定义Microfacet distribution function $D(\textbf{m}): \mathbb{R}^3 \to \mathbb{R}$，这是一个密度函数；定义Bidirectional shadowing-masking function $G(\textbf{i}, \textbf{o}, \textbf{m}): \mathbb{R}^3 \times \mathbb{R}^3 \times \mathbb{R}^3 \to \{0,1\}$
$$
dA^m = D(\textbf{m})G(\textbf{i}, \textbf{o},\textbf{m})d\omega_mdA
$$
这里列出$D(\textbf{m})$$的几条性质：
1. $D(\textbf{m})$是一个大于等于$0$的密度函数
$$
0 \leq D(\textbf{m}) \leq \infty 
$$
2. microsurface的面积和至与macrosurface一样大
$$
dA \leq \int D(\textbf{m})d\omega_w dA \Rightarrow 1 \leq \int D(\textbf{m})d\omega_m
$$
3. microsurface和macroface在某个方向上$\textbf{v}$的投影面积相同
$$
(\textbf{v}\cdot\textbf{n})dA = \int D(\textbf{m})(\textbf{v}\cdot\textbf{m})d\omega_m dA \Rightarrow (\textbf{v}\cdot\textbf{n}) = \int D(\textbf{m})(\textbf{v}\cdot\textbf{m})d\omega_m
$$

### BSDF
辐射照度定义：
$$
E = \frac{d\Phi}{A}
$$
辐射度定义:
$$
L = \frac{dE}{d\omega \cos{\theta}} = \frac{d^2\Phi}{dA d\omega \cos{\theta}}
$$

对于Macrosurface，在入射方向$\textbf{i}$和出射方向$\textbf{o}$分别有：
$$
\begin{gathered}
L_i =  \frac{d^2\Phi_i}{dA \cdot d\omega_i \cdot |\textbf{i}\cdot\textbf{n}|}\\\\
L_o =  \frac{d^2\Phi_o}{dA \cdot d\omega_o \cdot |\textbf{o}\cdot\textbf{n}|} = \frac{\rho(\textbf{i},\textbf{o})d^2\Phi_o}{dA d\omega_o \cdot |\textbf{o}\cdot\textbf{n}|}\\\\
E_i = L_i \cdot d\omega_i \cdot \left|\textbf{i}\cdot\textbf{n}\right|
\end{gathered}
$$
其中$\rho(\textbf{i},\textbf{o})$是Fresnell函数

根据BSDF的定义：
$$
\begin{aligned}
f_s(\textbf{i},\textbf{o}) & = \frac{dL_o}{dE_i}\\\\
&=\frac{\rho(\textbf{i},\textbf{o})\cdot d\Phi_i}{L_i \cdot dA\cdot d\omega_i \cdot d\omega_o \cdot |\textbf{i}\cdot\textbf{n}| \cdot |\textbf{o}\cdot\textbf{n}|}
\end{aligned}
$$

对于$L_i$，从microfacesurface上分析（面积为$dA^m$，法向量为$\textbf{m}$）可以得到
$$
L_i = \frac{d^2\Phi_i}{d\omega_i\cdot dA^m\cdot |\textbf{i}\cdot\textbf{m}|} = \frac{d^2\Phi_i}{d\omega_i\cdot D(\textbf{m})\cdot G(\textbf{i}, \textbf{o}, \textbf{m}) \cdot d\omega_m\cdot dA\cdot |\textbf{i}\cdot\textbf{m}|}
$$
带入上式可以得到
$$
f_s(\textbf{i},\textbf{o}) = \frac{|\textbf{i}\cdot\textbf{m}|}{|\textbf{i}\cdot\textbf{n}| \cdot |\textbf{o}\cdot\textbf{n}|} \cdot \rho(\textbf{i}, \textbf{o})\cdot D(\textbf{m}) \cdot G(\textbf{i}, \textbf{o}, \textbf{m}) \cdot \frac{d\omega_m}{d\omega_o}
$$