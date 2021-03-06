---
layout: post
comments: true
title: 형태소분석
tags: [machineLeanrning]
---

### 형태소 분석
`형태소`란 국어사전 정의로, 뜻을 가진 가장 작은 말의 단위 이다.  
형태소 분석은 자연어처리에서 가장 근간이 되는 분석으로, 인간의 언어 현상을 컴퓨터와 같은 기계에서 이용해서 모사할수 있도록 하기 위한것이다. 

예를 들어보자, `아버지가 방에 들어가신다.`라는 구문을 형태소 분석을 해보면
`아버지 + 가 + 방에 + 들어가 + 시 + ㄴ다`   
다음과같이 쪼개어지고 형태소 분석에서는 품사 까지 태깅하며 분석을 하게된다.
`아버지/NNG + 가/JKM + 방/NNG + 에/JKM + 들어가/VV + 시/EPH + ㄴ다/EFN`   

### 품사 태그 (kkma 기준)

| 태그 | 품사 |
| :--: |:--: |
| NN | 명사 |
| NR | 수사 |
| NP | 대명사 |
| VV | 동사 |
| VA | 형용사 |
| VX | 보조사 |
| VC | 지정사 |
| MD | 관형사 |
| MA | 부사 |
| I C | 감탄사 |
| JK | 조사 |
| JC | 접속조사 |
| JX | 보조사 |
| EP | 선어말 어미 |
| EF | 종결 어미 |
| EC | 연결 어미 |
| ET | 전성 어미 |
| XP | 접두사 |
| XS | 접미사 |
| XR | 어근 |
| SF | 마침표,물음표,느낌표 |
| SE | 줄임표 |
| SS | 따옴표,괄호표,줄표 |
| SP | 쉼표,가운뎃점,콜론,빗금 |
| SO | 붙임표 |
| SW | 기타기호 |
| OH | 한자 |
| OL | 외국어 |
| ON | 숫자 |
| UN | 명사추정범주 |
 
다음과같은 태그들로 형태소를 분류한다.

### 파이썬 형태소분석기 KoNLPy

KoNLPy는 파이썬에서 여러 형태소분석기를 합쳐둔 패키지이다. 주로 사용되는 패키지들을 정리해보자면
- Kkma
- Komoran
- Hannanum
- Twitter
- Mecab

다음과같은 형태소 분석기들이 있는데 각각마다 성능,속도가 다르니 목적에 맞는 분석기를 선택해 사용하는것이 좋을 것이다.



