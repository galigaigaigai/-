타이타닉에서의 생존 확률은?

AX-딥러닝 프로젝트 곽려봉 2017075632
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


# 1.Introduction
저는 타이타닉 데이터 세트를 사용하기로 결정했고, 그 전에 웹사이트를 둘러보고 영감을 얻기 위해 다른 시나리오들을 살펴보는 데 시간을 보냈습니다. 저는 또한 길을 따라 몇 가지 설명적인 데이터를 시각화하는 데 집중할 것입니다. 그런 다음 무작위 숲을 ，사용하여 타이타닉의 생존을 예측하는 모델을 만들었습니다.
1.1 Load and check data
Load packages
library('ggplot2') # visualization
library('ggthemes') # visualization
library('scales') # visualization
library('dplyr') # data manipulation
library('mice') # imputation
library('randomForest') # classification algorithm
Now that our packages are loaded, let’s read in and take a peek at the data.
train <- read.csv('../input/train.csv', stringsAsFactors = F)
test  <- read.csv('../input/test.csv', stringsAsFactors = F)
	
full  <- bind_rows(train, test) # bind training & test data
	
#check data
str(full)
##'data.frame':    1309 obs. of  12 variables:
##$ PassengerId: int  1 2 3 4 5 6 7 8 9 10 ...
##$ Survived   : int  0 1 1 1 0 0 0 0 1 1 ...
##$ Pclass     : int  3 1 3 1 3 3 1 3 3 2 ...
##$ Name       : chr  "Braund, Mr. Owen Harris" "Cumings, Mrs. John Bradley (Florence Briggs Thayer)" "Heikkinen, Miss. Laina" "Futrelle, Mrs. Jacques Heath (Lily May Peel)" ...
##$ Sex        : chr  "male" "female" "female" "female" ...
##$ Age        : num  22 38 26 35 35 NA 54 2 27 14 ...
##$ SibSp      : int  1 1 0 1 0 0 0 3 0 1 ...
##$ Parch      : int  0 0 0 0 0 0 0 1 2 0 ...
##$ Ticket     : chr  "A/5 21171" "PC 17599" "STON/O2. 3101282" "113803" ...
##$ Fare       : num  7.25 71.28 7.92 53.1 8.05 ...
##$ Cabin      : chr  "" "C85" "" "C123" ...
##$ Embarked   : chr  "S" "C" "S" "S" ...
그들은 우리의 변수, 유형 및 각 변수의 처음 몇 가지 관찰에 대해 이해했습니다. 우리는 12개의 변수에 대해 1309개의 관찰을 수행하고 있다는 것을 알고 있습니다. 일부 변수 이름은 100% 계발적이지 않기 때문에 다음과 같이 우리가 처리해야 하는 일이 더 명확해집니다.
Variable Name	Description
Survived	Survived (1) or died (0)
Pclass	Passenger’s class
Name	Passenger’s name
Sex	Passenger’s sex
Age	Passenger’s age
SibSp	Number of siblings/spouses aboard
Parch	Number of parents/children aboard
Ticket	Ticket number
Fare	Fare
Cabin	Cabin
Embarked	Port of embarkation

# 2. Feature Engineering
    2.1 What’s in a name?


   2.2 Do families sink or swim together?
    2.3 Treat a few more variables …
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
