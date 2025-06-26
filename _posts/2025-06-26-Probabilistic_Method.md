---
title: Probabilistic Method
date: 2025-06-26 23:50:40 +0900
categories: [Mathematics, Probability]
tags: [mathematics, probability, probabilistic method]
---

> 대학교에서 공학수학을 들으며 재미있었던 내용이라 적어보려 한다!

## 들어가며
**Probabilistic method**는 어떤 특정한 조건을 만족하는 combinatorial object의 존재성을 증명하는 방법 중에 하나입니다.  Combinatorial object는 순열, 조합, 그래프, 트리같은 느낌의 뭔가 성질이 있고, 뭔가를 셀 수 있는 구조(?) 라고 보시면 됩니다.  

Probabilistic method의 기초가 되는 아이디어는 굉장히 간단합니다. 가능한 모든 combinatorial object의 sample space를 생각해봅시다. 예시로 그래프 간선을 색칠한다고 했을 때 가능한 모든 색칠법을 생각해본다는 그런 느낌입니다.

이제 이 sample space에서 랜덤하게 하나를 선택할 때 특정 조건을 만족하는 combinatorial object를 뽑을 확률이 0보다 크다면 sample space에 그 조건을 만족하는 object가 무조건 한 개 이상 존재한다는 것을 알 수 있습니다. 

즉, Probabilistic method는 combinatorial object의 적절한 distribution을 잡아서 그 분포에서 랜덤하게 뽑을 때 조건을 만족할 확률이 0보다 큼을 증명함으로써 존재성을 증명하는 방법입니다. 

이렇게 Probabilistic method에 대해 간략하게 알아보았고, 구체적인 내용은 아래 순서대로 작성할 것 같습니다. (Maybe?)

1. The Basic Counting Argument
2. Expectation Argument
3. Sample and Modify
4. Second Moment Method
5. Conditional Expectation Inequality
6. Proof of Lovász Local Lemma
7. Applications of Lovász Local Lemma

개요는 이쯤에서 끝마치고... 이제 본 게임을 시작해봅시다. :)

## References
-   Mitzenmacher, M., & Upfal, E. (2005). Probability and computing: Randomization and probabilistic techniques in algorithms and data analysis. Cambridge university press.
