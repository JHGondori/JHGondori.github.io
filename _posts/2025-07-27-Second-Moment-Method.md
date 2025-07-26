---
title: Probabilistic Method - Second Moment Method
date: 2025-07-27 03:15:40 +0900
categories: [Mathematics, Probability]
tags: [mathematics, probability, probabilistic method]
math: true
---
> **Second Moment Method**는 Chebyshev's Inequality로부터 유도되는 부등식을 이용하는 Probabilistic method 중 하나입니다. 바로 시작해봅시다.

## Second Moment Method
일단 유도를 위한 Chebyshev's Inequality부터 알아봅시다.
### Chebyshev's Inequality

<blockquote class = "theorem">

임의의 $a>0$에 대해 다음이 성립한다.

$$
\Pr(|X-\mathbf{E}[X]|\geq a) \leq \frac{\mathbf{Var}[X]}{a^2}
$$

</blockquote>

### Proof
증명을 위해서는 Markov's Inequality를 사용해야 합니다!

Markov's Inequality는 $X$가 non-negative random variable일 때, 

$$
\Pr(X\geq a)\leq\frac{\mathbf{E}[X]}{a}
$$

가 성립한다는 부등식입니다.

이 부등식을 이용해 Chebyshev's Inequality를 증명해봅시다.

$$
\Pr(|X-\mathbf{E}[X]|\geq a) = \Pr((X-\mathbf{E}[X])^2\geq a^2)
$$

여기서 $Y = (X-\mathbf{E}[X])^2$로 설정하면,

$$
\Pr(Y\geq a^2)\leq \frac{\mathbf{E}[Y]}{a^2}=\frac{\mathbf{Var}[X]}{a^2}
$$

따라서 부등식이 성립함을 알 수 있습니다.

### To return
Second Moment Method는 아래 정리를 사용합니다.

<blockquote class = "theorem">

임의의 $a>0$에 대해 다음이 성립한다.

$$
\Pr(X = 0) \leq \frac{\mathbf{Var}[X]}{(\mathbf{E}[X])^2}
$$

</blockquote>
 
### Proof
위에서 다룬 Chebyshev's Inequality를 적용하면 바로 유도됩니다.

$$ 
\Pr(X=0) \leq \Pr(|X-\mathbf{E}[X]| \geq \mathbf{E}[X]) \leq \frac{\mathbf{Var}[X]}{(\mathbf{E}[X])^2}
$$

---

### Threshold values

Second Moment Method는 Random graph에서 threshold values를 알아내고 싶을 때 이용됩니다. 그냥 threshold는 다양한 의미를 가지고 있긴 하지만, 여기서 다루는 threshold는 아래와 같은 의미를 가지고 있습니다.

<blockquote class = "theorem">

어떤 $p(n)$이 존재해

<ol>
<li>
$\lim_{n\rightarrow\infty}\frac{p_1(n)}{p(n)}=0$일 때, $G_{n, p_1(n)}$이 거의 확정적으로 원하는 property를 가지지 않으며, (확률이 거의 0)
</li>
<li>
$\lim_{n\rightarrow\infty}\frac{p_2(n)}{p(n)}=\infty$일 때, $G_{n, p_2(n)}$이 거의 확정적으로 원하는 property를 가지면, (확률이 거의 1)
</li>
</ol>

Random graph model에서 phase transition이 일어난다고 볼 수 있으며, $p(n)$을 threshold라고 부른다.

</blockquote>

Random graphs에서 대부분의 property는 transition이 일어나기 전에는 안 나타나지만 transition이 일어나면 나타나게 되는 threshold가 존재한다고 합니다. 

이제 그 예시를 알아보도록 합시다!

### Example : Threshold behavior in random graphs

<blockquote class = "theorem">

$G_{n, p}$에서 $p=f(n)$이라고 가정합시다. $G$를 $G_{n, p}$에서 뽑힌 random graph라 할 때, 사건 $A$를 $G$가 4개, 혹은 그 이상 개수의 정점으로 이루어진 clique를 가지는 사건으로 둡시다. 
<ol>
<li>
만약 $f(n)=\mathcal{o}(n^{-2/3})$ 이라면, $\Pr(A)=\mathcal{o}(1)$ 이다.
</li>
<li>
만약 $f(n)=\mathcal{w}(n^{-2/3})$ 이라면, $\Pr(A)=1-\mathcal{o}(1)$ 이다.
</li>
</ol>
</blockquote>

