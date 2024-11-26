# AI-X딥러닝 프로젝트 
타이타닉에서의 생존 확률은?
# Members
실내건축디자인 곽려봉 2017075632 EMAIL:guolifeng917@gmail.com


# CONTENTS
1. Introduction
 1.1 Load and check data

2. Feature Engineering
 2.1 What’s in a name?
 2.2 Do families sink or swim together?
 2.3 Treat a few more variables …

3. Missingness
 3.1 Sensible value imputation
 3.2 Predictive imputation
 3.3 Feature Engineering: Round 2

4. Prediction
    4.1 Split into training & test sets
    4.2 Building the model
    4.3 Variable importance
    4.4 Prediction!

5. Conclusion


# 1. Introduction
저는 타이타닉 데이터 세트를 사용하기로 결정했고, 그 전에 웹사이트를 둘러보고 영감을 얻기 위해 다른 시나리오들을 살펴보는 데 시간을 보냈습니다. 저는 또한 길을 따라 몇 가지 설명적인 데이터를 시각화하는 데 집중할 것입니다. 그런 다음 무작위 숲을 ，사용하여 타이타닉의 생존을 예측하는 모델을 만들었습니다.

# 1.1 Load and check data
![1732591662746](https://github.com/user-attachments/assets/4d8b04e9-7185-414c-a4fa-642984207c61)

Now that our packages are loaded, let’s read in and take a peek at the data.

![image](https://github.com/user-attachments/assets/0a2e2df0-dae3-4bff-8884-4b115756f6c9)

![image](https://github.com/user-attachments/assets/7161c2e6-d0ef-4633-8eca-27f47ae36ee0)


그들은 우리의 변수, 유형 및 각 변수의 처음 몇 가지 관찰에 대해 이해했습니다. 우리는 12개의 변수에 대해 1309개의 관찰을 수행하고 있다는 것을 알고 있습니다. 일부 변수 이름은 100% 계발적이지 않기 때문에 다음과 같이 우리가 처리해야 하는 일이 더 명확해집니다.

![image](https://github.com/user-attachments/assets/b02d686c-726a-410c-a372-ad0301557fb6)


# 2. Feature Engineering
    
 # 2.1 What’s in a name?
나의 관심을 끌었던 첫 번째 변수는 passenger name이었는데, 예측에 사용하거나 다른 새로운 변수를 만드는 데 사용할 수 있는 다른 의미 있는 변수로 분해할 수 있었기 때문입니다. 예를 들어 승객 이름이 승객 이름 변수에 포함되어 있으면 성을 사용하여 가족을 나타낼 수 있습니다. 기능공학을 좀 합시다!

![image](https://github.com/user-attachments/assets/0ac09e81-9ddb-41fd-9b0a-1e979c578520)

![image](https://github.com/user-attachments/assets/a43739d8-5224-47b7-b165-325a9a9c74d1)

![image](https://github.com/user-attachments/assets/405dbba8-e4a2-4c6c-a3a3-013980b29726)

![image](https://github.com/user-attachments/assets/482933ea-a59c-443d-a5bf-392ffbb1b941)

![image](https://github.com/user-attachments/assets/5b20e162-3236-4a34-a315-1582d1fc403b)

![image](https://github.com/user-attachments/assets/86a9e1c9-4872-4b6e-be31-a26bcc79824c)

우리는 875개의 고유한 성을 가지고 있습니다. 성을 바탕으로 민족성을 추론하고 싶습니다.
    
    2.2 Do families sink or swim together?

이제 승객 이름을 몇 가지 새로운 변수로 분할하는 작업을 처리했으니 한 걸음 더 나아가 몇 가지 새로운 가족 변수를 만들 수 있습니다. 먼저 형제/배우자 수(배우자가 두 명 이상일 수도 있나요?)와 자녀/부모 수를 기준으로 가족 크기 변수를 만들겠습니다.
   
    ![image](https://github.com/user-attachments/assets/2c466179-0b35-4da5-8ead-b2d1b365b709)

가족 크기 변수는 어떻게 생겼나요? 생존과 어떤 관련이 있는지 이해하는 데 도움이 되도록 훈련 데이터에 표시해 보겠습니다.

![image](https://github.com/user-attachments/assets/7333f873-90ec-42ca-be42-f5d306909574)

![image](https://github.com/user-attachments/assets/3a7abbf6-5296-44a6-8d99-039e836510c2)

아하하. 독신자와 가족 규모가 4세 이상인 사람들에게는 생존 처벌이 있다는 것을 알 수 있습니다. 이 변수를 세 가지 수준으로 분해할 수 있는데, 이는 대가족 수가 상대적으로 적기 때문에 도움이 될 것입니다. 이산화된 가족 규모 변수를 생성해 보겠습니다.

![image](https://github.com/user-attachments/assets/c0f03ae0-e6f6-4245-bd34-cac352f1bd62)

![image](https://github.com/user-attachments/assets/8e51aca7-3762-45be-87df-21c84139eb97)

모자이크 플롯은 독신자와 대가족에게는 생존 처벌이 있지만 소가족 승객에게는 혜택이 있다는 규칙을 유지한다는 것을 보여줍니다. 연령 변수로 더 많은 일을 하고 싶지만 263개 행에 연령 값이 누락되어 있으므로 실종 문제를 해결할 때까지 기다려야 할 것입니다.

    2.3 Treat a few more variables …

    남은 것은 무엇인가요? 승객실 변수에는 갑판에 대한 정보를 포함하여 잠재적으로 유용한 정보가 있을 것입니다. 살펴보겠습니다.

    ![image](https://github.com/user-attachments/assets/089a1f36-9791-4202-a93a-3434ddb539fc)
    
    ![image](https://github.com/user-attachments/assets/20f5ecc9-db1b-46ac-8960-3add7cf43f9f)

    ![image](https://github.com/user-attachments/assets/689fd797-89e3-4932-b24e-f43b88736002)

    ![image](https://github.com/user-attachments/assets/ebf78517-74b8-442c-8ea4-b32a0fdaa0c8)

    ![image](https://github.com/user-attachments/assets/9fc94009-e030-45e8-bfe8-66f0f7a93d70)

여기에는 여러 개의 방이 나열된 캐빈(예: 28열: "C23 C25 C27")을 살펴보는 것을 포함하여 더 많은 작업을 수행할 수 있지만, 칼럼의 희소성을 고려할 때 여기에서 멈출 것입니다.

# 3. Missingness
    3.1 Sensible value imputation
    3.2 Predictive imputation
    3.3 Feature Engineering: Round 2
# 4. Prediction
    4.1 Split into training & test sets
    4.2 Building the model
    4.3 Variable importance
    4.4 Prediction!
# 5. Conclusion
