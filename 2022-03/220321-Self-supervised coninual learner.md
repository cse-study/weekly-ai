+++

title = "Self-supervised continual learners"
date = "2022-03-21"
[profile]  
	enable = true  
	avatar = "/assets/img/yuho.jpg"  
	name = "Yuho Jeong"  
	github = "yuhodots"
	email = "yuho8437@unist.ac.kr"

+++

최근 1년간 진행된 continual learning 연구 중에서 self-supervised approach를 사용한 논문들에 대해서 간단히 정리합니다.
<!--more-->

- **"Co2l: Contrastive continual learning." ICCV 2021**
  - Asymmetric SupCon loss로 새로운 지식을 학습(novel learning)하고, self-supervised instance-wise relation distill(IRD)로 과거의 지식을 보존(prevent forgetting)
  - Asymmetric SupCon: contrastive learning에 current task examples와 memory buffer examples를 둘 다 사용하지만, anchor로는 current task examples만 사용. 이렇게 하면 단순히 contrastive learning 하는 것 보다 효과 좋음
  - IRD: reference(previous) model output과 동일해지도록 현재 모델 regulate (2N개 examples에 대해 전부)
- **"How Well Does Self-Supervised Pre-Training Perform with Streaming ImageNet?." NeruIPS 2021**
  - Self-supervised learning 방식으로 pre-training하면, streaming data에 대해서 joint training(non-streaming) 만큼의 성능이 나온다는 것을 주장
  - Pre-training은 MoCo-v2 protocol을 따르고, OpenSelfSup 라는 prior works의 구현을 기반으로 하였음
  - Streaming data의 distribution shift가 조금인 경우에는 joint training과 self-supervised pre-training의 성능이 거의 비슷하고, large distribution shift인 경우에는 MAS(memory aware synapse)와 data replay 방법을 사용하면 비슷해짐
- **"Rethinking the Representational Continuity: Towards Unsupervised Continual Learning." ICLR 2022**
  - Label unannotated인 unsupervised continual learning(CURL)을 SimSiam과 Barlow Twining라는 prior works 알고리즘 사용하여 해결해보았더니 신기하게도 supervised continual learning보다 catastrophic forgetting에 강건함
  - Lifelong Unsupervised Mixup(LUMP)는 previous task(in memory buffer)와 current task 사이의 interpolate를 활용하는 방법이며, LUMP를 안 써도 잘하지만 LUMP를 사용하면 더 잘함
  - Unsupervised continual learning과 supervised continual learning이 low layer에서는 similar하고 high layer에서는 dissimilar함. Unsupervised continual learning의 loss landscape이 더 smooth 함
  - Test 단계에서 classifying은 KNN을 사용한다고 하는데, 어떻게 사용한건지 아직 제대로 살펴보진 않았음

### Comments

- Self-supervised learning이 좋은 representation을 학습한다는 점, 그리고 새로운 지식을 추가적으로 배우는 경우 중에서 특히 해당 데이터의 양이 적을 때 더 효과적이라는 것이 이미 실험적으로 알려져 있었음. 이 장점은 continual learning이 풀고자 하는 문제와 일치하므로 self-supervised learning 방식이 continual learning task에서 효과적일 것이라는 점은 어느정도 예상된 일이었음
- 따라서 매우 많은 연구자들이 동시에 해당 문제를 거의 비슷한 방식으로 접근했다는 것이 인상적임

### References

- [Cha, Hyuntak, Jaeho Lee, and Jinwoo Shin. "Co2l: Contrastive continual learning." ICCV 2021.](https://openaccess.thecvf.com/content/ICCV2021/html/Cha_Co2L_Contrastive_Continual_Learning_ICCV_2021_paper.html)
- [Hu, Dapeng, et al. "How Well Does Self-Supervised Pre-Training Perform with Streaming ImageNet?." NeruIPS 2021.](https://openreview.net/pdf?id=gYgMSlZznS)
- [Madaan, Divyam, et al. "Rethinking the Representational Continuity: Towards Unsupervised Continual Learning." ICLR 2022.](https://openreview.net/pdf?id=9Hrka5PA7LW)
