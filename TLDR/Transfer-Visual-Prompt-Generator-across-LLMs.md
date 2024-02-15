# [TLDR] VPGTrans: Transfer Visual Prompt Generator across LLMs 

# Abstract
- 텍스트 이미지 쌍을 학습시켜서 멀티모달 모델 훈련시키는건 공수 많이 드는 작업임
- 기존 LLM을 비교적 가벼운 visual prompt generator (VPG)와 연결하려고 했는데, 여전히 리소스 많이 필요
- VPG를 작은 MLLM에서 학습 후 큰 MLLM으로 옮기면 어떨까?
    - 실험을 통해 VPG transfer의 성능 테스트함


![Figure1](https://github.com/jaealways/must-read-paper-CV-daily/assets/71856506/ee4aeacc-8e30-4c4b-8c31-181f6817a87d)


## multimodal LLMs (MLLMs)
### visual prompt generator (VPG)
- visual content 생성하기 위해 사용자의 입력 프롬프트를 DALL-E와 같은 AI 기반 이미지 생성 모델에 지시
- VPG: 특정 프롬프트에 기반해서 이미지 생성
- Projector: 텍스트 이미지 임베딩을 저차원으로 매핑, LLM이 이해할 수 있게 이미지를 변환
- LLM: 입력을 바탕으로 시각 정보에 대한 답변함

## Results and Findings
- LLM 사이즈나 타입 간 VPG를 옮겼을 때 GPU 시간과 필요한 training data 수 감소시킴

# Maximizing the Transfer Efficiency with a Two-stage Transfer Strategy
##  Key Factors for VPG Transfer
- warm-up: 학습속도 또는 하이퍼파라미터를 일정 단계에 걸쳐 점진적으로 조정하는 단계?
- 학습된 VPG를 사용해서 학습을 가속화하기
- linear projector warm-up하면 좋다?
- 단어 변환기를 통해 LLMtgt의 프로젝터를 초기화하면 linear projector warm-up 가속화할 수 있음
- Linear project의 warm-up은 학습률을 높여 빠르게 수렴하게 함

## A Two-stage VPG Transfer Framework
![Figure5](https://github.com/jaealways/must-read-paper-CV-daily/assets/71856506/5224cbd8-d498-4570-9f69-1f73aa5080a6)
- Stage-1: (a) inherit the VPG of LLMsrc (b) initialize the projector by merging the projector of LLMsrc and word converter. (c) Then the projector will be warmed up for 1 epoch with a large learning rate.
- Stage-2: (d) conduct a vanilla fine-tuning for the VPG and projector for n epochs.

# Conclusion
- 서로 다른 크기와 유형의 LLM 사이에 transfer efficiency를 극대화하기 위한 주요요소 살펴봄
- 비용을 크게 줄이면서 비교 가능하거나 더 나은 성능 달성하는 두 단계 프레임워크 제안
- 기존 MLLM에서 VPG transfer를 통한 practical value 증명



