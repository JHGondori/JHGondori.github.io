---
title: Probabilistic Method - Sample and Modify
date: 2025-07-08 22:05:40 +0900
categories: [Mathematics, Probability]
tags: [mathematics, probability, probabilistic method]
math: true
---

> 중간에 좀 공백이 있었지만... 마저 꾸준히 쓰는걸로...!
## Sample and Modify
바로 전 post인 Derandomization에서 probabilistic method로 원하는 object를 무조건 얻어낼 수 있는 방법을 알아보았습니다. 요리조리 잘 하면서 randomness를 줄여서 원하는 속성을 만족하도록 구성했죠. 

지금까지 다룬 Probabilistic method에서는 directly하게 random structure를 원하는 특성을 만족하도록 구성해나가며 증명했었습니다. 그래프에서 바로 $1/2$의 확률로 간선을 색칠하거나.. 
정점을 두 개의 Set 중 하나에 집어넣어버리거나... 등등 이렇게 했었죠. 

**Sample and Modify**는 증명 과정을 두 부분으로 쪼개서 indirect하게 증명하는 방법입니다. 
일단 먼저 random하게 object를 생성하고(Sample), 그 다음 생성된 object를 잘(?) 조작해서(Modify) 원하는 object를 만들어내는 과정이라고 보시면 됩니다. 

이건 진짜 말로는 하나도 이해가 되지 않더라고요...(~~뭐 제대로 된 설명도 없는데~~) 그래서 예시와 함께 이해해봅시다.

### Example 1 (Independent Set)

만약 그래프가 $n$개의 정점과 $m$개의 간선을 가지고 있으면, 최소 $n^2/4m$ 개의 정점을 가지는 independent set을 가진다.

### Proof
짧고 굵죠... 일단 Independent set이 뭔지부터 알아봅시다.

#### Independent Set?
정의는 진짜 간단합니다. Graph $G = (V, E)$ 안의 Independent set $S\subseteq V$는 $\forall v, w\in S, (v, w)\notin E$인 집합입니다. 
다르게 생각하면 Graph $G$의 모든 간선은 많아야 한 개가 $S$에 속한다고 볼 수 있습니다. 

#### Back to Proof
다시 증명으로 돌아옵시다. 위에서도 말했지만, 증명은 두 부분으로 나뉘게 됩니다. 시작하기에 앞서 Graph vertices의 average degree $d = 2m/n$을 정의해 두겠습니다.

1. 먼저 각 정점에 대해 독립적으로 $1-1/d$ 의 확률으로 그래프에서 그 정점을 끝점으로 하는 모든 간선과 정점을 제거합니다.
2. 이렇게 만들어진 새로운 그래프에서 남아있는 각 간선에 대해 독립적으로 그 간선을 지우고, 그 간선의 양 끝 정점 중 하나를 제거합니다. 독립적으로 수행하기 때문에 제거되는 정점이 겹칠 수 있습니다.

이렇게 그래프를 수정하면, 2번 과정에서 모든 간선이 제거되므로 남는 정점들은 서로 연결될 수 없습니다. 즉, 남은 정점들은 확정적으로 Independent set이 됩니다.

이제 $X$를 1번 과정에서 남은 정점의 개수로 정의하고, $Y$를 1번 과정에서 남은 간선의 개수로 정의합시다. 2번 과정을 거치고 남는 정점의 개수는 최소 $X-Y$가 된다는 점을 알 수 있을 겁니다. 

그렇다면? $\mathbf{E}[X-Y]$를 구하면 되겠죠~

$\mathbf{E}[X]=n/d$ 라는 점은 쉽게 알 수 있습니다. $Y$의 기댓값은 양쪽 끝 정점이 살아남아야 간선 1개가 살아있을 것이기 때문에 아래와 같이 구할 수 있습니다.

$$
\mathbf{E}[Y] = \sum_{i=1}^{m} \Pr(Y_i=1) = m(1-(1-1/d))^2=\frac{nd}{2}\frac{1}{d^2}=\frac{n}{2d}
$$

따라서 $X-Y$의 기댓값은 아래와 같음을 알 수 있습니다.

$$
\mathbf{E}[X-Y] = \frac{n}{2d}=\frac{n^2}{4m}
$$

1, 2번 방법을 적용했을 때 나오는 Independent set의 정점 개수의 기댓값이 $n^2/4m$보다 크다는 것을 알아냈으므로, 
Expectation argument를 이용하면 Independent set의 정점 개수는 적어도 $n^2/4m$이라는 것을 알 수 있습니다.

---

이거만으로는 이해하기 어려우니... 하나만 더 보죠.

### Example 2 (Graph with large girth)
$k$가 3 이상이고, $n$이 충분히 크다면, $n$개의 정점을 가지는 그래프 중 적어도 $\frac{1}{4}n^{1+1/k}$ 개의 간선을 가지고, 적어도 girth $k$를 가지는 그래프가 존재한다.

#### Graph girth?
이거도 정의가 그렇게 어렵지는 않습니다. Graph girth는 graph가 포함하는 가장 길이가 짧은 cycle입니다. 만약 acyclic graph 같이 cycle이 없으면, graph girth는 무한으로 정의됩니다. 

예시로 rectangle graph는 girth 4이고, 여기에 중간 대각선을 추가하면 girth 3이 될 겁니다. 

