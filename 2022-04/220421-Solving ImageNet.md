+++

title = "Solving ImageNet"
date = "2022-04-21"
[profile]  
	enable = true  
	avatar = "/assets/img/yuho.jpg"  
	name = "Yuho Jeong"  
	github = "yuhodots"
	email = "yuho8437@unist.ac.kr"

+++

이번 달에 알리바바 그룹에서 발표한 "Solving ImageNet: a Unified Scheme for Training any Backbone to Top Results" 논문을 읽고 리뷰합니다.

<!--more-->

### Summary

- 새로운 방법을 제안하는 논문은 아니고 technical report에 가까움
- ImageNet dataset에 대해서, 어떤 모델 구조더라도 하이퍼파라미터 튜닝 없이 동일하게 적용할 수 있는 USI(Unified Scheme for ImageNet)을 제안. Knowledge distillation과 몇 가지 modern tricks를 사용하였고, 모든 모델에 대해서 previous SOTA를 넘었음
- TResNet-L 구조의 teacher model과 더불어 논문에서 제안하는 하이퍼파라미터를 사용하면, CNN, Transformer, Mobile-oriented, MLP-only 형태의 student 모델에 대해서 모두 성능이 개선된다고 함
- 일반적인 knowledge distillation 형태(vanilla KD)와 동일하게, true label y에 대해서는 cross entropy loss를 사용하고, teacher label에 대해서는 temperature를 사용하여 soft label을 만든 뒤에 student prediction과 KLD를 계산함

### Comments

- Hyper-parameter tuning이 매우 time-consuming한 작업이지만 중요하기 때문에 모든 연구에서 어쩔 수 없이 수행해야했는데, 본 논문과 같은 연구 방향이 계속해서 발전하면 여러 연구자들의 시행착오 시간을 줄여줄 수 있어서 좋을 것 같다는 생각이 들었음
- 새로운 아이디어를 제안하여 하이퍼파라미터 튜닝의 수고를 덜어주는 내용일 줄 알았는데, 그게 아니라 좋은 teacher model을 만들었더니 모든 student model에 대해서 잘했다는 technical report 형식의 논문이어서 아쉬웠음
- 'No hyper-parameter tuning need'라고 하는데, ImageNet이 아닌 다른 데이터 셋에 적용할 때는 결국 teacher model을 하이퍼파라미터 튜닝을 통해 다시 찾아야하니 본질적인 'No hyper-parameter tuning need'는 아니라는 생각이 들었음

### References

- Ridnik, Tal, et al. "Solving ImageNet: a Unified Scheme for Training any Backbone to Top Results." arXiv preprint arXiv:2204.03475 (2022).
