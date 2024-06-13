![image](https://github.com/Jinwonie/temp_forecast/assets/155731578/ddb9f9f7-1080-4579-9952-04cea02d2d41)# 부산 평균기온 예측

## :alarm_clock: 개발 기간: 2024년 3월 27일 ~ 2024년 4월 12일
## 개발환경:
|IDE|프로그래밍<br/>언어|
|------|---|
|![Coalb](https://img.shields.io/badge/Colab-F9AB00?style=for-the-badge&logo=googlecolab&color=525252)|![PYTHON](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)|

## :people_holding_hands: 멤버구성 및 역할
[조장]

천진원(AUTO-ARIMA(S-ARIMA, ARIMA) 모델링)

[조원]

김현주(CNN-LSTM 모델링), 심재은(DNN, RNN, LSTM 모델링), 이승후

* EDA, Preprocessing은 조원 모두가 함께 진행

## :bulb: 기획 선정 및 배경
현재 지구온난화는 지구온난화를 넘어 지구열대화라는 새로운 용어로 사용해야한다고 논의되는 만큼 그 심각성이 매우 커진 상황입니다.

다가오는 기후변화를 예측하지 못한다면 우리 인류는 지구온난화의 각종 위협에 제대로 대처하지 못하고 결국 인류 멸망이라는 최악의 시나리오에 직면하게 될 것입니다.

그러므로 미래의 기후를 예측하고 다가오는 기후변화에 대응하는 것은 매우 중요한 과정입니다. 따라서 본 프로젝트를 통해 각종 기후지표를 통한 다변량 시계열 예측을 통해 미래 기온을 예측하는 모델을 구축하여 기후변화에 대응하고자 합니다.

## :robot: 모델 개발
> ### EDA
1. 컬럼 정보 확인

|컬럼명|
|------|
|날짜|
|지점|
|평균기온(℃)|
|최저기온(℃)|
|최고기온(℃)|
|평균습도(%rh)|
|강수량(mm)|
|일조합(hr)|
|일조율(%)|
|일사합(MJ/m2)|
|평균풍속(m/s)|

* 최초 데이터는 최고기온(℃)까지로, 평균습도 ~ 평균풍속까지는 모델 예측에 필요한 기후 변수를 추가한 것임

1. 피쳐 간 상관관계 분석<br/>
![image](https://github.com/Jinwonie/temp_forecast/assets/155731578/104814c8-4c75-4eae-aebb-c574e07d000e)

2. 이상치 확인<br/>
![image](https://github.com/Jinwonie/temp_forecast/assets/155731578/64c2279a-e2d9-460a-97dc-a0cfa95945ea)

* 강수량에서 많은 이상치 탐지, 그러나 한국 기후 특성상 여름철 장마로 인해 발생한 것으로, 이는 계절 특성에 의한 것이므로 이상치라고 판단하지 않았음

3. 날짜별 시각화<br/>
- 날짜별 평균기온
![image](https://github.com/Jinwonie/temp_forecast/assets/155731578/015e792a-6e2f-436a-9917-0e9d88669964)

- 날짜별 평균습도
![image](https://github.com/Jinwonie/temp_forecast/assets/155731578/60f3974e-0e8c-433a-bed0-da7e2d12bc27)

- 날짜별 평균강수량
![image](https://github.com/Jinwonie/temp_forecast/assets/155731578/aef82e70-fcf9-4e07-aac0-7f7d52194339)

- 날짜별 평균풍속
![image](https://github.com/Jinwonie/temp_forecast/assets/155731578/37c595e0-1b76-4221-a677-b128c10d0fd2)

> ### Preprocessing
1. 불필요한 컬럼 제거(지점, 일조합(hr), 일조율(%))

> ### Modeling
1. 

