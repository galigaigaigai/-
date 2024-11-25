타이타닉에서의 생존 확률은?

AX-딥러닝 프로젝트 곽려봉 2017075632
•	1. Introduction
        o	1.1 Load and check data
•	2. Feature Engineering
        o	2.1 What’s in a name?
        o	2.2 Do families sink or swim together?
        o	2.3 Treat a few more variables …
•	3. Missingness
        o	3.1 Sensible value imputation
        o	3.2 Predictive imputation
        o	3.3 Feature Engineering: Round 2
•	4. Prediction
        o	4.1 Split into training & test sets
        o	4.2 Building the model
        o	4.3 Variable importance
        o	4.4 Prediction!
•	5. Conclusion


1.	Introduction
저는 타이타닉 데이터 세트를 사용하기로 결정했고, 그 전에 웹사이트를 둘러보고 영감을 얻기 위해 다른 시나리오들을 살펴보는 데 시간을 보냈습니다. 저는 또한 길을 따라 몇 가지 설명적인 데이터를 시각화하는 데 집중할 것입니다. 그런 다음 무작위 숲을 ，사용하여 타이타닉의 생존을 예측하는 모델을 만들었습니다.
