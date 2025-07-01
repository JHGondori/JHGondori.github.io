---
title: Probabilistic Method - Derandomization
date: 2025-07-01 17:32:40 +0900
categories: [Mathematics, Probability]
tags: [mathematics, probability, probabilistic method]
math: true
---

> 사실 지금까지는 시작도 안했다고 볼 수 있습니다... 화이팅
>
> 몇몇은 뇌피셜이 있어서 잘 걸러서 보시면 될거 같아요

## 이게 뭐에요
지금까지는 Probabilistic method로 존재성만 증명했습니다. 그래서 있는 건 알겠는데, 어떻게 찾을까요? ~~왜 궁금한데~~

증명할 때 Random하게 뽑아서 나올 확률이 0보다 크다는 점을 이용했으므로, 랜덤하게 construct하면 원하는 combinatorial object를 언젠간 찾을 수 있을 겁니다. 

Probabilistic method로 최소 $p$의 확률로 원하는 object를 얻을 수 있다는 점을 알아냈다면 평균적으로 $1/p$번의 랜덤 시행으로 원하는 object를 얻을 수 있습니다. p가 엄청 작지만 않으면 노가다 뛰는 것보단 이렇게 찍어서 들어맞는 걸 찾는게 더 효율적일 수 있을 것 같네요. 찾기만 하면 되니까요. 근데 랜덤하다는 게 좀.. 마음에 걸립니다. 

근데 특정한 경우에서는 무조건 원하는 object를 찾을 수 있는 deterministic construction algorithm을 Probabilistic method로부터 얻어낼 수 있습니다.

이 방법을 Derandomization이라고 합니다. 원래 Random algorithm에서 시간복잡도를 크게 늘리지 않고 deterministic하게, 아니면 최대한 randomness를 줄이고 찾는 법으로 볼 수도 있어요. Derandomization하는 방법에도 여러가지가 있다는데, 여기서는 conditional expectations를 이용해 Derandomization하는 법을 알아가봅시다. 
## Derandomization
General하게 하는 법은 배우질 않아서 잘 몰라요. 예전에 찾아보긴 했는데, 아직 임의의 random algorithm을 derandomization하는 법은 알려지지 않았다고 봤던 거 같습니다. 예시 하나를 보고 그냥 이런 거구나~ 하고 알아가고 넘어가도록 하죠.

### Random algorithm
전 post에서 다룬 Maximum Cut으로 돌아가서 랜덤 알고리즘을 어떻게 짜는지부터 봅시다. 랜덤 알고리즘도 방법이 다양해서 예시만 들고 넘어가도록 할게요.

 Probabilistic method를 쓸 때 랜덤하게 set $A, B$를 설정했었습니다. 그리고 $\Pr\left( C(A, B)\geq \frac{m}{2}\right)$가 0보다 크다는 점을 이용해 존재성을 증명했습니다. 

여기서 Las Vegas algorithm으로 찾으면 됩니다. 그냥 될 때까지 랜덤 돌리는 거에요.

~~~
repeat until success
	1. Assign A, B randomly.
	2. If C(A, B)>=m/2, algorithm succeed and print (A, B). 
	   else, failed.
~~~

2번은 $\mathcal{O}(m)$으로 판별할 수 있습니다. 이제 성공 확률을 알아보죠. 아래와 같은 과정으로 성공 확률에 대한 정보를 얻을 수 있습니다.

$$
p = \Pr\left( C(A, B)\geq\frac{m}{2}\right) 
$$

로 정의했을 때,

$$
\begin{align*} \frac{m}{2} & = \mathbf{E}[C(A, B)]\\
 & = \sum_{i\leq m/2-1}i\Pr(C(A, B)=i)+\sum_{i\geq m/2}i\Pr(C(A, B)=i)\\
 & = \sum_{i\leq m/2-1}\left(\frac{m}{2}-1\right)\Pr(C(A, B)=i)+\sum_{i\geq m/2}m\Pr(C(A, B)=i) \\
 & = (1-p)\left(\frac{m}{2}-1\right)+pm
 \end{align*}
 $$
 
 따라서, $p\geq\frac{1}{m/2+1}$입니다. 이러면 $m/2+1$ 번 정도 랜덤 가챠를 돌리면 cut value가 m/2를 넘기는 Cut을 얻을 수 있다고 볼 수 있죠.
### Derandomization using conditional expectations
다행히도 지금 다루는 문제는 derandomization을 통해 deterministic construction algorithm을 알아낼 수 있습니다.

현재 아는 정보는 $E[C(A, B)]\geq m/2$ 밖에 없습니다. ~~슬프네요.~~

여기서 정점을 $V=\{v_1, \dots, v_n\}$으로 ordering하고, $x_i$를 $v_i$가 들어간 set으로 정의합시다. ($x_i$는 $A$ 또는 $B$가 될겁니다.)

