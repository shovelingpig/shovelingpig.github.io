---
layout: post
title:  "[Portfolio] 서울대생들을 위한 강의 로드맵 사이트, SNUGH"
subtitle:   "SNUGH"
categories: portfolio
tags: portfolio   
comments: true
---


## 개요
> 삽질하는 뚱땡이의 서울대학교 강의 로드맵 사이트, '스누그'를 소개합니다. 
  
- 목차
	- [스누그는 어떤 웹사이트일까요](#스누그는-어떤-웹사이트일까요)  
	- [스누그의 차별화 포인트](#스누그의-차별화-포인트)
	- [스누그의 핵심 고객](#스누그의-핵심-고객)
	- [스누그의 기술 스택](#스누그의-기술-스택)
	- [스누그를 만든 사람들](#스누그를-만든-사람들)
	- [스누그를 만들며 느낀 점](#스누그를-만들며-느낀-점)
  
  
## 스누그는 어떤 웹사이트일까요
---
스누그(SNU Graduation Helper)는 대학생들이 `장기적인 강의 로드맵`을 그리도록 도와주고, 해당 강의 로드맵에 대한 `졸업 시뮬레이션` 결과를 제공하는 사이트에요. 요즘들어 복수전공이나 부전공, 연합전공 등을 하는 학생들의 수가 엄청나게 늘어나고 있잖아요? 스누그는 이러한 추세 속에서 대학생들이 적절한 강의를 적절한 시기에 수강할 수 있도록 도와주고 복잡한 졸업요건들을 체계적으로 관리해줘요.

<img src="/assets/img/post_img/snugh_logo.png" width="100" height="100" />


## 스누그의 차별화 포인트
---
* 스누그는 `서울대학교의 10년치 강의 데이터와 졸업요건 데이터`를 가지고 있어요.

<img src="/assets/img/post_img/snugh_main_web1.png" width="700" height="400" />

* 스누그를 이용하면 `입학부터 졸업까지 장기적인 강의 로드맵`을 만들 수 있어요.

<img src="/assets/img/post_img/snugh_main_web2.png" width="700" height="400" />

* 스누그는 강의 로드맵에 대한 `졸업 시뮬레이션 기능`을 제공해요.

<img src="/assets/img/post_img/snugh_main_web3.png" width="400" height="550" />


## 스누그의 핵심 고객
---
스누그는 `대학교 강의에 진심인 모든 서울대 학생들`을 위해 만들어졌어요. 특히 `복수전공이나 부전공` 등을 하는 학생들이 빠르게 늘어나는 추세 속에서, `복잡한 졸업요건을 관리`하기 힘들어하는 서울대 친구들을 돕기 위해 스누그는 탄생했답니다. 비싼 등록금을 내고 대한민국 최고의 교수님들께 수업을 들을 수 있는 값진 기회인데 자신에게 적절한 강의를 적절한 시기에 효율적으로 들을 수 있다면 얼마나 좋을까요? 현재 스누그는 비록 서울대 학생들만 이용할 수 있지만 점차 지원하는 대학을 늘려나갈 계획이에요. 제 2의 스누그(SNUGH)인 유그(YUGH)나 쿠그(KUGH) 등이 만들어지는 날이 어서 왔으면 좋겠네요.


## 스누그의 기술 스택
---
### Frontend
* TypeScript
* Svelte
* AWS (Amplify)

### Backend
* Django & DRF
* MySQL
* Redis
* Docker & Docker Compose
* AWS (EC2, RDS)


## 스누그를 만든 사람들
---
스누그는 `서울대학교 웹/앱개발 동아리 와플 스튜디오`의 베이비 암모나이트 팀이 만들었어요.


## 스누그를 만들며 느낀 점
---
스누그는 삽질하는 뚱땡이가 와플 스튜디오에서 백엔드 세미나를 수강하고 `처음으로 백엔드 개발자로 활동했던 프로젝트`입니다. 안드로이드 개발을 할 때에는 백엔드는 당연히 엄청 어려운 것이겠지라는 막연한 생각이 있었는데, 실제로 벡엔드 개발에 뛰어들어보니 정말 흥미롭고 재미있는 이슈들이 많은 분야였어요. 백엔드 세미나에서 배운 내용을 바탕으로 새로운 API들을 하나하나 만들어가고 막히는 부분이 생기면 동아리 선배님들께 질문하여 해결하니 서버 개발도 생각보다 어렵지 않다는 것을 깨달았어요. 

`Django라는 파이썬 웹개발 프레임워크는 Routing이나 ORM, Serialize 등의 여러가지 고급 기능들을 적절한 추상화의 수준에서 편리하게 제공`하고 있어서 초심자인 저도 주요한 서버 개념들을 쉽게 이해할 수 있었어요. 물론 향후 대규모의 서비스에서는 안정성을 위해 정적 타이핑을 사용하고 IoC 개념이 효과적으로 적용된 Java(Kotlin) 진영의 Spring Framework를 공부해서 사용하는 게 좋겠지만, 백엔드 개발을 처음 시작하는 초심자에게는 Django도 굉장히 좋은 선택인 것 같아요.

많은 개발자 분들이 자신에게 프론트엔드가 더 잘 맞는지 백엔드가 더 잘 맞는지 자주 고민을 합니다. 하지만 저는 개인적으로 데이터를 비동기적으로 받아와서 UI에 적절한 디자인으로 표시하고 컴포넌트들의 라이프사이클을 관리하는 일이 대부분인 프론트엔드 개발보다, `대량의 데이터를 저장 및 관리하고 적절한 형태로 가공하여 여러 클라이언트에게 다양한 루트로 서빙하는 백엔드 개발`이 더 재밌는 것 같아요. 또 이번 프로젝트에서 AWS를 통한 서버 인프라 관리를 수행해보았는데 DevOps도 정말 재미있는 분야라는 것을 깨달았습니다. `Github Action을 이용해서 배포 자동화를 구축하고 처음으로 Release Branch에 Push를 했을 때 느꼈던 쾌감`은 아직도 잊을 수가 없어요.

개발이라는 분야가 어떤 사람에게는 지루한 업무일수도 있겠지만, 적어도 저같이 적성에 맡는 사람들에게는 정말 늘 새롭고 짜릿한 분야인 것 같아요. 저도 얼른 회사에 들어가서 실무를 경험해보고 싶네요. 편안한 사무실에 앉아서 공부도 하고 개발도 할 수 있는데 돈까지 주다니... 그것이 덕업일치. 얼른 현업 개발자가 되서 여러가지 신기한 프로덕트들을 만들어보고 싶어요. 현업 개발자가 되는 그 날까지 누구보다 열심히 공부하고 다양한 경험을 쌓기 위해 노력할 거에요.

> "성공의 열쇠는 취미를 직업으로 삼는 것이다." - 카를라