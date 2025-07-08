---
title: Probabilistic Method - The Basic Counting Arguments
date: 2025-06-27 18:10:40 +0900
categories: [Mathematics, Probability]
tags: [mathematics, probability, probabilistic method]
math: true
---
> 그래프에 대한 기본(?) 지식이 필요해요!

## The Basic Counting Arguments
Probabilistic Method로 Combinatorial Object의 존재성을 보이기 위해서, 우리는 object에 대한 적절한 distribution을 만들고, 그 distribution에서 랜덤하게 뽑을 때 조건을 만족하는 object가 골라질 확률이 0보다 크다는 것을 보여야 합니다.


그래서 어떻게 하는 걸까... 예시를 통해 알아봅시다. 

이 post에서는 기본적인 조합적 증명으로 Probabilistic Method를 쓸거라 아 이런느낌이구나~ 정도 알아가시면 될 거에요.


아래와 같은 정리를 증명해보면서 슬슬 알아가보도록 합시다.
#### Theorem
$K_n$ 을 n개의 정점을 가진 complete graph라고 하자.

<blockquote class = "theorem">

If $\binom{n}{k} 2^{-\binom{k}{2}+1} \lt 1$, then it is possible to color the edges of $K_n$ with two colors so that it has no monochromatic $K_k$ subgraph.

</blockquote>

#### Proof
~~초장부터 훅 들어오네~~

좀 풀어 쓰자면, 먼저 n개의 정점을 가진 complete graph의 모든 간선을 두 개의 색으로 색칠합니다. 편의상 빨강, 파랑으로 색칠하도록 합시다. 이 때 저 $n, k$의 조건을 만족하면, $K_k$와 동형인 모든 $K_n$ 부분 그래프 중에 간선의 색이 모두 같은 색인 것이 존재하지 않도록 색칠할 수 있다는 뜻입니다. 


이 문제는 어떤 조건을 만족하는 간선 색칠법이 존재한다는 것을 보이는 문제이므로, 모든 간선을 랜덤하게 색칠하고, 조건을 만족할 확률이 0보다 크다는 것을 보이면 됩니다. 


$K_n$의 모든 간선을 독립적으로 $\frac{1}{2}$의 확률로 빨간색 또는 파란색으로 색칠한다고 합시다. 그리고 $K_n$의 부분 그래프 중 $K_k$와 동형인 모든 것(이 다음부터 $k$ - cliques라고 부를게요. Cliques는 별거 없어서 찾아보시면 될거에요. :) )을 1부터 $\binom{n}{k}$까지 번호를 매깁시다. 

이제 $i$번째 $k$ - clique가 단색인 사건을 $A_i$라고 합시다. 이 때 사건 $A_i$가 일어나기 위해선 간선 하나의 색을 아무거나 하나로 두고, 나머지 $\binom{k}{2}-1$ 개의 간선이 두 가지 색 중 정확히 처음 정한 색이 되어야 하므로 $A_i$가 일어날 확률은 아래와 같다는 사실을 알 수 있습니다. 

$$
\Pr(A_i) = 2^{-\binom{k}{2}+1}
$$ 

이제 여기서 Union bound를 쓰면, 적어도 하나가 단색일 확률에 대한 식이 아래와 같이 나오게 됩니다. 

$$
\Pr\left(\bigcup_{i=1}^{\begin{pmatrix}n\\k\end{pmatrix}}A_i\right)\leq\sum_{i=1}^{\begin{pmatrix}n\\k\end{pmatrix}}\Pr(A_i)=\begin{pmatrix}n\\k\end{pmatrix}2^{-\begin{pmatrix}k\\2\end{pmatrix}+1}
$$

그렇습니다. Theorem에 있던 뭔 소린지 모르겠던 If 조건이 튀어나온 것을 볼 수 있습니다!

~~너무 억지 아니여?~~ 

자 여기서 만약 $\binom{n}{k} 2^{-\binom{k}{2}+1} \lt 1$이라면, 

$$
\Pr\left(\bigcap_{i=1}^{\begin{pmatrix}n\\k\end{pmatrix}}\bar{A_i}\right) = 1 - \Pr\left(\bigcup_{i=1}^{\begin{pmatrix}n\\k\end{pmatrix}}A_i\right) \gt 0
$$

이 성립하게 됩니다. 즉, 랜덤하게 색칠했을 때, 모든 $k$ - cliques가 단색이 아닐 확률이 0보다 크다는 뜻입니다. 

따라서 $\binom{n}{k} 2^{-\binom{k}{2}+1} \lt 1$이면, 모든 $k$-cliques가 단색인 색칠법이 존재한다는 사실이 증명됩니다. ~~와!~~ 


이렇게 조합적 증명(Counting Arguments)으로 Probabilistic method를 사용하는 하나의 예시를 알아보았습니다. 다음부터 유용한 기법(?)들을 알아가봅시다. :)

#### 여담
숫자 스케일이 감이 안와서 wolframalpha로 $n=1000$ 일 때 $k$가 얼마 이상이어야 저 요상한 조건을 만족하는지 계산해보았는데, $k=16$부터 만족하더라고요. 즉 $k$가 이 값 이상이 되면 모든 $k$-cliques가 단색이 아니도록 하는 색칠법이 존재하게 됩니다. 

그리고 $n=1000, k=20$일 때 $\binom{n}{k} 2^{-\binom{k}{2}+1} \simeq 4.3\times 10^{-16}$이 나옵니다. 즉, 랜덤하게 색칠했을 때 monochromatic 20-clique가 없을 확률이 무려 $1-4.3\times 10^{-16}$이 됩니다. 그냥 대충 그려도 없을 거 같네요..ㅎㅎ

만약 단색인 $k$ - cliques가 없는 색칠법을 찾고 싶다면 Monte-Carlo Algorithm을 무지성으로 갖다 박으면 될 거 같습니다.

## References
-   Mitzenmacher, M., & Upfal, E. (2005). Probability and computing: Randomization and probabilistic techniques in algorithms and data analysis. Cambridge university press.