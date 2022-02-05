+++

title = "AlphaCode"
date = "2022-02-05"
[profile]  
	enable = true  
	avatar = "/assets/img/yuho.jpg"  
	name = "Yuho Jeong"  
	github = "yuhodots"
	email = "yuho8437@unist.ac.kr"

+++

2022년 2월에 딥마인드에서 발표한 **AlphaCode** 블로그 포스팅을 읽고 내용을 공유합니다. 
<!--more-->

### Summary

- AlphaCode란?: competitive programming task를 human-level로 풀 수 있는 시스템. Codeforces의 10개 대회에 대해 테스트 했을 때, 참가자들의 평균 수준의 성능 달성 (상위 54%)
- Model: Transformer-based langauge model 이라고 포스팅에 언급되어 있음. Language generation(code generation)이 주요 역할인 것으로 보아 decoder-centric langauge model 중 하나를 사용했을 것으로 생각됨. 그 뒤에 promising program으로 결과를 필터링했다고 하는데, rule-based로 결과를 필터링 했다는 의미로 대충 이해했음 (promising program의 정확한 의미를 아는 분 있으면 코멘트 부탁드립니다)
- Training: Github code로 pre-training하고, competitive programming task에 대해 fine-tuning 진행하였음 (일반적인 language model 학습하는 방식과 동일하게)

### Comments

- Attention 기반 시각화가 너무 아름다움🥺 기회가 되면 나중에 한번 만들어보고 싶음
- 포스팅 원문에서 방법론 추가에 따른 모델의 발전과정을 볼 수 있음

### References

- Alphacode 블로그 포스팅: [Competitive programming with AlphaCode](https://deepmind.com/blog/article/Competitive-programming-with-AlphaCode)
- Alphacode 시각화: [AlphaCode Attention Visualization](https://alphacode.deepmind.com/)
- Alphacode paper: https://storage.googleapis.com/deepmind-media/AlphaCode/competition_level_code_generation_with_alphacode.pdf
- Alphacode dataset: https://github.com/deepmind/code_contests