### Proof
일단 $\mathcal{o}(n), \mathcal{w}(n)$이 무엇인지 알아봅시다!

#### Asymptotic bounds

$\mathcal{o}(n), \mathcal{w}(n)$와 같은 것들을 asymptotic bounds라고 하는데요, 얘네들의 의미는 다양하게 표현할 수 있습니다. 원래 정의는 막 어떤 적당한 정수 $n_0$이 존재하고, 적당한 상수 $c$가 존재해서 모든 정수 $n\geq n_0$에 대해 $f(n)$은 $c g(n)$보다 작거니 크거니 어쩌구 저쩌구... 이러는데, 이런 내용은 지금 문제를 푸는 데에 그렇게 중요하지는 않아요. 그래서 그나마 간단한 정의를 이용해서 문제를 풀어봅시다.

1. $f(n) = \Theta(g(n))$

    얘는 $f$ grows at the same rate as $g$라는 뜻을 가지고 있어요. 간단하게 아래와 같이 표현할 수 있습니다. 예시로 $f=n, g=2n$을 들 수 있겠네요.

    $$
    \lim_{n\rightarrow\infty} f(n)/g(n)\neq 0, \infty
    $$

2. $f(n)=\mathcal{O}(g(n))$

    얘는 $f$ grows no faster than $g$라는 뜻을 가지고 있습니다. 예시로 $f=n, g=n^2$이 있어요.

    $$
    \lim_{n\rightarrow\infty} f(n)/g(n)\neq \infty
    $$

3. $f(n) = \Omega(g(n))$

    얘는 $f$ grows at least as fast as $g$라는 뜻을 가지고 있습니다. 예시로 $f=3n^2, g=2\log n$이 있겠죠.

    $$
    \lim_{n\rightarrow\infty} f(n)/g(n)\neq 0
    $$

4. $f(n)=\mathcal{o}(g(n))$

    얘는 $f$ grows slower than $g$라는 뜻을 가지고 있습니다. 예시로 $f=n, g=n^2$가 있죠.

    $$
    \lim_{n\rightarrow\infty} f(n)/g(n) = 0
    $$

5. $f(n)=\mathcal{w}(g(n))$

    얘는 $f$ grows faster than $g$라는 뜻을 가지고 있습니다. 예시로 $f=n, g=n^2$가 있죠.

    $$
    \lim_{n\rightarrow\infty} f(n)/g(n) = \infty
    $$

6. $f \sim g$

    얘는  $f/g$가 1로 간다는 뜻입니다. $f=n+1, g=n$이런 식이겠죠.

그렇다면 문제에 있는 $f(n)=\mathcal{o}(n^{-2/3})$은 $\lim_{n\rightarrow\infty} pn^{2/3} =0$로 볼 수 있고, $f(n)=\mathcal{w}(n^{-2/3})$은 $\lim_{n\rightarrow\infty} pn^{2/3} =\infty$로 볼 수 있게 됩니다.

#### Proof of 1.
1번 증명부터 해봅시다!

$C_1, C_2, \dots , C_M$을 $G$에서 만들 수 있는 모든 4개 정점 sets라고 둡시다. $M=\binom{n}{4}$겠죠.

이 다음, $i=1, \dots , M$에 대해 

$$
X_i = \begin{cases}
& 1 \quad \mathsf{if\;} C_i\;\mathsf{is\;a\;clique} \\
& 0 \quad \mathsf{otherwise,}
\end{cases}
$$

을 정의합시다. 여기서 $X = \sum_{i=1}^{M} X_i$로 두면, $\Pr(X_i = 1) = p^6$이므로, (4개 정점을 서로 연결하는 6개의 간선이 모두 있어야 합니다!)

$$
\mathbf{E}[X] = \binom{n}{4} p^6 = \Theta(n^4p^6)=\Theta((pn^{2/3})^6)
$$

이며, 여기서 $p = f(n) = \mathcal{o}(n^{-2/3})$이므로, 

