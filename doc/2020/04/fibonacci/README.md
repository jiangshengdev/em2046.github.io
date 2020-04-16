# 斐波那契数列时间复杂度计算

想要计算斐波那契数列的时间复杂度需要先了解斐波那契数列的定义与算法。

## 定义

在数学中，斐波那契数（Fibonacci number），一般使用 $F_{n}$ 表示，构成序列后，称之为斐波那契数列（Fibonacci sequence），序列中每一个数字都是前面两个数字的和，从 0 和 1 开始。定义如下，

> $$F_{0}=0,\quad F_{1}=1,$$
>
> $$F_{n}=F_{n-1}+F_{n-2},\quad n>1$$

序列起始位置的值为：

> $$0,\;1,\;1,\;2,\;3,\;5,\;8,\;13,\;21,\;34,\;55,\;89,\;144,\;\dots$$

为了方便查阅，使用表格列出，前 13 位斐波那契数 $F_{n}$ 为：

| $F_{0}$ | $F_{1}$ | $F_{2}$ | $F_{3}$ | $F_{4}$ | $F_{5}$ | $F_{6}$ | $F_{7}$ | $F_{8}$ | $F_{9}$ | $F_{10}$ | $F_{11}$ | $F_{12}$ |
| ------- | ------- | ------- | ------- | ------- | ------- | ------- | ------- | ------- | ------- | -------- | -------- | -------- |
| 0       | 1       | 1       | 2       | 3       | 5       | 8       | 13      | 21      | 34      | 55       | 89       | 144      |

## 算法

不同的算法，时间复杂度可能有着明显的差异。对于斐波那契数列，常见的算法有递归法与迭代法。

### 递归版

参考定义可以直接得出递归版本的算法，使用 JavaScript 语言描述如下，

```javascript
function fibonacci(n) {
  if (n < 2) {
    return n;
  } else {
    return fibonacci(n - 1) + fibonacci(n - 2);
  }
}

console.log(fibonacci(40));
```

接下来将对此算法进行时间复杂度的分析。

#### 算法分析

对于一个算法的复杂度分析，通常关注的是随着问题规模的增长，计算成本如何增长。更加关心**足够大**的问题，注重考查计算成本的增长趋势。当输入的 n 足够大之后，将算法需执行的基本操作次数定义为 $T(n)$，需占用的存储单元数定义为 $S(n)$。分析时一般忽略空间复杂度，只考虑时间复杂度。

可以使用大 O 符号（$O$）描述算法的时间复杂度，定义 $T(n)=O(f(n))， T(n)<c f(n)$ ，其中 $c$ 为常数，$O(f(n))$ 表示计算成本的上界，也即是算法在最坏的情况下需执行的基本操作次数。与 $T(n)$ 相比，$f(n)$ 更加简洁，但依然反映前者的增长趋势。对于上界而言，有两条规则如下，

常系数可忽略：

> $O(f(n))=O(c\cdot f(n))$

低次项可忽略：

> $O(n^{a}+n^{b})=O(n^{a}), a>b>0$

算法的时间复杂度可以分类为高效解、有效解、难解。

##### 高效解

常数复杂度 $O(1)\;$，对数复杂度 $O(\log^{c}n)$。

不管常数是多少，都可以看作一样：

> $$O(1) = 2 = 2020 = 2020^2$$

常底数可忽略：

> $$\forall\quad a,b>0,\quad \log_{a}n=\log_ab\cdot\log_bn=O(\log_{b}n)$$

常数次幂可忽略：

> $$\forall\quad c>0,\quad \log n^{c}=c\cdot\log n=O(\log n)$$

对数多项式可忽略次数较低者：

> $$\log^{2020}n+\log^{2019}n=O(\log^{2020}n)$$

##### 有效解

多项式复杂度 $O(n^c)$。

多项式中常系数与低次项可忽略：

> $$2020n+2020=O(n)$$
>
> $$(n)\times(n^{2}-n)=O(n \times n^2) = O(n^{3})$$
>
> $$(2020n^{2}-2020)/(2020n)=O(n^{2}/n)=O(n)$$
>
> $$a_{k}n^{k}+a_{k-1}n^{k-1}+\dots+a_{1}n+a_{0}=O(n^{k}),\quad a_{k}>0$$

##### 难解

指数复杂度 $O(2^{n})。$

对于所以的多项式复杂度，都会被 2 的指数复杂度覆盖。当 n 足够大时 $2^{n}$ 总会大于 $n^{c}$，比如当 n 为 10 时，$2^{n}\rightarrow 2^{10}$ 就已经大于 $n^{3}\rightarrow 10^{3}$ 了。

> $\forall\quad c>1,\quad n^{c}=O(2^{n})$

这类算法的计算成本增长极快，通常被认为是不能忍受的。

JavaScript 等高级语言的**基本指令**，均等效于常数条 RAM 的**基本指令**。在渐进的意义下，二者大体相当。

对于递归算法可以使用递归跟踪或者递推方程的方式计算出算法的复杂度。

#### 递推方程

根据递归算法列出时间复杂度的递推方程如下，

