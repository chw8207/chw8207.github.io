---
layout: post
title: Analysis of Recommendation Algorithms for E-Commerce
# image: 
#   path: /assets/img/blog/jeremy-bishop@0,5x.jpg
description: >
  E-Commerce의 등장으로 부각받는 추천시스템에 대해 살펴보고, 전통적 방법과 협업필터링 방법을 비교해보는 논문입니다.
sitemap: false
---

<!-- Version 9 is the most complete version of Hydejack yet.
{:.lead}

[Modernized](#linking-in-style) [design](#whats-in-the-cards), [big headlines](#ready-for-the-big-screen), big new features: [Built-In Search](#built-in-search), [Sticky Table of Contents](#sticky-table-of-contents), and [Auto-Hiding Navbar](#auto-hiding-navbar). That [and more](#and-much-more) is Hydejack 9.

- Table of Contents
{:toc .large-only} -->
## Introduction(서론)

추천시스템 논문에 본격적으로 들어가기에 앞서 서론 부분에 대해 살펴보겠습니다. 
요즈음 일상에서 우리는 E-Commerce라는 용어를 자주 접한다는 것을 많이 느끼실텐데요.
E-Commerce는 우리말로 하면 '전자 상거래'라는 뜻으로 대표적인 사이트로는 
아마존[Amazon](https://www.amazon.com/)이 있습니다. 이런 E-Commerce사이트에서는
고객들에게 수백만 가지의 상품을 제공하고 있어요. 제품이 너무 많다보니 저 역시 
이런 E-Commerce사이트에서 물건을 고르는 데 시간이 많이 걸렸는데요, 
이러한 문제점을 해결하기 위해 **추천시스템**이 등장하여 E-Commerce와 결합하였습니다.
추천시스템과 관련된 기법은 여러 가지가 있지만 그 중 **협업 필터링(CF)**기법은
가장 성공적이고 쉬운 모델 중 하나라고 여겨지고 있다고 해요. 그래서 이 논문에서 
협업 필터링에 대해 많이 다루고 있는거 같습니다. 그렇지만 협업 필터링이 당면한 과제는 
아래와 같습니다. 
- 알고리즘의 확장성
- 고객을 위한 추천의 질(quality)를 향상시키는 것
   - 특히 false positives(고객이 좋아하지 않는 물건 추천)

그럼 이번 논문에서 주로 어떤 내용을 다루는지 궁금하지 않으신가요?
이번 논문에서 다룰 내용은 크게 두 가지로 나눠서 볼 수 있습니다.
- 서로 다른 추천시스템에 대한 체계적인 실험적 평가를 제공
- E-commerce에서 흔한 희귀한 데이터에 맞는 새로운 알고리즘 개발

이번 논문에서 사용한 데이터셋은 **대형 E-Commerce(Fingerhut Coperations )**와
연구자가 직접 개발한 **[자체 추천리스템 리서치 사이트(MovieLens)](www.movielens.umn.edu)**입니다.

다음으로 연구의 목적 또는 기여하고자 하는 바에 대해 살펴보겠습니다. 
기여하고자 하는 바는 아래와 같이 세 가지로 요약할 수 있습니다.
- E-Commerce 사이트의 실제 데이터에 대한 추천시스템의 효과 분석
- original 협업 필터링&차원축소에 기반한 알고리즘&전통데이터알고리즘의 성능 비교
- 이전에 연구된 알고리즘보다 효율적이고, 매우 희귀한 데이터에서 퀄리티가 좋은 
  새로운 추천시스템 형성에 대한 접근

마지막으로 연구의 이론적 배경에 대해 살펴보겠습니다. 이론적 배경에 대해 간단히 살펴보고 넘어가면
논문 내용이 더 쉽게 다가온다는 생각이 들었습니다. 논문이 주로 **추천시스템 및 알고리즘 비교**이기 때문에
이 부분은 간략히 살펴보겠습니다. 이론적 배경으로는 크게 **KDD(Knowledge Discovery in Databases)**와
**차원 축소(Dimensionality Reduction)**이 있습니다. 
#### KDD(Knowledge Discovery in Databases)

KDD는 쉽게 말해 우리가 알고 있는 **데이터마이닝**이라고 생각하면 됩니다.
추천시스템에서도 데이터마이닝 방법이 사용되고 있는데, 
그 중 가장 많이 사용되는 방법이 **연관규칙**입니다. 
#### 차원축소(Dimensionality Reduction)

차원축소는 말 그대로 차원을 축소하는 기법인데, 추천시스템에서는
행렬의 행 또는 열을 축소시키는 것을 이야기하고 있습니다. 
차원축소기법 중 **주성분분석(PCA)**가 널리 이용되고 있으며,
**특이값 분해(SVD)**를 활용한 **LSI(잠재의미색인)**기법도 이용되고 있습니다.
## 방법론

서론에 대해 살펴본 후, 추천시스템의 방법론에 대해 살펴보겠습니다. 추천시스템의 방법론에서는 
아래와 같은 내용 순서대로 살펴보고 있었습니다.
- 추천시스템
- 전통적 데이터마이닝(연관규칙)
- 협업필터링

#### 추천시스템

방법론에서 먼저 등장한 내용은 추천시스템에 대한 전반적이 내용이었습니다. 
추천시스템에서 핵심 내용은 **<span style='color:red'>상위 N개의 항목을 생성하는 것</span>**입니다.
