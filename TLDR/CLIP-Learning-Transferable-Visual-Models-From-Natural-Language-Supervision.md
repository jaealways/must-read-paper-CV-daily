# [TLDR] CLIP: Learning Transferable Visual Models From Natural Language Supervision 

- 기존 SOTA CV는 이미 지정된 object를 맞추도록 훈련됨
- 만약 이미지와 관련된 raw text를 통해 대량의 학습을 하면 determined되지 않은 object도 맞출 수 있지 않을까? -> 웹에 있는 metadata label을 사용해보자
- downstream task를 해결하기 위한 zero-shot transfering이 가능하지 않을까?
- 인터넷에서 공개된 대량의 데이터를 사용해서 (이미지,텍스트) 쌍 훈련
- CLIP은 GPT 계열로, OCR, action recognition 등 태스크 수행하는 방법 배움을 깨달음


![image](https://github.com/jaealways/must-read-paper-CV-daily/assets/71856506/f329bf1d-c8ed-49d6-8eb1-0359b72cb818)


## Approach
- NLP에서 deep contextual represenation이 가능해지면서, abundant source를 사용할 수 있어짐
- representation을 단순히 학습하는게 아니라 zero-shot transfer를 가능하게 함
- 인터넷에 널리 있는 4억개의 (자연어, 이미지) 데이터 쌍을 활용해서 학습시킴
- 위의 그림처럼 N*N의 Text, Image 쌍에서 서로 매치하는 N쌍은 가깝게, 먼 $N^2-N$쌍은 멀어지게 contrasive learning 진행해서 cross-entropy loss 최소화하려 함
- 5개의 ResNet과 3개의 Vision Transformer를 훈련시킴.

- 가령 image classification 한다면, 이미지를 Image Encoder에 보내고, 이미지 벡터 뽑아냄
- classifier에 지정된 class text encoder로 텍스트 벡터 뽑음
- 둘 dot product해서 가장 큰 값으로 분류함
- prompt engineering: a photo of {label} 등으로 문장형으로 바꿔주는 것
    - Polysemy 다의성 이슈 (가령 crane은 크레인과 학 둘다 가능)
    - 좀 더 label에 대한 context information 줄 수 있는 형태로 바꿔주기
    - 성능 향상됨

## Conclusion
- NLP에서 사용하던 transfer를 CV도메인에서도 사용할 수 있을까?
- CLIP은 다양한 작업을 수행할 수 있는 pretraining을 학습하고, 프롬프트를 통해 zero-shot transfer 가능하게 함