$$
T(n)=T(n-1)+T(n-2)+1,\quad n>1
 \label{recursion1}
$$

$$
T(0)=1
 \label{recursion2}
$$

$$
T(1)=1
 \label{recursion3}
$$

上式中 $+1$, $=1$ 中的 $1$ 均为时间复杂度。根据递归版代码中的第二个判断分支，计算 $T(n)$ 需要先计算出第 $n-1$ 位与 $n-2$ 位的结果然后求和，所以等式右边为计算 $n-1$ 位所需时间 $T(n-1)$ 加上计算 $n-2$ 位所需时间 $T(n-2)$ 再加上求和时间 1。下面两行等式 $\ref{recursion2}$ 与 $\ref{recursion3}$ 为递归基，均为 1 的时间复杂度。

为了求解这样一个递推式，我们不妨设置一个 $S(n)$，

**令**

$$
S(n)=[T(n)+1]/2
 \label{recursion4}
$$

**则**

$$
 S(0)=1=fib(1),\quad S(1)=1=fib(2)
 \label{recursion5}
$$

**故**

$$
 S(n)=S(n-1)+S(n-2)=fib(n+1)
 \label{recursion6}
$$

其中 $fib$ 为 fibonacci 的简写，详细计算过程如下，

**$S(0)$ 计算过程**

> 将 $n=0$ 代入等式 $\ref{recursion4}$ 中
>
> $S(0)=[T(0)+1]/2$
>
> 其中$T(0)$的值可以查看等式 $\ref{recursion2}$
>
> $S(0)=(1+1)/2$
>
> $S(0)=1$
>
> 查阅定义中的表格中 $F_{1}$ 的值为 $1$
>
> $S(0)=fib(1)$

**$S(1)$ 计算过程**

> 将$n=1$带入等式 $\ref{recursion4}$ 中
>
> $S(1)=[T(1)+1]/2$
>
> 其中$T(1)$的值可以查看等式 $\ref{recursion3}$
>
> $S(1)=(1+1)/2$
>
> $S(1)=1$
>
> 查阅定义中的表格中 $F_{2}$ 的值为 $1$
>
> $S(1)=fib(2)$

**$S(n)$ 计算过程**

> 依次计算
>
> $S(2)=fib(3)$
>
> $S(3)=fib(4)$
>
> $S(4)=fib(5)$
>
> 使用递推公式表达
>
> $S(n)=fib(n+1)$

使用通项公式计算出 $fib(n)$ 的值为$\frac{1}{\sqrt{5}}[(\frac{1+\sqrt{5}}{2})^{n}-(\frac{1-\sqrt{5}}{2})^{n}]$，在渐进的意义下时间复杂度为 $O(\Phi^{n}),\quad \Phi=\frac{1+\sqrt{5}}{2}=1.6180339887\ldots .$递归法时间复杂度 $T(n)$ 在渐进的意义下为 $O(2^{n}) .$

**$T(n)$ 计算过程**

> 根据公式 $\ref{recursion4}$
>
> $T(n)=2\cdot S(n)-1$
>
> 根据公式 $\ref{recursion6}$
>
> $T(n)=2\cdot fib(n+1)-1$
>
> 在渐进的意义下
>
> $T(n)=O(\Phi^{n})=O(2^{n})$

使用递归法计算斐波那契数的算法时间复杂度上也呈现出斐波那契数的形式，由于 $\Phi$ 比 2 小并且严格的比 1 大，依然是一个指数，可以用 $O(2^{n})$ 描述。

##### 斐波那契数列通项公式推导

上方计算 fib(n) 的值的详细过程如下，

设 $\{a_{n}\}$ 为斐波那契数列，根据斐波那契数列的定义可得，

$$
 \forall\quad n\ge3,\quad a_{n}=a_{n-1}+a_{n-2},\quad a_{1}=a_{2}=1
 \label{general1}
$$

尝试构造出一个等比数列，

$$
a_{n}+p\cdot a_{n-1}=q\cdot(a_{n-1}+p\cdot a_{n-2})
 \label{general2}
$$

**$p;q$ 计算过程**

> 由定义 $\ref{general1}$
>
> $a_{n}=1\cdot a_{n-1}+1\cdot a_{n-2}$
>
> 由等式 $\ref{general2}$ 变形
>
> $a_{n}=(q-p)a_{n-1}+q\cdot p\cdot a_{n-1}$

> 由上方两个式子
>
> $\begin{cases}q-p=1\\q\cdot p=1\end{cases}$
>
> 求解方程组
>
> $q=\frac{1}{p}$
>
> $\frac{1}{p}-p-1=0$
>
> $p^{2}+p-1=0$
>
> 运用二次公式$\frac{-b\pm\sqrt{b^{2}-4ac}}{2a}$解出 q 与 p

被构造出的等比数列其中 $p; q$ 值为：

$$
\begin{cases}
 p=\frac{\sqrt{5}-1}{2}
 \\
 q=\frac{\sqrt{5}+1}{2}
 \end{cases}
 \label{general3}
$$

