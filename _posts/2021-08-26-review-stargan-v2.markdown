---
layout: post
title:  "[Paper Review] StarGAN v2: Diverse Image Synthesis for Multiple Domains"
subtitle:   "StarGAN v2"
categories: review
tags: review   
comments: true
---


## 개요
> Scalability와 Style Diversity 두마리 토끼를 모두 잡은 생성 모델, StarGAN v2를 소개합니다.

- 목차
	- [원본 논문](#원본-논문)  
	- [용어 정리](#용어-정리)  
	- [배경](#배경)  
	- [저자가 해결하고자 하는 문제](#저자가-해결하고자-하는-문제)
	- [문제 해결을 위해 도입한 방법론](#문제-해결을-위해-도입한-방법론)
	- [제안된 신경망 구조](#제안된-신경망-구조)
	- [해결방안을 도입한 근거](#해결방안을-도입한-근거)
	- [성과](#성과)
	- [한계](#한계)
	- [궁금한 점](#궁금한-점)


## 원본 논문
---
[Paper](https://arxiv.org/abs/1912.01865)

[Official Implementation](https://github.com/clovaai/stargan-v2)


## 용어 정리
---
* **I2I Translation**: Image-to-image Translation의 약자로 어떤 이미지에서 일부 특징들을 바꾼 다른 이미지로 변환하는 과정을 의미합니다.
* **Domain**: `시각적으로 구분할 수 있는 하나의 카테고리로 묶일 수 있는 이미지들의 집합`을 의미합니다. 주로 I2I 변환의 기준이 됩니다. 예를 들어 남자, 여자 등의 특정 성별이나 개, 고양이 등의 특정 종을 하나의 도메인으로 볼 수 있습니다. 비교적 그 정의가 명확한 편입니다.
* **Style**: `특정 이미지가 지닌 독특한 시각적 외향`을 의미합니다. I2I 변환에서는 Style이 다양하게 바뀌어도 도메인 분류에는 영향을 미치지 않습니다. 주로 이미지 내의 색깔이나 주요하지 않은 경계선들이 Style에 해당되며, 인물 사진의 경우 헤어스타일이나 피부색 등이 주로 Style로 분류됩니다. 비교적 그 정의가 모호한 편입니다.
* **Identity**: I2I 변환 과정에서도 바뀌지 않는 `특정 이미지가 지닌 고유한 특성`을 의미합니다. 주로 이미지 내의 주요한 경계선들이 Identity에 해당되며, 인물 사진의 경우 얼굴의 형태나 자세 등이 주로 Identity로 분류됩니다. Content라고도 부릅니다. 비교적 그 정의가 모호한 편입니다.
* **AdaIN**: Adaptive Instance Normalization의 약자입니다. AdaIN(x, s)는 x를 정규화한 뒤 s를 기준으로 다시 역정규화하여 x의 분포를 s의 분포로 변환하는 정규화 과정을 의미합니다. 수식은 아래와 같습니다.

<img src="/assets/img/post_img/stargan-v2-adain.PNG" width="300" height="100" />


## 배경
---
**좋은 I2I 변환 모델은 Scalability와 Style Diversity를 모두 갖춘 모델**입니다. 여기서 `Scalability`란 단일 신경망을 활용해 다중 도메인 간의 I2I 변환을 수행할 수 있는 특성을 의미하고, `Style Diversity`란 각각의 도메인 내에서도 다양한 스타일의 이미지를 생성할 수 있는 특성을 의미합니다. 즉, 좋은 I2I 변환 모델의 요건을 충족하기 위해서는 여러 도메인들로 자유롭게 확장할 수 있어야 하고 다양한 이미지들을 생성할 수 있어야 합니다.

StyleGAN 등 Style Diversity를 달성한 기존의 모델들은 단일 신경망으로 다중 도메인 간 I2I 변환을 할 수 없는 Scalability의 한계가 있었습니다. 다중 도메인 간 I2I 변환을 하기 위해서는 각기 다른 도메인 쌍에 대해서 학습시킨 여러 신경망을 활용해야 했습니다. 그렇기 때문에 K개의 도메인 간에 I2I 변환을 수행하기 위해 K(K-1)개의 생성 모델이 필요했습니다.

StarGAN 등 Scalability를 달성한 기존의 모델들은 하나의 도메인 내에서 다양한 스타일의 이미지를 생성하지 못하는 Style Diversity의 한계가 있었습니다. 사전에 정의된 도메인 라벨을 One Hot Vector 형식으로 활용했기 때문에, 모델이 각 도메인당 결정론적 매핑을 학습하여 같은 Source Image에 대해서는 각 도메인당 하나의 동일한 Output만을 생성했습니다. 이처럼 **기존에도 Scalability와 Style Diversity 중 하나를 갖춘 모델은 존재했으나, 이 둘을 모두 갖춘 모델은 없는 상황**이었습니다.


## 저자가 해결하고자 하는 문제
---
본 논문의 저자들은 다중 도메인으로 확장 가능할뿐만 아니라 다양한 스타일의 이미지를 생성할 수 있는 `Scalability와 Style Diversity를 모두 갖춘 신경망`을 만들고자 했습니다.


## 문제 해결을 위해 도입한 방법론
---
본 논문의 저자들은 Scalability를 갖춘 StarGAN에서 **Domain Label을 Style Code로 대체**하여 Style Diversity를 함께 달성하고자 했습니다. 여기서 Style Code란 이미지의 스타일이 임베딩된 벡터를 의미합니다. 본 논문에서는 임의의 Gaussian Noise를 Style code로 변환하는 과정을 학습하는 `Mapping Network`와 주어진 Reference Image에서 Style Code를 추출하는 과정을 학습하는 `Style Encoder`를 활용하여, 기존의 고정된 Domain Label을 다양한 스타일을 표현할 수 있는 Domain-specific Style Code로 대체했습니다. 이 외에도 R1 Regularization을 수행하고 Depth-wise Concatenation 대신 AdaIN 방식으로 Style을 Generator에 주입하여 학습 안정성을 개선하는 방법을 사용했습니다.


## 제안된 신경망 구조
---

<img src="/assets/img/post_img/stargan-v2-architecture.PNG" width="830" height="350" />


## 해결방안을 도입한 근거
---
* **Adversarial Loss**: Generator가 더 진짜같은 이미지를 생성하도록 하는 Loss입니다.

<img src="/assets/img/post_img/stargan-v2-adv-loss.PNG" width="300" height="100" />

* **Style Reconstruction Loss**: Generator가 이미지 생성에 Style Code를 활용하도록 강제하는 Loss입니다.

<img src="/assets/img/post_img/stargan-v2-sty-loss.PNG" width="300" height="60" />

* **Style Diversification Loss**: Generator가 더 다양한 Style의 이미지를 생성하도록 Image Space를 돌아다니게 만드는 Loss입니다.

<img src="/assets/img/post_img/stargan-v2-ds-loss.PNG" width="300" height="60" />

* **Cycle Consistency Loss**: Generator가 이미지의 고유한 Identity 자체는 보존하도록 하는 Loss입니다.

<img src="/assets/img/post_img/stargan-v2-cyc-loss.PNG" width="300" height="60" />

* **Full Objective**: 최종적인 Loss Function은 다음과 같습니다.

<img src="/assets/img/post_img/stargan-v2-full-objective.PNG" width="300" height="120"/>


## 성과
---
StarGAN v2를 이용하면 Latent Code를 Mapping Network에 넣어 생성한 Style Code나 Style Encoder를 통해 Reference Image에서 추출한 Style Code를 통해 특정한 스타일의 이미지를 생성할 수 있습니다. (Mapping Network를 이용한 생성 방식을 `Latent-guided Synthesis`, Style Encoder를 이용한 생성 방식을 `Reference-guided Synthesis`라고 부릅니다.)

StarGAN v2는 다음과 같은 4가지 장점을 가지고 있습니다,
1. **도메인에 대한 정보가 이미 Mapping Network를 통해 Style Code에 반영되어 있어서** Generator가 오직 Style Code에만 집중할 수 있습니다.
2. **Style Space가 고정되어있지 않고 학습에 의해 유연하게 얻어집니다.**
3. **모델이 다중 도메인으로 확장 가능하기 때문에 다양한 데이터셋의 훈련 데이터를 모두 활용할 수 있습니다.** 이 과정을 통해 Domain-invariant한 특징들을 더 잘 학습할 수 있고 Regularization Effect로 인해 처음 보는 샘플에 대해서도 더 좋은 일반화 성능을 나타냅니다.
4. **Domain-shared Style Code 대신 Domain-specific Style Code를 사용함으로써 더욱 다양한 Output을 생성**할 수 있습니다.

StarGAN v2는 Celeb-HQ 데이터셋과 AFHQ 데이터셋에 대한 `정량적인 평가(FID, LPIPS)`와 `정성적인 평가(AMT)` 결과, 기존의 다른 모델들보다 생성된 **이미지의 질(Visual Quality)**, **스타일의 다양성(Diversity)**, **다중 도메인으로의 확장 가능성(Scalability)** 측면에서 상대적으로 성능이 우수했습니다. 여기서 FID(Frechet Inception Distance)는 진짜 이미지들의 분포와 생성된 이미지들의 분포 사이의 거리를 의미하고, LPIPS(Learned Perceptual Image Patch Similarity)는 생성된 이미지의 다양성을을 의미합니다. AMT는 Amazon Turk라는 설문 기관에 조사를 의뢰하여 Visual Quality가 높고 Reference Image와 스타일이 비슷한 사진을 사람이 직접 고르는 방식으로 평가한 정성적 성능 지표입니다.

<img src="/assets/img/post_img/stargan-v2-eval1.PNG" width="400" height="200"/>

<img src="/assets/img/post_img/stargan-v2-eval2.PNG" width="400" height="200"/>

<img src="/assets/img/post_img/stargan-v2-eval3.PNG" width="400" height="200"/>


## 한계
---
* **학습 속도가 느립니다.** 본 논문에 의하면 8 Batch로 100K Iteration 학습을 수행하는데 1개의 Tesla V100 GPU를 이용하여 3일이 걸렸습니다. Inference에 소요되는 시간도 상대적으로 길어서 상용화를 위한 제품에 활용하기 위해서는 Pruning 등의 경량화 과정이 필요합니다.
* 기존의 생성 모델들보다 더 다양한 스타일의 분포를 학습하긴 하지만 **여전히 모든 스타일에 대한 전체적인 분포는 학습하지는 못합니다.**
* MWGAN과 달리 Inter-domain Loss를 적용하고 있지 않기 때문에 여러 도메인 간의 복잡한 관계를 학습하지는 못합니다. 따라서 Target Domain에서 생성된 이미지들의 분포가 MWGAN에 비해 Real Distribution에 상대적으로 덜 가깝습니다.


## 궁금한 점
---
* StarGAN v2에 MWGAN의 MMW Distance(Multi-marginal Wasserstein Distance)를 적용해볼 수는 없을까?
* FID와 LPIPS가 각각 Visual Quality와 Diversity를 평가하기에 가장 적절한 지표일까?
* 어떤 논리와 근거로 논문의 저자들은 Domain-specific Style Code가 Domain-shared Style Code보다 더 Output Diversity가 높다고 주장하고 있는 걸까?
* 미용, 성형, 패션, 예술 등의 분야에서 Reference-guided 이미지 합성을 통해 만들 수 있는 상용화 가능성이 있는 프로덕트는 없을까?
> 예를 들어 미용 분야에서는 고객이 원하는 헤어스타일의 인물 사진을 Reference Image로 입력하면 그 헤어스타일을 한 고객의 모습을 생성해주는 모델을 만들 수 있다. 또 성형 분야에서는 고객이 자신이 좋아하는 연예인의 사진을 Reference Image로 입력하면 고객 얼굴의 특정 부분을 해당 연예인처럼 성형한 후의 추정 얼굴을 생성해주는 모델을 만들 수도 있다. 패션 분야에서는 유명 디자이너가 만든 가방 사진을 Reference Image로 입력하면 비슷한 스타일의 지갑 디자인을 생성해주는 모델도 생각해볼 수 있다. 또는 고객이 원하는 스타일의 의상을 선택하면 해당 의상을 착용한 고객의 모습을 생성해주는 가상 피팅 서비스도 만들 수 있다.
* 본 논문에서 정의하고 있는 Style과 Identity의 정의에 모호한 측면이 있다. 더 수학적으로 엄밀히 정의할 수는 없을까?
> 내 생각은 다음과 같다. Domain은 시각적으로 구분할 수 있는 하나의 카테고리로 묶일 수 있는 이미지들의 집합이다. Domain을 시각적으로 구분할 수 있도록 하는 특징들을 Domain의 Feature Set이라고 하자. Identity는 학습 과정에서 Cycle Consistency Loss를 통해 보존되는 Feature Set이다. Cycle Consistency Loss를 학습에 적용하는 방식에 따라 Identity를 유동적으로 변경할 수 있다. Style은 특정 이미지의 전체 Feature Set에서 Identity와 Domain의 Feature Set을 제외한 차집합이다. 따라서 Domain과 Identity를 어떻게 설정하느냐에 따라서 Style의 범위 또한 바뀐다. 마지막으로 Domain-specific Style Code란 Style에 Domain의 Feature Set에 대한 정보를 합한 벡터이다. 
* 이미지 속 다양한 Feature들의 Combination 중에서 특정 Combination을 선택하여 각각을 Style, Domain, Identity로 설정할 수는 없을까?
* Self-supervised Learning에서 사진의 일부를 Masking하는 방법을 응용하여 Cycle Consistency Loss를 특정 Feature Set에만 적용시키지 않는 방법은 없을까? 또는 데이터 전처리가 아닌 모델링 구조를 통해 이러한 Style과 Identity의 구분을 하이퍼파라미터로 조금 더 유연하게 설정할수는 없을까?
> 예를 들어 특정 연예인의 코로 성형한 내 모습을 보고 싶으면 코의 모양만을 Identity에서 제외시키고 Style로 포함시킬 수는 없을까?