직관적으로 그래프가 간선이 많아지면 많아질 수록 girth가 낮아질 것이라고 생각이 들 수 있지만, 간선의 밀도가 높아져도 girth가 큰 값일 수 있다는 것이 위 예제가 의미하는 뜻입니다. 
Wikipedia에 graph girth 문서에 들어가보니 간선의 개수가 많아도 잘 배치해서 girth를 크게 하는 경우에 대한 예시들이 있더라고요. 신기하네요.

아, 그리고 하나 더 알아봅시다.
#### Random graph models
이 문제를 풀 때 random graph model을 알면 수월합니다. Random graph models는 $|V|=n$인 무방향 그래프 $G = (V, E)$를 랜덤하게 고르는 모델입니다. 
1. $G_{n, p}$ model
	$G_{n, p}$ model은 모든 정점 쌍 $(u, v)$를 독립적으로 $p$의 확률로 간선 집합 $E$에 넣는 모델입니다. 
    이 $G_{n, p}$ model로 만들어진 그래프 중 $m$개의 간선을 가진 그래프가 만들어질 확률은 아래와 같이 나타나게 될 겁니다.

$$ 
p^m(1-p)^{n(n-1)/2-m}
$$

2. $G_{n, N}$ model
	$G_{n, N}$ model은 그냥 모든 가능한 정점 $n$개, 간선 $N$개의 무방향 그래프 중 하나를 서로 동등한 확률로 뽑는 모델입니다. 그렇다면 어떤 한 그래프가 뽑힐 확률은 아래와 같이 나타나게 될 겁니다.

$$
\binom{n(n-1)/2}{N}^{-1}
$$

#### Back to Proof
다시 증명으로 돌아와 봅시다. 아래와 같은 sample and modify를 하는 랜덤 알고리즘을 생각해봅시다.

1. $p=n^{1/k-1}$인 $G_{n, p}$에서 $G$ 하나를 가져옵니다.
2. $G$에서 길이가 $k-1$이하인 cycle 각각에 대해 간선 하나를 무작위로 지웁니다.

2번 과정이 끝나면 자명하게 girth가 $k$ 이상이 될 겁니다.

여기서 $X$를 1번 과정 후 남은 간선의 개수로 두고, $Y$를 1번 과정 후 $G$에 있는 cycle 중 길이가 $k-1$이하인 cycle 개수로 둡니다. 
그렇다면, 2번 과정 후 남는 간선의 개수는 $X-Y$ 이상일 겁니다. 즉, $\mathbf{E}[X-Y]$를 구하면 문제가 해결될 겁니다!

$\mathbf{E}[X]$는 $G_{n, p}$ model의 특징에 의해 각 간선이 뽑힐 확률이 $p$이므로 아래와 같이 나타날 것임을 알 수 있습니다.

$$ 
\mathbf{E}[X] = p\binom{n}{2} = \frac{1}{2}(n-1)n^{1/k}=\frac{1}{2}\left(1-\frac{1}{n}\right)n^{1+1/k}
$$

$\mathbf{E}[Y]$는 좀 어려워요. 일단 길이 $i$인 cycle을 생각해봅시다. $G_{n, p}$에서는 특정 길이 $i$ cycle이 생길 확률은 $p^i$입니다. 그리고 길이 $i$ cycle의 개수는 $\binom{n}{i}(i-1)!/2$입니다. 
$i$개를 고를 때 역순으로 ordering된 거는 서로 같은 것이기 때문에 염주순열로 생각해야 하기 때문에 저런 값이 나오게 됩니다. 이를 통해 아래 사실을 알 수 있습니다. (근사는 뭐... 이렇게 된다고 대강 보시면 됩니다.)

$$
\begin{align*}\mathbf{E}[Y] & = \sum_{i=3}^{k-1}\binom{n}{i}\frac{(i-1)!}{2}p^i\leq\sum_{i=3}^{k-1}n^i p^i \\
&= \sum_{i=3}^{k-1} n^{i/k}\leq (k-3)n^{(k-1)/k} \\
&\lt kn^{(k-1)/k}
\end{align*}
$$

진짜 rough하게 근사하긴 합니다. 뭐 생각 안하고 대충 근사 하는게 편하죠. 이제 다 끝났습니다. $X-Y$의 기댓값에 대한 식은 아래와 같이 나타나게 됩니다.

$$
\begin{align*}
\mathbf{E}[X-Y] & \gt \frac{1}{2}\left(1-\frac{1}{n}\right)n^{1+1/k} - kn^{(k-1)/k} \\
& = \frac{1}{2}\left(1-\frac{1}{n}-\frac{2k}{n^{2/k}}\right)n^{1+1/k} \\
& \geq \frac{1}{4} n^{1+1/k} \qquad\dots\mathsf{what?}
\end{align*}
$$

이게 마지막 식이 좀.. 너무 근사를 때려버리긴 하는데, (Wolfram alpha 왈 $k=100$이면 $n$이 $1.27\times 10^{130}$ 이상이어야 저 부등식이 성립한다네요. 얼탱) 뭐 $n$이 충분히 크다니까~

암튼 결론적으로 Expectation argument에 의해 $n$이 충분히 크면 적어도 $\frac{1}{4}n^{1+1/k}$개의 간선, girth $k$인 그래프가 존재한다는 사실을 알 수 있게 됩니다. 끝!

### 여담
Probabilistic method를 배우고 과제를 풀 때 Sample and Modify를 하는 문제가 없어서 제대로 이해했는지는 모르겠지만.. 에라 모르겠다~

## References
-   Mitzenmacher, M., & Upfal, E. (2005). Probability and computing: Randomization and probabilistic techniques in algorithms and data analysis. Cambridge university press.