# NaverMovieSentiment

네이버 영화 감성 분석

## 1. Point  

우리 팀의 포인트는 크게 2가지 입니다. 

첫째로는 네이버 영화 감성 분석 또는 인터넷 상에 있는 데이터의 감성 분석을 위해서는 구어체 데이터를 바탕으로한 Pretrain 모델(XLnet,BERT)가 필요하다고 생각했습니다.
그래서 국립 국어원에 있는 메신저 말뭉치, 구어 말뭉치를 전처리해서 Pretrain 작업에 있습니다. (학습 중인 관계로, 아직 비공개)

두번째로는, 분류기의 성능 개선입니다. Adversarial training의 개념을 활용했습니다.

![Adversarial Training](https://miro.medium.com/max/1000/1*WSqDW1hE8b9MU2GfQjqlxA.jpeg)

딥러닝의 경우, noise에 취약하다고 합니다. 그래서 위 그림을 보게 되시면 noise를 더하게 되면 pander를 gibbon으로 분류하게 됩니다.
이를 방지하고자 Adversarial training은 원래의 데이터에 '해당 데이터에서 분류를 할 수 없을 정도로 가장 큰 noise'를 더하고, 이를 분류할 수 있도록 파라미터를 학습합니다.
Loss는 기존의 classification loss에 adversarial training loss를 더한 방식입니다.(adversarial training loss는 regularization 의 개념이라고 생각하셔도 됩니다)

이를 통해서 분류 성능이 올라가게 되고, 아래 표에 비교군(LSTM으로 구성된 classifier)와 대조군(LSTM + Adversarial training 개념 적용한 classifier)를 참고하시면 됩니다.

|  | Loss | ACC |   
| ---          | ---          | ---          | ---          
| LSTM | x3 | 0.3938 | 0.8395 |  
| LSTM + adv | # | x3 | # |  

## 2. 향후 방향
XLnet 학습이 완료되면, 해당 XL net으로 감성 분석 데이터의 분류기 학습 과정을 진행할 예정이고, 추가적으로 XLnet에 adversarial training 요소를 추가 시켜서 분류 성능을 더욱 극대화 시킬 예정입니다.
