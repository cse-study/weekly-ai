+++
title = "Whisper: Robust Speech Recognition via Large-Scale Weak Supervision"
date = "2022-09-23"
[profile]  
	enable = true  
	avatar = "/assets/img/yuho.jpg"  
	name = "Yuho Jeong"  
	github = "yuhodots"
	email = "yuho8437@unist.ac.kr"

+++

OpenAI에서 공개한 Speech Recognition 모델 Whisper에 대해서 세 줄 요약 합니다. 

<!--more-->

[[paper](https://cdn.openai.com/papers/whisper.pdf)] [[blog](https://openai.com/blog/whisper/)]

### Whisper

- Web에서 수집된 68만 시간 분량의 multilingual, multitask data를 학습한 automatic speech recognition (ASR) 시스템: 당연하게도 **Encoder-Decoder Transformer** 구조
- Multilingual, multitask data를 학습한 모델이므로, decoder에 주어지는 special token에 따라 '영어 음성을 영어 문서로 작성', '비영어 음성을 영어 문서로 기술', '비영어 음성을 비영어 문서로 기술'등의 다양한 task를 모두 수행할 수 있는 매우 general한 end-to-end 모델임
- Overall process는 논문의 figure로 제공하고 있음: (1) 처음에는 Voice activity를 감지하여 실제로 음성이 존재하는 데이터인지 감지. (2) 실제로 음성이 존재하는 데이터라면, 해당 음성이 어떤 언어인지 인식하는 langauge identification 과정 거침. (3) Special token에 따라 transcription 혹은 to-English translation을 학습하는데 (4) 이 과정에서 timestamp token에 따라 time-aliged transcription 혹은 text-only transcription을 수행하도록 학습
