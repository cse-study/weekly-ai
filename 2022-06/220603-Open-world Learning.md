+++
title = "Open-world Learning"
date = "2022-06-03"
[profile]  
	enable = true  
	avatar = "/assets/img/yuho.jpg"  
	name = "Yuho Jeong"  
	github = "yuhodots"
	email = "yuho8437@unist.ac.kr"

+++

Chen, Zhiyuan, and Bing Liu의 "Lifelong machine learning." chapeter 5, Open-world Learning을 읽고 간단하게 정리합니다.

<!--more-->

### Problem Definition

- Closed-world assumption: 모든 테스트 클래스가 이미 학습 과정에서 본 것들로 이루어짐
- Open-world learning: 모델 테스트 단계에서 이전에 본 적 없는 클래스가 입력되는 경우에, scratch부터 재학습 시키지 않더라도 모델이 대응할 수 있어야 함. 관련된 용어로는 cumulative learning 혹은 open-world recognition 등이 존재

1. $N$개의 class에 대해 학습한 모델이 테스트에서 해당 $N$개에 속하지 않는 unseen class를 발견한 경우, 이를 rejected $R$ set에 보관
2. $R$ set에서 $k$개의 unseen class를 인식하고, 각 class에 알맞게 학습 데이터 (자동으로) 수집
3. 충분한 데이터가 쌓였다면 $k$개 class에 대한 incremental learning을 통해 $N+k$ class의 지식을 지닌 모델로 업데이트

### How to Solve?: CBS Learning

- CBS Learning: center-based similarity space learning
- Classification 하려는 target class의 center feature $c$와 sample feature의, feature space 상에서의 similarity가 높도록 학습

### Deep Open Classification (DOC)

- 1-vs.-rest layer: Softmax를 사용하는 대신 $N$개의 sigmoid layer를 last layer로 사용함. 모든 sigmoid output에 대해서 threshold $t$ (default=0.5)를 넘지 못하면 reject(unseen class로 취급)함. 그리고 reject되지 않은 경우에는 제일 높은 sigmoid output을 가진 class를 선택함.
- Basic DOC는 1-vs.-rest layer를 사용하며, 당시(2017) SOTA 성능을 보였음
- 근데 생각보다 0.5 threshold를 넘어가는 unseen class가 많았음. 따라서 threshold를 통계 기반으로 정밀하게 조절할 수 있는 방법을 고안했더니 더 성능이 올랐음 (자세한 내용 책 직접 참고)

### References

- Chen, Zhiyuan, and Bing Liu. "Lifelong machine learning." *Synthesis Lectures on Artificial Intelligence and Machine Learning* 12.3 (2018): 1-207

