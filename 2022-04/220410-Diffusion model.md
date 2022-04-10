+++

title = "Generative Modeling by Estimating Gradients of the Data Distribution"
date = "2022-04-10"
[profile]  
	enable = true  
	avatar = "/assets/img/yuho.jpg"  
	name = "Yuho Jeong"  
	github = "yuhodots"
	email = "yuho8437@unist.ac.kr"

+++

Diffusion model이라는 generative model의 새로운 방향성을 제시한 Yang Song 저자의 Generative Modeling by Estimating Gradients of the Data Distribution에 대해서 리뷰합니다.

<!--more-->

### Summary

#### Backgrounds

- 기존 generative modeling 방법

  - Likelihood-based models: autoregressive models / normalizing flow models / energy-based models (EBMs) / variational auto-encoders (VAEs) 등과 같이, PDF를 정의하고 해당 PDF의 likelihood를 maximize 하는 방법
  - Implicit generative models: generative adversarial network과 같이, 직접적으로 PDF를 모델링하지는 않는 방법

- 기존 방법의 한계점

  - Likelihood-based models: tractable normalizing constant를 보장하기 위해 모델 구조에 제약이 있고, true data distribution을 모르기 떄문에 surrogate objectives사용 (e.g. ELBO)
  - Implicit generative models: mode collapse가 발생하기도 하는 불안정한 adversarial training에 의존

- 저자가 새로 제안하는 방법

  - Score-based model: PDF를 모델링하는 것이 아닌, score function이라고 불리는 "log-PDF의 gradient" $ 
    \nabla_\mathbf{x} \log p(\mathbf{x}) \approx \mathbf{s}_\theta(\mathbf{x})$를 모델링하는 방법
    
- Score-based model은 tractable normalizing constant가 필요하지 않고 성능도 매우 좋으며 likelihood 계산도 가능


#### Score-based model

- 모델 학습 방법
  - 모델 $\mathbf{s}(\mathbf{x})$와 데이터의 $\nabla \log p(\mathbf{x})$ 사이의 squared L2를 최소화. 즉, Fisher divergence $\mathbb{E}_{p(\mathbf{x})}[|| \nabla\log p(\mathbf{x})-\mathbf{s}(\mathbf{x})||_2^2]$ 식을 최소화
  - 하지만 우리는 $p(\mathbf x)$에 대한 특정 포인트(소유하고있는 데이터) 정보만 알고있기 때문에 위의 식을 그대로 사용할 수 없음
  - 다행히도, true $ \nabla_\mathbf{x} \log p(\mathbf{x})$를 알지 못할 때 사용할 수 있는 score-matching이라는 방법이 존재
- 데이터 샘플링 방법 (테스트)
  - 임의의 prior $\mathbf x_0$에서 시작하여, 아래의 Langevin dynamics을 따라 $\mathbf x$를 계속해서 업데이트하면 됨 (Langevin dynamics 식 제작에 score function 필요)

![img](/assets/img/lagevin.png)

- Naive score-based generative modeling 
  - 전체적으로는, score-mathcing을 통해 score function을 먼저 모델링한 뒤에, 해당 score function을 가지고 정의된 Langevin dynamics을 따라 $\mathbf x$를 업데이트하여 최종 샘플링 포인트를 찾는 것 (Naive score-based generative modeling)
  - 하지만 Naive score-based generative modeling 방법은 low density regions에서는 정확하지 않다는 점 때문에, prior $\mathbf x_0$에서 시작하여 초기에 $\mathbf x$ 업데이트 과정에서 좋은 업데이트가 수행되지 않는다는 단점이 있음
- 개선 방법
  - Naive score-based generative modeling의 문제점을 개선하기 위해서, 데이터에 noise perturbation을 기반으로한 'Noise Conditional Score-Based Model'와 'annealed Langevin dynamics' 방법을 적용하였음
  - 자세한 내용은 [이 곳](https://yang-song.github.io/blog/2021/score/#score-based-generative-modeling-with-multiple-noise-perturbations) 참고

### Comments

- 해당 논문은 generative modeling 분야에 새로운 방향성을 제시한 논문으로, 후속 연구들이 계속해서 쏟아지고 있어서 기여가 큰 논문임
- Gradient of log PDF라는 새로운 관점을 제시한 점도 좋았지만, 개인적으로는 naive score-based generative modeling을 적용하였을 때 잘 되지 않았다는 것에서 멈추지 않고, 계속해서 개선점을 찾아내 결국엔 좋은 성능의 모델을 얻어냈다는 점이 좋았음

### References

- [Yang Song, Generative Modeling by Estimating Gradients of the Data Distribution](https://yang-song.github.io/blog/2021/score/)
- Song, Yang, and Stefano Ermon. "Generative modeling by estimating gradients of the data distribution." *Advances in Neural Information Processing Systems* 32 (2019).
