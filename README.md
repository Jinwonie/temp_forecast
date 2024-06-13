# 부산 평균기온 예측

## :alarm_clock: 개발 기간: 2024년 03월 27일 ~ 2024년 04월 12일
## 개발환경:
|IDE|프로그래밍<br/>언어|
|------|---|
|![Coalb](https://img.shields.io/badge/Colab-F9AB00?style=for-the-badge&logo=googlecolab&color=525252)|![PYTHON](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)|

## :people_holding_hands: 멤버구성 및 역할
천진원(조장)

김민근, 주현수, 허영민

: 전체 과정 함께 진행

## :bulb: 기획 선정 및 배경
한국교육개발원의 고교 졸업자의 대학진학률 현황 분석에 따르면 2021년 기준 한국의 대학 진학률은 등록자 기준 73.7%이고, 각 나이대별 취학률 또한 OECD 평균 보다 높은 수치를 기록하고 있습니다.

그러나 현실적으로는 다양한 요인으로 인해 학업을 중단하는 경우가 있습니다. 한국교육개발원의 학업 중단율 분석에 따르면 2021년 기준 전문대학과 대학을 포함한 학업 중단율은 13%에 달하는 높은 수치를 기록하고 있습니다.

이러한 학업 중단 현상은 개인의 미래를 저해하고 국가 차원의 중요한 고급 인력을 잃는 결과를 초래할 수 있습니다. 따라서 이를 해결하고 예방하기 위해 학업 중단의 원인 분석 및 예측 조기 대응 시스템을 마련하는 것이 필요합니다.

그러므로 저희는 학업 중단의 원인을 다각도로 분석하고, 예측 모델을 설계해 학생들의 학업 중단을 최소화하고, 국가 발전을 위한 고급 인력을 유지할 수 있는 방안을 모색하기 위해 해당 주제를 선정했습니다.

## :robot: 모델 개발
> ### EDA
1. 컬럼 정보 확인

|컬럼명|설명|
|------|----|
|marital|결혼여부|
|application mode|지원방법|
|application order|지망순|
|course|전공|
|attendence|주/야간 수업 참석 여부|
|previous qualification|고등교육전에 학생이 취득한 자격|
|nationality|학생 국적|
|mother qualification|학생 어머니 최종학력|
|father qualification|학생 아버지 최종학력|
|mother occupation|어머니 직업|
|father occupation|아버지 직업|
|displaces|실향민 여부|
|special|특별 교육이 필요 여부|
|debtor|채무자 여부|
|fees up to date|최근 수업료 수납 여부|
|gender|성별|
|scholarship|장학생 여부|
|enrollment age|입학 나이|
|international|국제학생 여부|
|1st credited|첫 학기에 이수한 교과목 단위|
|1st enrolled|첫 학기에 등록한 교과목 단위|
|1st evaluations|첫 학기에 평가가 있는 교과목 단위|
|1st approved|첫 학기에 승인한 교과목 단위|
|1st grade|첫 학기 등급|
|1st without evaluations|첫 학기 평가가 없는 교과목 단위|
|unemploymen|실업률|
|inflation rate|인플레이션율|
|gdp|gdp|
* 2학기 credited, enrolled, evaluations, approved, grade, without evaluations도 존재함

2. 타겟 불균형 확인(6:4 정도로 불균형 존재)
![image](https://github.com/Jinwonie/dropout_prediction_model/assets/155731578/c9139a3c-b7fb-497f-8544-e77a604c7f40)

3. 피쳐 간 상관관계 분석((abs)0.65보다 높은 상관관계)<br/>
![image](https://github.com/Jinwonie/dropout_prediction_model/assets/155731578/ead96e81-66a7-46a0-b304-3c15a1ee4e61)

4. 각 feature에 따른 target 비율 측정
- 유학생 신분에 대한 학업 포기 비율
![image](https://github.com/Jinwonie/dropout_prediction_model/assets/155731578/d181450f-aa88-479f-8606-e122bcdef277)

- 장학금 여부에 대한 학업 포기 비율
![image](https://github.com/Jinwonie/dropout_prediction_model/assets/155731578/fbd01432-260a-4c2f-b4da-fb4f022300a5)

- 성별별 학업 포기 비율</br>
![image](https://github.com/Jinwonie/dropout_prediction_model/assets/155731578/162326d7-f2f5-4208-a752-b2c1b47d1413)

- 전공과정별 학업 포기 비율
![image](https://github.com/Jinwonie/dropout_prediction_model/assets/155731578/acddfb11-a902-4c16-b9a8-d6fcb1c1172c)

3. 이상치 탐지에서의 성능 비교 및 전처리 이후 모델의 정확도 측정을 위한 데이터 증강 작업 및 acc, f1 score 측정 함수 생성<br/>
![image](https://github.com/Jinwonie/dropout_prediction_model/assets/155731578/20644785-ab9f-473e-a7c0-d027023df933)


4. 이상치 탐지
- 여러 이상치 탐지 기법을 통해 이상치를 탐지하고 Base Model을 통해 성능 비교<br/>(Base Model = LogisticRegression(solver='liblinear'))

|탐지기법|성능(val_acc)|
|--------|-----|
|Z-score|92.30%|
|IsolationForest|92.80%|
|LOF|88.50%|
|DBSCAN|90.20%|
|IQR|83.20%|

> ### Preprocessing
1. raw_data 기준으로 Model을 돌리고 가장 성능이 좋은 모델을 Bese Model로 선정, 전처리 전후 성능을 비교

Best Model: LogisticRegression(acc: 90.60%, f1: 87.35%)

2. 도메인 지식, EDA, Featrue Importance를 활용하여 버전 별로 데이터를 관리하며 전처리를 실시하여 모델 성능 향상을 측정함.

ver 1. 성적 파생변수 추가 + credited 컬럼 제거

- 성적과 관련된 파생변수끼리 상관관계가 있고, Target과도 높은 상관관계가 있으므로 파생변수를 생성함.
   
   - 2nd grade - 1st grade: 성적 등락(grade increse)
   
   - 1st grade * 1st approved: 총 학점 획득량(1st / 2nd weighted grade)
  
   - 2st grade * 2st approved

ver 2.

- weigthed grade를 반대로 나누어서 비슷한 효과지만 격차를 줄여보면 어떨지 실험(이유: 대부분 카테고리컬 데이터로 이루어져 있어 곱셈의 경우 데이터 간 큰 수치 차이로 인해 성능이 떨어질 것을 우려)

- 실험 결과 ver 1의 성능이 더 좋았으므로 ver 1에 추가 전처리 진행

ver 3.
- EDA를 통해 각 변수들을 분석하면서 변수 제거

  - Marital은 Dropout, Graduate의 비율이 동등했고 유의미한 데이터는 데이터 수 자체가 매우 적었으므로 모델 성능에 영향을 미치지 못할 것으로 예상, 제거 결정

  - GDP, Inflation rate, Unemployment는 비슷한 feature로, 모델의 복잡도를 높여 예측 성능에 좋지 않은 영향을 줄 것으로 예상하여 feature importance가 가장 높은 Unemployment 제외 나머지 feature 제거(feature importance는 DT, RF, XGB, LGBM에서 확인)

  - without evaluation은 평가가 없는 점수로, grade에도 직접적인 연관이 없고 feature importance에서도 큰 영향력이 없으므로 제거

ver 4, 5에서는 feature importance를 보면서 제거 이후 성능이 이전에 비해 낮아질 때까지 진행함

- ver 4: attendance 제거 ver 5: international 제거

ver 6. 이상치 제거와 Standard Sclaer로 스케일링 진행

- 이상치 제거 전후 비교

![image](https://github.com/Jinwonie/dropout_prediction_model/assets/155731578/d2cca084-259c-4fa2-9dc3-172784e477fd)

IsolationForest가 성능 향상에 유의미했음

- 스케일링 전후 비교<br/>
![image](https://github.com/Jinwonie/dropout_prediction_model/assets/155731578/40746469-7ac2-404b-a02a-e98b8433a3cd)

![image](https://github.com/Jinwonie/dropout_prediction_model/assets/155731578/1c086c05-22cb-4068-8ac9-e30ef5f0d138)

스케일링이 성능 향상에 유의미했음.

> ### Modeling & Model ensemble(ver 6. 기준)
1. 하이퍼파라미터 튜닝 전 모델 비교 및 모델 선정<br/>
![image](https://github.com/Jinwonie/dropout_prediction_model/assets/155731578/35bcec37-4144-48b7-beea-496966a35c99)<br/>
![image](https://github.com/Jinwonie/dropout_prediction_model/assets/155731578/61f609ee-1b16-46c1-8573-fef4ae3b37e6)<br/>
- Voting = LGBM, GB, RF, ADAboost

- 성능 측정 결과 RF, GB, LGBM, ADA, Voting이 성능이 좋았음

2. 하이퍼파라미터 최적화 후 최종 성능 비교(Grid Search CV)<br/>
![image](https://github.com/Jinwonie/dropout_prediction_model/assets/155731578/78b91b9c-8293-4653-bcf7-22fc790492c1)<br/>
![image](https://github.com/Jinwonie/dropout_prediction_model/assets/155731578/54e16982-e4c2-45ff-ae2f-92107caa99bf)<br/>

- 최종 성능 측정 결과 LGBM이 acc 90.97, f1 84.12로 가장 좋은 성능을 보였고, 최종 모델로 선정됨

