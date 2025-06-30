---
title: Probabilistic Method - Expectation Argument
date: 2025-06-30 22:20:40 +0900
categories: [Mathematics, Probability]
tags: [mathematics, probability, probabilistic method]
math: true
---

> 여기는 진짜 쉽습니다!

## Expectation Argument(를... 가장한 Cut 배우기)
제목 그대로 기댓값을 사용하는 겁니다! 이 아이디어는 아래 정리에서 나옵니다.

### Theorem
만약 $E[X]=\mu$라면, $\Pr(X\geq\mu)\gt 0$ 와 $\Pr(X\leq\mu)\gt 0$이 성립한다.
### Proof
~~솔직히... 자명하죠~~

만약 $\Pr(X\geq \mu)=0$ 이면,

$$
\mathbf{E}[X] = \sum_{x}x\Pr(X=x)=\sum_{x\lt\mu}x\Pr(X=x)\lt\sum_{x\lt\mu}\mu\Pr(X=x)=\mu
$$

이므로, $\mathbf{E}[X]=\mu$ 라는 가정에 모순입니다. 따라서 $\Pr(X\geq\mu)\gt 0$이 성립하게 됩니다. 

반대 방향도 똑같이 증명해주면 됩니다.

---

Theorem부터 어떤 느낌으로 쓸 건지 감이 오실 겁니다. 그냥 랜덤하게 뽑을 때의 기댓값 이상일 확률, 이하일 확률이 모두 0보다 크다는 점을 이용하면 바로 존재성을 증명할 수 있겠죠. 

이 방법을 활용하는 문제들은 그냥 문제를 잘 이해하고 확률변수만 잘 설정해주면 쉽게 풀 수 있습니다. 그래서 예시를 하나 풀어보고, 좀 더 나아가서 Derandomization까지 하는 방법을 알아가보도록 합시다.(요놈은 다음 포스트에!)

### Example - Finding a Large Cut
만약 그래프 $G = (V, E)$가 $m$개의 간선을 가지고 있고, 각 간선의 가중치가 1일 때, Maximum cut의 값은 최소 $m/2$이다. 
### Proof
#### Cut?
일단 cut이 뭔지부터 알아봅시다(~~분량 채우기~~). 

Cut $S$는 그래프 $G=(V, E)$에서 정점 집합 $V$를 두 개의 서로 겹치지 않는 부분집합인 $S$와 $V\backslash S$로 나누는 것을 의미합니다. 여기서 $S$는 $V\subset S$이고, $S\neq\varnothing$여야 합니다. 안그러면... 의미가 없겠죠.

그리고 Cut-set이라는 것도 있는데, 간선 $(u, v)\in E$ 중 정점 $u$와 $v$ 중 정확히 하나만 $S$에 포함되는 간선들의 집합을 Cut-set이라고 합니다. 수학적으로(?)는 아래와 같이 정의됩니다. 

$$
\{(u, v)\in E | u\in S, v\in V\backslash S\}
$$

조금 이해가 어렵다면 Cut $S$에 의해 분리되는 간선들의 집합이라고 보시면 편합니다. 

그리고 unweighted undirected graph에서 cut $S$와 $V\backslash S$ 사이 간선, 즉 cut-set에 포함되는 간선의 개수를 cut의 size 또는 weight라고 합니다.

Weighted Graph에서는 cut-set에 포함되는 모든 간선의 가중치를 합한 값을 cut의 value 또는 weight라고 합니다. 만약 graph 간선의 weight가 모두 1이라면 unweighted, weighted 둘의 cut weight는 같을 겁니다.

좀 어렵게 느껴질 수도 있지만, 다른 관점으로 보면 Cut은 그래프의 각 정점을 두 가지 색으로 칠하는 것이랑 다른게 없다는 걸 알 수 있습니다. 이러면 cut-set에 포함되는 간선은 그냥 양 끝 점의 색깔이 다른 간선이라고 보면 됩니다. 훨씬 편해지죠.
#### Minimum Cut and Maximum Cut

