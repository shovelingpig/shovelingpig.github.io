---
layout: post
title:  "[Portfolio] 최저임금에 비례한 지각비 관리 앱, Finger Call"
subtitle:   "Finger Call"
categories: portfolio
tags: portfolio   
comments: true
---


## 개요
> 삽질하는 뚱땡이가 개발한 두번째 모바일 앱, '핑거콜'을 소개합니다. 
  
- 목차
	- [핑거콜은 어떤 앱일까요](#핑거콜은-어떤-앱일까요)  
	- [핑거콜의 차별화 포인트](#핑거콜의-차별화-포인트)
	- [핑거콜의 핵심 고객](#핑거콜의-핵심-고객)
	- [핑거콜의 기술 스택](#핑거콜의-기술-스택)
	- [핑거콜을 만든 사람들](#핑거콜을-만든-사람들)
	- [핑거콜을 만들며 느낀 점](#핑거콜을-만들며-느낀-점)
  
  
## 핑거콜은 어떤 앱일까요
---
핑거콜(Finger Call)은 동아리나 스타트업, 교실 등의 집단공동체에서 `지각비를 자동으로 관리`하기 위한 모바일 앱입니다.

<img src="/assets/img/post_img/fingercall_logo.png" width="100" height="100" />


## 핑거콜의 차별화 포인트
---
지금 당신이 소속되어 있는 팀에서 핑거콜을 사용하면 어떤 점들이 유용할까요?

* 팀의 `모임 장소, 날짜, 인원 등을 체계적으로 관리`할 수 있어요.
* 아직 도착하지 않은 팀원의 `실시간 위치를 문자로 공유`받을 수 있어요.
* `최저시급의 70%에 비례한 초당 지각비`가 실시간으로 올라가는 모습을 흥미롭게 지켜볼 수 있어요.
* 실시간으로 누적되는 지각비를 바탕으로 지각하는 팀원에게 `재촉 문자`를 보낼 수 있어요.
* `팀 내 분위기를 유쾌하게 유지`하면서도 팀원들의 지각 비율을 효과적으로 줄일 수 있어요.

<img src="/assets/img/post_img/fingercall_main.png" width="300" height="500" />


## 핑거콜의 핵심 고객
---
핑거콜은 `시간을 엄수하는 것이 중요한 모든 형태의 집단`을 위해 만들어졌어요. 어떻게 하면 팀의 사기를 떨어뜨리지 않으면서도 팀 내 지각 비율을 효과적으로 떨어뜨릴 수 있을지 고민을 많이 했죠. 저희는 지각이라는 문제를 유쾌하게 해결해보고 싶었어요. 그래서 최저임금 비례 실시간 지각비나 재촉 문자와 같은 `게임성 요소`들을 앱 내에 최대한 자연스럽게 녹여냈답니다. 저희 서비스는 특히 아래와 같은 집단에서 사용하면 효과적이에요.

* 말썽쟁이 아이들이 많은 `학교`나 `학원`의 교실
* 팀원들끼리 아직 서먹서먹한 `동아리`, `소모임`, `조별과제`
* 아직 체계가 명확히 정립되지 않은 `스타트업`


## 핑거콜의 기술 스택
---
### Mobile
* Android (Java)
* MVP Architecture
* RxJava
* OkHttp, Retrofit
* Google Map SDK

### Backend
* Django
* MySQL
* Redis
* AWS (EC2, RDS)


## 핑거콜을 만든 사람들
---
핑거콜은 `서울대학교 창업 동아리 멜팅팟`의 2기 회원들이 만들었답니다. 삽질하는 뚱땡이의 학과 친구인 굳센 바위를 중심으로 팀이 결성되었고, 수차례의 아이디어 회의를 통해 많은 후보군 중에 핑거콜을 선택하게 되었어요. 핑거콜을 선택한 이유는 다름이 아니라 저희 팀에서 가장 유용하게 쓸 것 같았던 앱이기 때문이에요. 저희 팀에서도 어느날 지각비를 걷기 시작했는데 놀랍게도 그 날부터 지각률이 급격하게 줄어들었답니다. 경제적 유인이 심리에 미치는 영향이 생각보다 강력하다는 것을 깨달았어요.


## 핑거콜을 만들며 느낀 점
---
핑거콜은 혹시 다른 팀들도 우리처럼 `지각을 어떻게 관리해야 할 지 난처한 상황`이 있지 않을까 하는 문제의식에서 시작된 서비스에요. 타인을 알기 위해서는 먼저 자신을 들여다보라는 말이 있잖아요. 저희 팀 내부의 문제를 먼저 들여다보니 다른 사람들의 Pain Point도 보이기 시작했어요. `시간 엄수(Punctuality)`는 모든 조직에서 가장 기본이 되면서도 강제하기 어려운 규칙인 것 같아요. 하지만 여러 사람이 서로 협업하는 업무일수록 시간을 엄수하지 않았을 때 발생하는 손해는 기하급수적으로 전달됩니다. 그렇기 때문에 팀이 앞으로 꾸준히 전진하기 위해서는 팀원들 개개인이 모두 시간을 엄중히 지키는 것이 필요한 것 같아요. 핑거콜을 만드느라 밤도 많이 새고 고생도 많이 했지만, `조직 내에서 철저히 시간을 지켜야 하는 이유`에 대해 깊게 생각해볼 수 있었던 좋은 기회였던 것 같아요.

> "시간 엄수는 비지니스의 영혼이다" - 토마스 할리버튼