$$
\lim_{n\rightarrow\infty} \mathbf{E}[X] = \lim_{n\rightarrow\infty} \Theta((pn^{2/3})^6) = 0
$$

따라서 $\mathbf{E}[X] = \mathcal{o}(1)$임을 알 수 있습니다. 

$G_{n, p}$에서 4개 이상 정점의 clique를 가질 확률은 $\Pr(X\geq 1)$으로 볼 수 있는데요, $X$가 non-negative 정수이므로 이 때 쓸 수 있는 유용한 부등식이 있습니다. 

$$
\mathbf{E}[X] = \sum_{i=0}^{\infty} \Pr(X\gt i)\geq \Pr(X\geq 1)
$$

이죠. 이를 이용하면, 

$$
\Pr(X\geq 1)\leq \mathbf{E}[X] = \mathcal{o}(1)
$$

임을 알 수 있습니다. 이렇게 1번의 증명이 끝났습니다. 이제 2번을 증명해봅시다.

#### Proof of 2.
여기서 Second Moment Method를 사용합니다. 근데.. 보기보다 개빡셉니다. 그림 없이는 이해가 힘들지도...

한번 1번 증명처럼 접근해볼까요? 여기서는 $p = f(n) = \mathcal{w}(n^{-2/3})$이므로, 대충 중간과정 좀 생략해서 $\mathbf{E}[X]$가 $n$이 무한으로 갈 때 같이 무한으로 가는 것을 알 수 있습니다. 

여기서 기댓값이 무한이니까 $G_{n, p}$에서 4-clique가 있을 확률도 거의 1이지 않을까..? 라고 생각하시면 안됩니다! 

만약 $1/n^2$의 확률로 $G_{n, p}$에서 4-clique를 찾을 수 있다고 가정해봅시다. 얘는 $n$이 커지면 0으로 가는 확률이죠. 하지만, 4-clique 자체가 $\binom{n}{4}$만큼 있기 때문에 $\mathbf{E}[X] = \Omega(n^2)$이 됩니다.  얘는 $n$이 무한으로 가면 같이 무한으로 가버리죠. 따라서! 다른 증명 방법이 필요합니다.

목표는 아래 식이 성립함을 보이는 것입니다.

$$
\Pr(X=0)\leq\frac{\mathbf{Var}[X]}{(\mathbf{E}[X])^2}=\mathcal{o}(1)
$$

즉, $\mathbf{Var}[X] = \mathcal{o}(\mathbf{E}[X]^2)$임을 보여야 합니다. 이에 대한 증명을 위한 하나의 보조정리를 알아봅시다.

---

**Lemma**

<blockquote class = "theorem">

$Y_i$는 0또는 1의 값을 가지는 random variable이고, $Y = \sum_{i=1}^m Y_i$로 두자. 이 때 다음 식이 성립한다.

$$
\mathbf{Var}[Y]\leq\mathbf{E}[Y] + 2\sum_{i\lt j} \mathbf{Cov}(Y_i, Y_j)
$$

</blockquote>

**Proof of the Lemma**

$$
\begin{align*} \mathbf{Var}[Y] &= \mathbf{E}[Y^2]-(\mathbf{E}[Y])^2 \\
&= \mathbf{E}\left[\sum_i Y_i^2 + 2\sum_{i\lt j} Y_i Y_j\right] - \sum_i (\mathbf{E}[Y_i])^2 - 2\sum_{i\lt j} \mathbf{E}[Y_i] \mathbf{E}[Y_j] \\
&= \sum_i \mathbf{Var}[Y_i] + 2\sum_{i\lt j} \mathbf{Cov}(Y_i, Y_j)
\end{align*}
$$

여기서 $Y_i$가 0 또는 1이기 때문에 

$$
\mathbf{Var}[Y_i] = \mathbf{E}[Y_i^2]-(\mathbf{E}[Y_i])^2 = \mathbf{E}[Y_i] - (\mathbf{E}[Y_i])^2 \leq \mathbf{E}[Y_i]
$$

이므로 아래 Lemma가 성립함을 알 수 있습니다.

$$
\mathbf{Var}[Y]\leq\mathbf{E}[Y] + 2\sum_{i\lt j} \mathbf{Cov}(Y_i, Y_j)
$$

