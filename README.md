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
   
![image](https://github.com/user-attachments/assets/e812fe11-172a-44ed-8dbf-41ac4b710fe7)


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
이제 누락된 데이터를 탐색하고 귀책을 통해 수정할 준비가 되었습니다. 이 작업을 수행하는 데는 여러 가지 방법이 있습니다. 데이터 세트의 크기가 작기 때문에 전체 관측값(행)이나 누락된 값이 포함된 변수(열) 중 하나를 삭제하는 것을 선택해서는 안 됩니다. 데이터의 분포(예: 평균, 중앙값 또는 모드)를 고려할 때 누락된 값을 합리적인 값으로 대체할 수 있는 옵션이 남아 있습니다. 마지막으로 예측을 수행할 수 있습니다. 후자의 두 가지 방법을 모두 사용할 것이며, 결정을 유도하기 위해 몇 가지 데이터 시각화에 의존할 것입니다.
    3.1 Sensible value imputation
![image](https://github.com/user-attachments/assets/64fa4380-f552-4580-8a64-4e25e8566d9d)

![image](https://github.com/user-attachments/assets/2ac691cf-477e-432a-b859-f5a5e45e1258)

![image](https://github.com/user-attachments/assets/7186f464-6a81-445a-980f-d609a1a84868)

우리는 이러한 데이터를 기반으로 시작할 수 있는 프레젠테이션 데이터를 추론할 수 있는 현재의 데이터를 추론할 수 있습니다.우리는 그들이 각각 80달러를 지불했고, NNA를 각각 1과 NA. 그래서 그들이 출발했던 곳부터 시작했나요?

![image](https://github.com/user-attachments/assets/b0295916-6195-42c8-91d9-094b94152b94)

![image](https://github.com/user-attachments/assets/da0f9a14-cc7a-4dfe-a9c0-1c3e1416e411)

이 시각화로 볼 때 NA 티켓 가치를 그들의 선복과 출발 중앙값인 8.05달러로 대체하는 것이 상당히 합리적으로 보입니다.

![image](https://github.com/user-attachments/assets/8283b36c-3977-4fda-b375-758ac3dc9aa6)


    3.2 Predictive imputation
  
  마지막으로, 앞서 언급했듯이 우리의 데이터에는 상당한 연령 값이 누락되어 있습니다. 우리는 누락된 연령 값을 더 선호할 것입니다. 왜냐 하면 우리는 할 수 있기 때문입니다. 우리는 다른 변수를 기반으로 나이를 예측하는 모형을 만들 것입니다.

   ![image](https://github.com/user-attachments/assets/1de35716-e30a-499e-94d0-a8e02d97d451)

   ![image](https://github.com/user-attachments/assets/e092c8fa-8d14-4030-9bc4-dfb96cc72280)

   rpart(회귀적 재귀 파티션)를 사용하여 누락된 연령을 예측할 수 있지만 다른 것을 위해 이 작업을 수행하기 위해 mice 패키지를 사용할 것입니다. 여기서 연쇄 방정식을 사용하는 다중귀인에 대한 더 많은 정보를 읽을 수 있습니다(PDF). 아직 그렇게 하지 않았기 때문에 먼저 요인 변수를 분해한 다음 마우스 귀인을 수행할 것입니다.

 ![image](https://github.com/user-attachments/assets/f5a78827-3d03-45d0-b869-f4b88b157918)

![image](https://github.com/user-attachments/assets/e35e2d82-6bb6-43dc-92f6-be1a7af45df9)

![image](https://github.com/user-attachments/assets/490883df-ef82-4a14-90d4-040c768f79af)

우리가 얻은 결과를 승객 연령의 원래 분포와 비교하여 오류가 완전히 없는지 확인합니다.

![image](https://github.com/user-attachments/assets/f3a675c1-f7d5-4a92-b234-4715605f998c)

![image](https://github.com/user-attachments/assets/b949c351-5d92-4af4-9f69-433eb70cd8ec)

상황이 좋아 보이니 원래 데이터의 연령 벡터를 마우스 모델의 출력으로 대체해 보겠습니다.

![image](https://github.com/user-attachments/assets/833dec0c-d2f4-4ca7-ab1e-4540530c3c14)

![image](https://github.com/user-attachments/assets/7c2c894d-cd0b-482b-aa86-dab03e6b2056)

현재 관심 있는 모든 변수에 대한 값을 입력하는 작업을 완료했습니다! 이제 완전한 연령 변수가 있으므로 몇 가지 마무리 작업만 하면 됩니다. 연령을 사용하여 조금 더 많은 기능 엔지니어링을 수행할 수 있습니다....

    3.3 Feature Engineering: Round 2
    이제 모든 사람의 나이를 알았으니 두 가지 새로운 연령 종속 변수를 만들 수 있습니다: 자녀와 어머니. 자녀는 단순히 18세 미만의 사람이 되고 어머니는 1) 여성, 2) 18세 이상, 3) 자녀가 0명 이상(농담이 아닙니다!), 4) '아가씨'라는 제목이 없습니다.

   ![image](https://github.com/user-attachments/assets/ff7c5167-b4f1-4af4-9176-16115ee96e64)

![image](https://github.com/user-attachments/assets/16f2ece4-6339-4878-8793-01e637233c5e)

![image](https://github.com/user-attachments/assets/558a418a-2f47-4c0b-846a-eeec34673523)

![image](https://github.com/user-attachments/assets/a5e423fb-8fd5-42a2-864e-b9d42d755b23)

아이가 되는 것이 아프지는 않지만 반드시 여러분을 구할 수 있는 것도 아닙니다! 어머니 변수를 생성하여 피처 엔지니어링을 마무리하겠습니다. 어쩌면 어머니들이 타이타닉 호에서 살아남았을 가능성이 더 높기를 바랄 수도 있습니다.

![image](https://github.com/user-attachments/assets/ff995da3-e295-4a75-b995-be803da62bc5)

![image](https://github.com/user-attachments/assets/e730229e-9322-4f73-b38b-7e81f78e5d2f)

![image](https://github.com/user-attachments/assets/9a09ccd4-ad6f-45d4-aad2-da0ee3b316fe)


우리가 관심을 갖는 모든 변수를 처리해야 하며 누락된 데이터가 없어야 합니다. 확인을 위해 다시 한 번 확인하겠습니다:

![image](https://github.com/user-attachments/assets/5386195d-a8b8-4690-bf3f-716441df1896)

![image](https://github.com/user-attachments/assets/b22dc0bf-ca08-44ee-89f1-9d640f15b7dc)

![image](https://github.com/user-attachments/assets/60ff2485-8556-4fd8-8e08-7017c8abe9cb)

와우! 마침내 쥐에 대한 멋진 대입을 포함한 타이타닉 데이터 세트의 모든 관련 누락 값 처리를 완료했습니다. 또한 생존을 안정적으로 예측하는 모델을 구축하는 데 도움이 될 몇 가지 새로운 변수를 성공적으로 만들었습니다.
# 4. Prediction
마침내 우리는 누락된 값을 신중하게 선별하고 처리한 변수를 바탕으로 타이타닉 호 승객 중 누가 살아남을지 예측할 준비가 되었습니다. 이를 위해 우리는 무작위 숲 분류 알고리즘에 의존할 것이며, 결국 모든 시간을 귀책에 할애했습니다.
    4.1 Split into training & test sets
    첫 번째 단계는 데이터를 원래의 테스트 및 훈련 세트로 다시 분할하는 것입니다.

   ![image](https://github.com/user-attachments/assets/884c7f56-70cd-40e1-8def-acc57c0f0d7c)

    4.2 Building the model
    그런 다음 훈련 세트에서 랜덤 포레스트를 사용하여 모델을 구축합니다.

   ![image](https://github.com/user-attachments/assets/bf7abad6-d39a-4d61-96d7-4f0febc58792)

![image](https://github.com/user-attachments/assets/3d9963ec-722c-462c-b2c4-146181c611b4)

검은색 선은 20% 미만으로 떨어지는 전체 오류율을 보여줍니다. 빨간색과 녹색 선은 각각 '죽은'과 '생존한'의 오류율을 보여줍니다. 지금 우리는 생존보다 훨씬 더 성공적으로 죽음을 예측하고 있다는 것을 알 수 있습니다. 그게 저에 대해 무엇을 의미할까요?
    4.3 Variable importance
모든 트리에서 계산된 지니의 평균 감소를 플롯하여 상대적 변수 중요도를 살펴봅니다.

![image](https://github.com/user-attachments/assets/f8ec1863-b662-4a75-8d3e-8de0dab5afe4)

![image](https://github.com/user-attachments/assets/5a247adc-6293-4165-8979-c107a4a21581)

와우, 제목 변수를 만들어서 다행입니다! 모든 예측 변수 중 상대적으로 가장 높은 중요도를 가지고 있습니다. 승객 등급이 5위로 떨어진 것을 보고 가장 놀랐지만, 아마도 어렸을 때 영화 타이타닉을 너무 많이 본 것에서 비롯된 편견일 수도 있습니다.
    
    4.4 Prediction!

    우리는 예측을 하는 마지막 단계를 준비했습니다! 여기서 끝나면 이전 단계를 반복하여 다른 모델을 사용하여 데이터를 조정하거나 다른 변수 조합을 사용하여 더 나은 예측을 달성할 수 있습니다. 하지만 지금은 저에게 좋은 출발점이자 중단점입니다.

   ![image](https://github.com/user-attachments/assets/2bcea8ae-3552-4df5-8755-4e7f5e2ca192)

# 5. Conclusion
감사합니다!