이제 관심을 가지는 Maximum Cut에 대해 알아봅시다. Cut에 대한 문제에는 Minimum Cut과 Maximum Cut이 있습니다. 

Minimum Cut은 그래프에서 Cut의 value를 가장 작게 하는 Cut을 찾는 문제입니다. 
얘는 다항 시간에 찾을 수 있는 알고리즘이 존재해요. Stone-Wagner algorithm이라고, Minimum cut을 $\mathcal{O}(|V||E|+|V|^2 \log|V|)$의 시간 복잡도로 찾을 수 있는 방법이 있습니다. 근데 얘는 지금 다루는 것이랑 관계가 없어서, 이정도만 하고 넘어갈게요.

Maximum Cut은 Minimum Cut의 반대입니다. Cut의 value를 가장 크게 하는 Cut을 찾는 겁니다. 말만 간단하지... 요놈은 NP-hard라고 합니다. 다항시간에 푸는 방법이 아직 없어요. 

하지만! Probabilistic method를 사용하면 하한값을 찾을 수 있습니다. 지금은 그 하한값을 찾는 과정 중 가장 간단한 형태의 문제를 풀려고 하는 겁니다. (진짜 간단해요.)
#### 진짜 Proof
그래프 $G$의 모든 정점 $v$를 집합 $A$, 또는 $B$에 독립적으로 넣어봅시다. 둘 중 하나에 들어갈 확률은 모두 독립적으로 $\frac{1}{2}$가 되겠네요. 그리고 $C(A, B)$를 cut 집합 $S=A$인 cut의 value로 둡시다. 

$E = \{e_1, e_2, \dots, e_m\}$으로 두면서 각 간선들을 ordering하고, 확률 변수 $X_i$를 아래와 같이 정의합시다.

$$
X_i = \begin{cases}
& 1\quad\mathsf{if}\ e_i\ \mathsf{is}\ \mathsf{between}\ A\ \mathsf{and}\ B, \\
& 0 \quad\mathsf{otherwise.}
\end{cases}
$$ 

이제 $C(A, B)$의 기댓값을 구해보죠. $C(A, B) = \sum_{i=1}^{m} X_i$이므로, $X_i$의 기댓값을 구하면 바로 $C(A, B)$의 기댓값도 구할 수 있습니다. $X_i$의 기댓값은 아래와 같이 구해집니다. 

$$
\mathbf{E}[X_i] = \Pr(X_i=1)=\frac{1}{2}
$$

따라서 $C(A, B)$의 기댓값을 아래와 같이 구할 수 있습니다.

$$
\mathbf{E}[C(A, B)] = \mathbf{E}\left[\sum_{i=1}^{m} X_i\right]=\frac{m}{2}
$$

여기까지 오면 이제 다 끝났다는 것을 알 수 있으실 겁니다. 기댓값이 $\frac{m}{2}$이므로, 위에서 다룬 expectation argument에 의해 아래와 같은 사실을 알 수 있습니다.

$$
\Pr\left( C(A, B)\geq \frac{m}{2} \right) \gt 0
$$

따라서, Maximum Cut value의 하한값은 $\frac{m}{2}$임을 알 수 있습니다. 증명 끝!

---

솔직히, Expectation Argument만으로는 별 내용이 없습니다. 그냥 기댓값을 구하고 딸깍하면 바로 풀린다는 것이 전부죠.. 문제를 이해하는 게 가장 빡세다고 볼 수 있습니다.

학교에서 $k-SAT$에 적용하는 예시도 배웠는데, 얘도 그냥 MAX-SAT가 뭔지 알아보고 한번 써보는 수준이었습니다. 딱히 별건 없어요. 
 
그래서 추가적인 내용 같은(?) 유익한(?) Expectation을 이용하는 deterministic construction algorithm을 다음 포스트에서 알아볼 겁니다. 이 방법을 Derandomization이라고 해요. 원래는 안 쓰려고 했는데... 여긴 내용이 뭐가 없어서 쓰면 좋을 것 같네요. 

## References
-   Mitzenmacher, M., & Upfal, E. (2005). Probability and computing: Randomization and probabilistic techniques in algorithms and data analysis. Cambridge university press.