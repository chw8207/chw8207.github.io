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
# Introduction(서론)

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
### 협업 필터링이 당면한 과제
- 알고리즘의 확장성
- 고객을 위한 추천의 질(quality)를 향상시키는 것
   - 특히 false positives(고객이 좋아하지 않는 물건 추천)

논문에서 주로 다루는 내용을 두 가지로 정리해볼 수 있습니다.
- 서로 다른 추천시스템에 대한 체계적인 실험적 평가를 제공
- E-Commerce사이트에서 흔하게 나타나는 희귀한 데이터(sparse data)에 맞는 새로운 알고리즘 개발
## Ready for the Big Screen