或

$$
 \begin{cases}
 p=-\frac{1+\sqrt{5}}{2}
 \\
 q=\frac{1-\sqrt{5}}{2}
 \end{cases}
 \label{general4}
$$

将结果 $\ref{general3}$ 带入等式 $\ref{general2}$ 可得

$$
 a_{n}+\frac{\sqrt{5}-1}{2}a_{n-1}=\frac{\sqrt{5}+1}{2}(a_{n-1}+\frac{\sqrt{5}-1}{2}\cdot a_{n-2})
 \label{general5}
$$

**令**

$$
 b_{n-1}=a_{n}+\frac{\sqrt{5}-1}{2}a_{n-1}
 \label{general6}
$$

**则**

$$
 b_{n-1}=\frac{\sqrt{5}-1}{2}b_{n-2}
 \label{general7}
$$

**$b_{n-1}$计算过程**

> 上一步等式 $\ref{general6}$ 至 $\ref{general7}$ 中间的详细计算过程如下
>
> 将 $n-1$ 作为一个整体，带入等式 $\ref{general6}$ 的 n 中
>
> $b_{(n-1)-1}=a_{(n-1)}+\frac{\sqrt{5}-1}{2}a_{(n-1)-1}$
>
> 即
>
> $$
>  b_{n-2}=a_{n-1}+\frac{\sqrt{5}-1}{2}a_{n-2}
>  \label{general8}
> $$
>
> 由等式 $\ref{general5}$ 与 $\ref{general6}$
>
> $$
> b_{n-1}=\frac{\sqrt{5}-1}{2}(a_{n-1}+\frac{\sqrt{5}-1}{2}\cdot a_{n-2})
>  \label{general9}
> $$
>
> 由等式 $\ref{general8}$ 与 $\ref{general9}$ 可得结果等式 $\ref{general7}$
>
> $b_{n-1}=\frac{\sqrt{5}-1}{2}b_{n-2}$

使用等式 $\ref{general6}$ 计算被构造的等比数列首项，等式 $\ref{general7}$ 得到公比，

$$
 \begin{cases}
 首项\quad b_{1}=a_{2}+\frac{\sqrt{5}-1}{2}a_{1}=\frac{\sqrt{5}+1}{2}
 \\
 公比\quad Q=\frac{\sqrt{5}+1}{2}
 \end{cases}
$$

可得，

$$
b_{n}=(\frac{\sqrt{5}-1}{2})^{n}
\label{general10}
$$

将 $n+1$ 作为整体带入等式 $\ref{general6}$ 可得，

$b_{(n+1)-1}=a_{n+1}+\frac{\sqrt{5}-1}{2}a_{(n+1)-1}$

即

$$
b_{n}=a_{n+1}+\frac{\sqrt{5}-1}{2}a_{n}
\label{general11}
$$

由等式 $\ref{general10}$ 与等式 $\ref{general11}$ 可得，

$$
a_{n+1}+\frac{\sqrt{5}-1}{2}a_{n}=(\frac{\sqrt{5}+1}{2})^{n}
\label{general12}
$$

同理对结果 $\ref{general4}$ 进行与结果 $\ref{general3}$ 类似的计算可得，

$$
a_{n+1}-\frac{1+\sqrt{5}}{2}a_{n}=(\frac{1-\sqrt{5}}{2})^{n}
\label{general13}
$$

斐波那契数列需要同时满足等式 $\ref{general12}$ 与等式 $\ref{general13}$ ，使用等式 $\ref{general12}$ 减去等式 $\ref{general13}$ 可得，

$\frac{\sqrt{5}-1}{2}a_{n}-(-\frac{1+\sqrt{5}}{2}a_{n})=(\frac{\sqrt{5}+1}{2})^{n}-(\frac{1-\sqrt{5}}{2})^{n}$

$(\frac{\sqrt{5}-1}{2}+\frac{1+\sqrt{5}}{2})a_{n}=(\frac{\sqrt{5}+1}{2})^{n}-(\frac{1-\sqrt{5}}{2})^{n}$

$\sqrt{5}\cdot a_{n}=(\frac{\sqrt{5}+1}{2})^{n}-(\frac{1-\sqrt{5}}{2})^{n}$

移位可得斐波那契数列的通项公式为，

$$
a_{n}=\frac{1}{\sqrt{5}}[(\frac{1+\sqrt{5}}{2})^{n}-(\frac{1-\sqrt{5}}{2})^{n}]
$$

至此，递归版算法时间复杂度计算中 $fib(n)$ 的值的计算细节描述完毕。

### 迭代版

递归法算法高达 $O(2^{n})$ 的时间复杂度，是由于内部含有大量重复的计算。可以在递归算法中引入缓存机制，避免重复计算以此方式提高效率。也可以直接使用迭代的方法，使用 JavaScript 语言描述如下，

```javascript
function fibonacci(n) {
  let f = 0;
  let g = 1;
  for (let i = 0; i < n; i++) {
    f = g + f;
    g = f - g;
  }
  return f;
}

console.log(fibonacci(40));
```

//TODO
