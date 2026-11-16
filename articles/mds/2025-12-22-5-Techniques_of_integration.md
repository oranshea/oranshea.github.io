本文为笔者整理的[MIT18.01SC](https://ocw.mit.edu/courses/18-01sc-single-variable-calculus-fall-2010/)关于积分技巧的知识内容
收录整理了课程中关于积分的一些基本技巧, 求解面积体积弧长等部分没有收入.*

# Part A: Trigonometric Powers, Trigonometric Substitution and Com / 关于三角幂 三角代换

## 基本恒等变换公式

下文中我们将用到
1. 
    $$
    \sin^2x + \cos^2x = 1
    $$

2. half-angle identites* / 半角恒等式
    $$
    \sin(2x) = 2\sin(x)\cos(x)
    $$
    $$
    \cos(2x) = \cos^2(x) - \sin^2(x)
    $$

以及常用的两个变形

$$
\cos^2x = \frac{1 + \cos(2x)}{2}
$$

$$
\sin^2x = \frac{1 - \cos(2x)}{2}
$$

## $\int\sin(x^n)\cos(x^m) \, dx$

关于这个积分, 分为两种情况: 
* easy case
* harder case

### 1. easy case
所谓easy case, 就是指数n, m至少有一个奇数.

我们运用换元法(这里是凑微分法)和$\sin^2(x) + \cos^2(x) = 1$进行恒等变化, 过程就会变得顺利. 

思考一下, 当我们把具有奇数指数的因式拆开并凑微分后, 指数变为偶数, 很容易地根据恒等变化进行转换(转换为和微分算子一致), 从而换元. ~~轻松解决问题~~

下面是一个例子(*摘自MIT18.01SC*):

$$
\begin{aligned}
\int \cos^3(2x) \, dx &= \frac{1}{2} \int \cos^3(u) \, du \quad (u = 2x) \\
&= \frac{1}{2} \int \cos^2(u) \cos(u) \, du \\
&= \frac{1}{2} \int (1 - \sin^2(u)) \cos(u) \, du \\
&= \frac{1}{2} \int (1 - v^2) \, dv \quad (v = \sin u) \\
&= \frac{1}{2} \left( v - \frac{1}{3} v^3 + c \right) \\
&= \frac{1}{2} \left( \sin(2x) - \frac{1}{3} \sin^3(2x) + c \right) \\
\int \cos^3(2x) \, dx &= \frac{1}{2} \sin(2x) - \frac{1}{6} \sin^3(2x) + C.
\end{aligned}
$$

### 2. hard case
当指数n, m都为偶数, 问题更加难解决. 

无论我们怎么凑微分, 总存在奇数因式, 我们无法像easy case中运用$\sin^2(x) + \cos^2(x) = 1$将剩余的因数统一转换为包含微分算子的式子.

因此我们使用
$$
\cos^2(x) = \frac{1 + \cos(2x)}{2}
$$

$$
\sin^2(x) = \frac{1 - \cos(2x)}{2}
$$

来进行降幂操作

如下例子(*摘自MIT18.01SC*):

$$
\int \sin^{4} x \cos^{2} x \, dx 
$$

先进行降幂操作

$$
\begin{aligned}
\sin^{4} x \cos^{2} x &= (\sin^{2} x)^{2} \cos^{2} x \\
&= \left( \frac{1 - \cos(2x)}{2} \right)^{2} \left( \frac{1 + \cos(2x)}{2} \right) \\
&= \left( \frac{1 - 2\cos(2x) + \cos^{2}(2x)}{4} \right) \left( \frac{1 + \cos(2x)}{2} \right) \\
&= \frac{1 - 2\cos(2x) + \cos^{2}(2x) + \cos(2x) - 2\cos^{2}(2x) + \cos^{3}(2x)}{8} \\
&= \frac{1 - \cos(2x) - \cos^{2}(2x) + \cos^{3}(2x)}{8}
\end{aligned}
$$

带入恒等变化的结果

$$
\begin{aligned}
\int \sin^{4} x \cos^{2} x \, dx &= \int \frac{1 - \cos(2x) - \cos^{2}(2x) + \cos^{3}(2x)}{8} \, dx \\
\end{aligned}
$$

同样操作再对$\cos^{2}(2x)$和$\cos^{3}(2x)$进行降幂操作. 这里给出结果:

$$
\begin{aligned}
\int \cos^{2}(2x) \, dx &= \frac{x}{2} + \frac{\sin(2x)}{4} + c_{1} \\
\int \cos^{3}(2x) \, dx &= \frac{1}{2} \sin(2x) - \frac{1}{6} \sin^{3}(2x) + c_{2}
\end{aligned}
$$

直到每一项都是1次的, 积分变得简单.

$$
\begin{aligned}
\int \sin^{4} x \cos^{2} x \, dx &= \int \frac{1 - \cos(2x) - \cos^{2}(2x) + \cos^{3}(2x)}{8} \, dx \\
&= \frac{1}{8} \left[ x - \frac{1}{2} \sin(2x) - \left( \frac{x}{2} + \frac{\sin(2x)}{4} + c_1 \right) \right. \\
&\quad \left. + \left( \frac{1}{2} \sin(2x) - \frac{1}{6} \sin^{3}(2x) + c_2 \right) \right] \\
&= \frac{1}{8} \left[ \frac{x}{2} - \frac{\sin(2x)}{4} - \frac{1}{6} \sin^{3}(2x) \right] + C \\
&= \frac{x}{16} - \frac{\sin(2x)}{32} - \frac{\sin^{3}(2x)}{48} + C
\end{aligned}
$$

## 一些三角换元

这部分相信各位已经都熟悉, 仅仅作出总结,
下表列出了不同的三角代换方法及其用途：

| 如果积分式中包含 (If your integrand contains) | 进行代换 (Make substitution)               | 得到结果 (To get)                  |
| :-------------------------------------------- | :----------------------------------------- | :--------------------------------- |
| $\sqrt{a^2 - x^2}$                            | $x = a \cos \theta$ 或 $x = a \sin \theta$ | $a \sin \theta$ 或 $a \cos \theta$ |
| $\sqrt{a^2 + x^2}$                            | $x = a \tan \theta$                        | $a \sec \theta$                    |
| $\sqrt{x^2 - a^2}$                            | $x = a \sec \theta$                        | $a \tan \theta$                    |

## 配方法

对于被积函数包含了一个根号下的二项式, 我们通常选择进行配方.

如$\int\frac{1}{\sqrt{x^2 + 4x}}\,dx$, 作如下转换:

$$
\int \frac{dx}{\sqrt{x^2 + 4x}} = \int \frac{dx}{\sqrt{(x + 2)^2 - 4}}
$$

配方过程我们可以使用对比系数法.

$$
x^2 + 4x = (x + a)^2 +  b = x^2 + 2ax + a^2 + c
$$

可得 $a = 2, c = -4$

配方完我们就可以使用二中的三角换元表格来进行换元了.

# Part B: Partial Fractions, Integration by Parts, Arc Length, and Surface Area

## Partial Fractions
也就是将有理函数$\frac{P(x)}{Q(x)}$拆分为几个简单的式子, 然后对各个式子积分.如下.

$$
\int\frac{4x - 1}{x^2 + x - 2}\leftrightarrow \int(\frac{1}{x - 1} + \frac{3}{x +2}) \, dx
$$

## Cover-up Method
Cover-up Method是一个将复杂的有理分式转换为部分分式的方法.在此举例说明.

假设我们要分解：

$$
\frac{x+3}{(x-1)(x+2)} = \frac{A}{x-1} + \frac{B}{x+2}
$$

**第一步**：求 $A$ (对应分母为 $x-1$)遮住左边分母中的 $(x-1)$。令 $x-1 = 0 \Rightarrow \mathbf{x = 1}$。将 $x=1$ 代入剩余部分：

$$
A = \left. \frac{x+3}{\square \cdot (x+2)} \right|_{x=1} = \frac{1+3}{1+2} = \frac{4}{3}
$$

**第二步**：求 $B$ (对应分母为 $x+2$)遮住左边分母中的 $(x+2)$。令 $x+2 = 0 \Rightarrow \mathbf{x = -2}$。将 $x=-2$ 代入剩余部分：

$$
B = \left. \frac{x+3}{(x-1) \cdot \square} \right|_{x=-2} = \frac{-2+3}{-2-1} = \frac{1}{-3} = -\frac{1}{3}
$$

**结果**：

$$
\frac{x+3}{(x-1)(x+2)} = \frac{4/3}{x-1} - \frac{1/3}{x+2}
$$

### 1.适用范围与局限性

 **最适用**: 分母全是互不相同的线性因子，如 $(x-a)(x-b)(x-c)$。

 **限制**: 如果分母有重复因子（如 $(x-1)^2$），Cover-up 只能求出*最高次幂的系数*。如果分母有不可约二次因式（如 $x^2+1$），通常需要结合代入法或系数比较法。
 对比系数应该都比较熟悉, 这里不再赘述.

### 2.如何理解

这是笔者本人思考

$$
\frac{x+3}{(x-1)(x+2)} = \frac{A}{x-1} + \frac{B}{x+2}
$$

对于上等式, 遮住$x - 1$实际就是两边同乘$x - 1$, 带入$x = 1$自然就能得到A, 同理也能解释为什么分母有重复因子只能求出其最高次幂的系数.

$$
\frac{x+3}{(x+2)} = \frac{A}{x-1}(x - 1) + \frac{B}{x+2}(x - 1)
$$

对于系数比较多的, 这种方法还是比较快的. [点这里](/assets/pdf/Cover-Up_MIT18_01SCF10_Ses74c.pdf)查看原文介绍.

对于因式分解, 这里介绍[长除法](/assets/pdf/long_division_MIT18_01SCF10_Ses75c.pdf), 相信大家都已经会使用.

对于Partial Fractions, [这里](/assets/pdf/partial_frac_big_example_MIT18_01SCF10_Ses75d.pdf)有个总结.

## Integration by Part 分部积分法
相信大家都会, 基本公式: 

$$
\int u \,dv =  uv - \int v \,du
$$

通过分部积分我们能求得

$$
\int \ln x = x \ln x -  x + C
$$

### Reduction Formula
那么$\int \ln^n x \, dx$呢?

通过分部积分我们可以得到

$$
\int \ln^n x \, dx= x \ln x - n\int (\ln x)^{n -1} \, dx
$$

可以写作$F_n(x) = x \ln x - nF_{n-1}(x)$, 我们称为reduction .formula

使用这个公式我们可以计算$\int \ln^n x \, dx$

这里再介绍另外一个reduction formula

$$
\int x^n e^{ax} \, dx = \frac{1}{a} x^n e^{ax} - \frac{n}{a} \int x^{n-1} e^{ax} \, dx
$$

其实这些公式可以使用一次分部积分来现推, 不用花费功夫去记忆.

(这里我推荐使用[表格积分法](#表格分部积分法-tabular-integration-by-parts), 一种分部积分技巧, 下文为, 维基百科翻译内容, 笔者~~AI~~翻译而来)

## 表格分部积分法 (Tabular Integration by Parts)

表格法（Tabular Method）是分部积分公式的简化形式，能够将复杂的重复积分过程总结在一个表格中。该方法因 1988 年的电影《立志凌云》（*Stand and Deliver*）而广为人知。

---

### 1. 基本原理
对于积分 $\int u \cdot v \, dx$，我们通过不断对 $u$ 求导，对 $v$ 积分来构造表格。

**示例 1：幂函数与三角函数组合
**
计算积分：

$$
\int x^3 \cos x \, dx
$$

**步骤说明：**
* 令 $u^{(0)} = x^3$（作为要求导的部分）。
* 令 $v^{(n)} = \cos x$（作为要积分的部分）。

**构造表格：**

| $i$  | 符号 (Sign) | A: 导数 $u^{(i)}$ | B: 积分 $v^{(n-i)}$ |
| :--- | :---------- | :---------------- | :------------------ |
| 0    | +           | $x^3$             | $\cos x$            |
| 1    | −           | $3x^2$            | $\sin x$            |
| 2    | +           | $6x$              | $-\cos x$           |
| 3    | −           | $6$               | $-\sin x$           |
| 4    | +           | $0$               | $\cos x$            |



**结果组合：**
将第 $j$ 行的 A 项与第 $j+1$ 行的 B 项相乘，并应用对应的符号。

$$
\begin{aligned}
\int x^3 \cos x \, dx &= (+1)(x^3)(\sin x) + (-1)(3x^2)(-\cos x) \\
&\quad + (+1)(6x)(-\sin x) + (-1)(6)(-\cos x) + C \\
&= x^3 \sin x + 3x^2 \cos x - 6x \sin x - 6\cos x + C
\end{aligned}
$$

---

### 2. 特殊情况：循环积分 (Recurring Integrals)
当导数项不会变成 0，但导数与积分的乘积出现了原始被积函数的倍数时，可以停止计算。这种情况常见于指数函数与三角函数的乘积。

**示例 2：指数函数与三角函数
**
计算积分：

$$
\int e^x \cos x \, dx
$$

| $i$  | 符号 (Sign) | A: 导数 $u^{(i)}$ | B: 积分 $v^{(n-i)}$ |
| :--- | :---------- | :---------------- | :------------------ |
| 0    | +           | $e^x$             | $\cos x$            |
| 1    | −           | $e^x$             | $\sin x$            |
| 2    | +           | $e^x$             | $-\cos x$           |

**观察：** 第 $i=2$ 行的 $A \times B$ 乘积（考虑符号）为 $\int e^x (-\cos x) dx$，这正是原始被积函数的负数。

**推导过程：**

$$
\int e^x \cos x \, dx = \underbrace{(+1)(e^x)(\sin x)}_{j=0} + \underbrace{(-1)(e^x)(-\cos x)}_{j=1} + \int \underbrace{(+1)(e^x)(-\cos x)}_{i=2} \, dx
$$


**整理得：**

$$
\begin{aligned}
\int e^x \cos x \, dx &= e^x \sin x + e^x \cos x - \int e^x \cos x \, dx \\
2 \int e^x \cos x \, dx &= e^x (\sin x + \cos x) + C' \\
\int e^x \cos x \, dx &= \frac{1}{2} e^x (\sin x + \cos x) + C
\end{aligned}
$$


---

### 3. 记忆要点
* **A 列选择：** 选容易求导至 0 的项（通常是多项式）。
* **B 列选择：** 选容易积分且不会消失的项。
* **连线规则：** 始终是“左上”连“右下”进行乘积。
* **水平行：** 如果在某一行停止（未到 0），该行的水平乘积必须放在积分号 $\int$ 内。

---

*Part B余下内容 以及 Part C内容, 课程中为求面积体积弧长, 以及极坐标和参数方程, 不再收录*

 
