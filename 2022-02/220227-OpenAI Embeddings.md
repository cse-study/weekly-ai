+++

title = "OpenAI Embeddings API"
date = "2022-02-27"
[profile]  
	enable = true  
	avatar = "/assets/img/yuho.jpg"  
	name = "Yuho Jeong"  
	github = "yuhodots"
	email = "yuho8437@unist.ac.kr"

+++

2022년 1월에 OpenAI에서 발표한 "Text and Code Embeddings by Contrastive Pre-Training" 논문의 관련 자료들을 읽고 내용을 공유합니다.
<!--more-->

### Summary

- OpenAI에서 GPT-3의 text (or code) embedding 결과를 쉽게 얻을 수 있도록 돕는 Embeddings API라는 툴을 공개함

- 입력 text(or code)와 엔진 이름을 입력하면, 해당 입력의 vector representation(embedding)을 얻을 수 있음

  ```python
  import openai
  response = openai.Embedding.create(
      input="canine companions say",
      engine="text-similarity-davinci-001")
  ```

- 관련하여 3가지 대표적인 use-cases(: Text Similarity, Text Search, Code Search)를 제공함.
- 편의를 위해 `delicious beans`과 같이 N개의 단어 조합으로 이루어진 Embeddings API 입력 text를 '쿼리'라고 칭하겠음. Text similarity는 두 개의 쿼리에 대해 API를 사용하여 유사도를 구하는 작업이고, Text Search는 주어진 쿼리에 대해 가장 유사도가 높은 도큐먼트를 데이터 셋 내에서 찾아내는 (쿼리와 도큐먼트 사이의 유사도를 구하는) 작업이고, Code Search는 주어진 쿼리에 대해 가장 유사도가 높은 함수(혹은 코드)를 데이터 셋 내에서 찾아내는 작업이라고 생각하면 됨.
- [링크](https://medium.com/@nils_reimers/openai-gpt-3-text-embeddings-really-a-new-state-of-the-art-in-dense-text-embeddings-6571fe3ec9d9)에 따르면, Embeddings API는 논문에서 말하는 것 처럼 성능이 현재 다른 모델들 대비 그렇게 좋은 것은 아니고, 모델과 feature dimension이 매우 커서 cost가 너무 높고, 토큰당 가격도 너무나 비싸다고 말하고 있음. (Davinci 모델의 경우 12288 dimensions을 사용하고 토큰당 0.6달러이기 때문에, 일반 유저가 사용하는 것은 거의 불가능하지 싶음)

### References

- OpenAI Blogs, ["Introducing Text and Code Embeddings in the OpenAI API".](https://openai.com/blog/introducing-text-and-code-embeddings/)
- Yannic Kilcher YouTube, ["OpenAI Embeddings (and Controversy?!)".](https://www.youtube.com/watch?v=5skIqoO3ku0)
- OpenAI Embeddings API: https://beta.openai.com/docs/guides/embeddings
- Nils Reimers, ["OpenAI GPT-3 Text Embeddings - Really a new state-of-the-art in dense text embeddings?"](https://medium.com/@nils_reimers/openai-gpt-3-text-embeddings-really-a-new-state-of-the-art-in-dense-text-embeddings-6571fe3ec9d9)
