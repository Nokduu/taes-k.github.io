---
layout: default
comments: true
title: (BSN) 2.프로젝트 기획
parent: 프로젝트 진행기
date: 2019.06.08
---

<h1>{{ page.title }}</h1>  
<div style="text-align:right; font-size:11px; color:#aaa">{{ page.date }} </div>

---

본 프로젝트는 다음 링크를통해 확인하실수 있습니다.  
  
Homepage : <http://www.stocknews.me>  
Github : <https://github.com/taes-k/stock_analysis>  

---

## 2.프로젝트 기획

이 프로젝트를 완성시키기위해 저는 다음과 같은 요구사항들을 정리했습니다. 

> 1\. 뉴스기사들을 실시간으로 크롤링 해야한다.  
> 2\. 크롤링한 뉴스기사들을 분석해서 호의적인 기사인지 부정적인 기사인지 판단할수 있어야 한다.  
> 3\. 크롤링한 뉴스기사와 관련된 상장기업을 찾아야한다. (다수)  
> 4\. 기업별로 호재/악재가 상이 해야한다.  
> 5\. 실시간으로 뉴스가 업데이트되며 보여 줄 수 있어야 한다.    
  
위에서 정리한 요구사항에 따라 이제 다음과같은 기술 스택 및 알고리즘을 만들어 보았습니다.  
  
***1. 뉴스기사들을 실시간으로 크롤링 해야한다.***  

인터넷 뉴스를 크롤링 하기위해 찾아보니 대부분의 인터넷 뉴스들은 카테고리별로 나누어져 최신 뉴스들을 확인하는데 많은 오버헤드가 들어갔습니다. 그러다가 [네이버뉴스 속보](https://news.naver.com/main/list.nhn?mode=LSD&mid=sec&sid1=001) 에서는 종합적인 뉴스들이 1분에 5-10개의 뉴스들이 실시간으로 업데이트되고 있음을 확인하여 해당 뉴스탭을 사용하기로 정했습니다.  
  
***2\. 크롤링한 뉴스기사들을 분석해서 호의적인 기사인지 부정적인 기사인지 판단할수 있어야 한다.***  
  
이 요구조건을 만족시키는 알고리즘을 만드는것이 가장 핵심이라고 생각했습니다. 하지만 꽤나 단순하게 생각하여 다음과같은 알고리즘을 구성했습니다.  
> 1\. 뉴스 제목을 형태소 분석을 통해 쪼개기  
> 2\. 형태소별 Positive 점수를 매긴 샘플 Positive 딕셔너리 제작   
> 3\. 결과로써 나온 점수를 반영해 Positive 딕셔너리 반영 (학습)   

***3\. 크롤링한 뉴스기사와 관련된 상장기업을 찾아야한다. (다수)***
  
가장먼저, 상장기업 테이블이 필요했습니다. 이 데이터는 KRX [주식공시시스템](http://kind.krx.co.kr/corpgeneral/corpList.do?method=loadInitPage) 사이트 에서 얻을수 있었습니다.  
  
이제 뉴스기사와 상장기업간의 연관성을 찾기위해 가장먼저 뉴스를 키워드화 시키는것이 필요하다고 생각했습니다.  
> 1\. 뉴스 제목, 본문을 형태소 분석을 통해 쪼개기   
> 2\. 제목에서 나오는 형태소와 본문에서 나오는 형태소의 가점을 다르게해 제목에서 키워드 추출 확률을 높임  
  
다음과 같은 조건을 통해 뉴스별로 상위 5개의 키워드를 추출한 후 해당 키워드 내에서 상장기업명이 있을시 해당 키워드 리스트를 상장기업명과 매칭시켜 데이터 딕셔너리로 저장시켜주는 알고리즘을 구성했습니다.  
> 1\. 뉴스별 상위 5개 키워드 추출후 상장기업명 포함시 데이터 딕셔너리로 저장 (학습)  
> 2\. 키워드 별 상장기업과 연관성의 크기가 다를수 있으므로 점수를 따로 저장  
> 3\. 해당 데이터 딕셔너리의 경우 과거 뉴스데이터들을 학습시켜 미리 초기 사전을 구축해 두도록 함  
  
위의 사전 과정이 완료되었으면 이제 뉴스별로 연관 상장기업들 데이터를 추출할수 있습니다.  
> 1\. 뉴스별 상위 5개 키워드 추출  
> 2\. 키워드별 데이터 딕셔너리를 통해 회사 연관 점수 계산
> 3\. 일정 점수 이상인 상장기업 데이터 추출

***4\. 기업별로 호재/악재가 상이 해야한다.***  
 
이 내용의 경우 하나의 키워드가 회사마다 관련성의 정도와 방향이 다르다는 요구조건 이었습니다. 이 요구조건을 해결하기위해 (3)요구조건에서 키워드와 상장기업별로 -1 ~ +1 의 실수형 점수로써 구분을 주었습니다.  
  
***5\. 실시간으로 뉴스가 업데이트되며 보여 줄 수 있어야 한다.***  
  
뷰단에서 모듈형으로 잦은 업데이트에 적합한 리액트로 구성하기로 했습니다.  

---

## 결정된 스택

위의 요구조건들을 만족시키기위해 다음과 같은 기술스택들로 개발을 하기로 결정했습니다.   

<div style="text-align:center; margin: 50px 0;">
<img src="https://taes-k.github.io/assets/images/project/bsn_2_plan/python.png" style="height:60px; margin:0 30px;">
<img src="https://taes-k.github.io/assets/images/project/bsn_2_plan/django.png" style="height:60px; margin:0 30px;">
<img src="https://taes-k.github.io/assets/images/project/bsn_2_plan/react.png" style="height:60px; margin:0 30px;">
</div>  
  
파이썬을 선택한 이유는 크롤링과 형태소분석을 위한 라이브러리들이 잘 구성되어있기 때문입니다. 또한 Django를 통해 간단하게 API 웹서버를 만들어 React front-end와의 연동이 가능하다고 판단 되었기 때문입니다.    

자 이제 다음은 개발기로 이어집니다!  

---