---

$\mathbf{E}[X]$는 알고 있으므로, Covariance를 구해봅시다. Covariance를 구할 때는 아래 식으로 적당히 부등식을 세워 구할 예정입니다.

$$
\mathbf{Cov}(X_i, X_j) = \mathbf{E}[X_i X_j] - \mathbf{E}[X_i]\mathbf{E}[X_j] \leq \mathbf{E}[X_i][X_j]
$$ 

$X_i, X_j$의 Covariance는 $\|C_i \cap C_j\| = 0, 1, 2, 3$으로 case를 나눠서 구할 수 있습니다.

1. $\|C_i \cap C_j\| = 0, 1$일 때

    이 경우에서는 정점은 겹칠 수 있더라도 간선은 서로 안겹치죠. 자명히 $X_i, X_j$는 독립입니다. $\mathbf{Cov}(X_i, X_j) = 0$임을 알 수 있죠.

2. $\|C_i \cap C_j\| = 2$일 때

    이 경우에서는 겹치는 두 정점 사이 간선 **하나**가 겹칩니다. 따라서 $\mathbf{E}[X_i X_j] = p^{(6+6-1)}$임을 알 수 있습니다. $X_i, X_j$ 둘 다 1이어야 하기 때문이죠. 이를 통해 아래 식을 자연스럽게 알아낼 수 있습니다.

    $$
    \mathbf{Cov}(X_i, X_j)\leq \mathbf{E}[X_i X_j] = p^{11}
    $$

    그리고 이런 상황이 나타나는 경우의 수는 6( = 8 - 2)개의 정점을 고르는 가짓수 $\binom{n}{6}$에 $C_i, C_j$에 넣는 경우의 수 $\binom{6}{2;2;2}$를 곱한 값입니다. (2개는 겹치는 정점으로 배정, 나머지 4개는 둘 둘로 나눠 배정합니다.)

3. $\|C_i \cap C_j\| = 3$일 때

    이 경우에서는 겹치는 3 정점 사이 간선 셋이 겹칩니다. 따라서 아래 식이 성립합니다.

    $$
    \mathbf{Cov}(X_i, X_j)\leq \mathbf{E}[X_i X_j] = p^{(6+6-3)} = p^9
    $$

    그리고 이런 상황이 나타날 경우의 수는 5( = 8 - 3)개의 정점을 고르는 경우의 수 $\binom{n}{5}$에 $C_i, C_j$에 넣는 경우의 수 $\binom{5}{3;1;1}$를 곱한 값입니다. (3개는 겹치는 정점으로 배정, 나머지 2개는 하나 하나로 나눠 배정합니다.)

다 왔습니다! 이제 지금까지 진행한 것을 종합해봅시다. $p = \mathcal{w}(n^{-2/3})$이므로, 

$$
\begin{align*} \mathbf{Var}[X] &\leq \mathbf{E}[X] + \sum_{i\neq j} \mathbf{Cov}(X_i, X_j) \\[1ex]
&= \binom{n}{4} p^6 + \binom{n}{6}\binom{6}{2;2;2} p^{11} + \binom{n}{5}\binom{5}{3;1;1} p^9 \\[2ex]
&= \Theta(n^4 p^6) + \Theta(n^6 p^{11}) + \Theta(n^5 p^9) \\[2ex]
&= \mathcal{o}(n^8 p^{12}) = \mathcal{o}((\mathbf{E}[X])^2)
\end{align*}
$$

맨 아래 줄은 $\mathbf{E}[X] = \Theta(n^4 p^6)$이라는 사실로부터 나옵니다! 따라서, 아래 식이 성립합니다.

$$
\Pr(X=0)\leq\frac{\mathbf{Var}[X]}{(\mathbf{E}[X])^2} = \mathcal{o}(1)
$$

즉,

$$
\Pr(X\geq1)= 1 - \mathcal{o}(1)
$$

이렇게 2번 증명까지 끝났습니다!

### 여담
이걸 살면서 쓸 일이 있을려나... 진짜 쉽지 않네요.

## References
-   Mitzenmacher, M., & Upfal, E. (2005). Probability and computing: Randomization and probabilistic techniques in algorithms and data analysis. Cambridge university press.