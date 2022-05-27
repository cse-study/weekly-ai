+++
title = "Data Augmentation for Deep Learning"
date = "2022-05-27"
[profile]  
	enable = true  
	avatar = "/assets/img/yuho.jpg"  
	name = "Yuho Jeong"  
	github = "yuhodots"
	email = "yuho8437@unist.ac.kr"
+++

Deep Learning 모델 성능 개선을 위한 Data Augmentation 방법들과 효과를 정리합니다.

<!--more-->

### Mixup (ICLR 2018)

- https://arxiv.org/pdf/1710.09412.pdf
- 한 줄 요약: 두 개의 샘플에 대해서, input space와 output space를 각각 동일한 비율로 linear interpolate한 샘플 생성
- 장점/효과: Decision boundarie가 클래스에서 클래스로 선형적으로 변하기 때문에 더 smoother한 uncertainty estimation 제공

### Manifold Mixup (ICML 2019)

- https://arxiv.org/abs/1806.05236
- 한 줄 요약: Itermediate layer의 representation을 mixup하는 방법
- 장점/효과: class-specific representations을 flatten하는 효과를 가짐. 그리고 이 flat representation에 대해서 학습때 보지 못했거나 data manifold를 벗어난 샘플은 low-confidence로 예측. 즉, 헷갈리는 샘플을 어떻게든 하나의 class로 할당하기 보다는, uncertainty 높은(어느 하나로 확신하지 않는) 예측을 뱉음

### AugMix (ICLR 2020)

- https://arxiv.org/pdf/1912.02781.pdf
- 한 줄 요약: 두 개의 샘플을 합치는 방법이 아닌, 하나의 샘플에 여러 복합적인 augmentation 방법 적용한 뒤에도 동일한 예측을 하도록 KLD 형태의 ConsistencyLoss를 regularizer로 사용하는 방법
- 장점/효과: Robustness 관점에서 좋은 성능 (Noise에 강건함)

### AutoAugment (CVPR 2019)

- https://arxiv.org/pdf/1805.09501.pdf
- 한 줄 요약: 최적의 augmentation policy를 찾도록 RL 기반 학습

### References

- Shorten, Connor, and Taghi M. Khoshgoftaar. "A survey on image data augmentation for deep learning." Journal of big data 6.1 (2019): 1-48