그리고 $\mathbf{E}[C(A, B) | x_1, \dots, x_k]$를 이미 $v_1, \dots, v_k$가 
들어간 set이 $x_1, \dots, x_k$로 정해졌을 때 $C(A, B)$의 기댓값으로 둡시다. 

그렇다면 아래와 같은 사실을 알 수 있습니다.

$$
\begin{align*}\mathbf{E}[C(A, B) | x_1, \dots, x_k] = & \frac{1}{2}\mathbf{E}[C(A, B) | x_1, \dots, x_k, v_{k+1}\in A] \\
& +\frac{1}{2}\mathbf{E}[C(A, B) | x_1, \dots, x_k, v_{k+1}\in B]
\end{align*}
$$

따라서,

$$
\max_{X\in{A, B}}\mathbf{E}[C(A, B) | x_1, \dots, x_k, v_{k+1}\in X]\geq \mathbf{E}[C(A, B)|x_1, \dots, x_k]
$$

이므로, 위의 식에서 $v_{k+1}$이 포함될 set인 $X$를 $A$와 $B$ 중에서 
$\mathbf{E}[C(A, B) | x_1, \dots, x_k, v_{k+1}\in X]$ 를 크게 하는 쪽으로 선택하면, 아래와 같은 식을 얻을 수 있습니다.

$$
\mathbf{E}[C(A, B)|x_1, \dots, x_k, x_{k+1}]\geq\mathbf{E}[C(A, B)|x_1, \dots, x_k]
$$

즉, 조건부 기댓값을 계속 늘려가는 쪽으로 각 정점이 들어갈 Set을 선택해가면, 최종적으로 모든 정점의 위치가 결정되었을 때 

$$
C(A, B) = E[C(A, B)|x_1, \dots, x_n]\geq E[C(A, B)]
$$

 가 되면서, 무조건 Cut value가 $m/2$보다 큰 Cut을 얻어낼 수가 있게 됩니다. 기존 랜덤 알고리즘은 $\frac{1}{m/2+1}$의 확률로 답을 얻어낼 수 있었는데, 그보다 엄청 좋아진 알고리즘을 얻었습니다... 가 아직 아닙니다.

### 아직 끝이 아니다
저기서 conditional expectation을 어떻게 중간에 구해서 비교할까요? (개인적으로 이게 중요해 보여요. 아니면... 아쉬운거죠ㅠㅠ) 

이 문제에서는 그렇게 어렵지 않습니다. 그래서 derandomization이 쉽게 되죠. 양쪽의 정점이 결정된 간선은 각각 cut-set에 들어가는지 확인하고, 그렇지 않은 간선은 그런 간선의 개수에 $1/2$를 곱해서 더하면 구할 수 있습니다. 저 간선들은 cut-set에 들어갈 확률이 무조건 $1/2$이기 때문입니다. 

Conditional expectation을 구하는 방법을 통해 생각하면, iteration $i$에서 $v_i$와 연결된 정점들 중 $A$에 속한 것의 개수가 많으면 $B$에 $v_i$를 넣고, $B$에 속한 것의 개수가 더 많으면 $A$에 $v_i$를 할당하면 됨을 알 수 있습니다. 

저렇게 하면 되는 이유는 어차피 $v_{i+1}, \dots, v_n$에 연결된 모든 간선이 Conditional expectation에 영향을 주는 요소는 $v_i$가 $A$에 들어가든 $B$에 들어가든 똑같고, 양쪽 끝이 $v_1, \dots, v_{i-1}$에 포함되는 간선 또한 이미 결정되어 있으므로 $v_i$와 $\{v_1, \dots, v_{i-1}\}$ 사이 간선만 생각하면 되기 때문입니다. 

따라서 최종적으로 아래와 같은 deterministic construction algorithm을 얻을 수 있습니다. 끝!

~~~
1. Initialize A = {} and B = {}
2. Assign v_1 to A or B, either way
3. Repeat for k = 2, ..., n:
	(a) Let N_A = {u in A | (v_k, u) in E} and
			N_B = {u in B | (v_k, u) in E}.
	(b) If |N_A|<=|N_B|, assign v_k to A,
		else, assign v_k to B.
~~~

Conditional Expectation을 이용한 Derandomization을 할 때 다른 부분을 설계하는 것은 그렇게 어렵지 않지만, conditional expectation을 구할 수 있는가? 가 중요합니다. 이거 못 구하면 말짱 도루묵인 알고리즘이 되기 때문이죠. General algorithm 문제에서 이 conditional expectation을 구하는 것이 쉽지 않다고 합니다. 그래서 일반적인 경우에서 derandomization하는 법이 아직 없는 것 같기도 하네요. 

### 여담
Latex 쓰는게 좀 익숙치가 않아서 쓰는게 엄청 빡세네요... 뭐 그래도 복습도 되고 Latex 연습도 되고 오히려 좋을지도?

## References
-   Mitzenmacher, M., & Upfal, E. (2005). Probability and computing: Randomization and probabilistic techniques in algorithms and data analysis. Cambridge university press.