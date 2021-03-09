# NS SHOP+ 판매실적 예측을 통한 편성 최적화 방안(모형) 도출
### toBigCon : 투빅스 빅콘테스트팀입니다.
<br/>
<br>


## 📅 프로젝트 기간
2020.07.20 ~ 2020.09.28
<br/>
<br>
  
## 👨‍👨‍👧‍👧 Members
- 김미성[[MiSungKim]](https://github.com/MiSungKim)
- 김태욱[[taeukkkim]](https://github.com/taeukkkim)
- 김태한[[han811]](https://github.com/han811)
- 이유진[[YoojLee]](https://github.com/YoojLee)
<br/>
<br/>

## 🔎 프로젝트 목적
- 2020 BigContest 챔피언스 리그
- **NS SHOP+ 판매실적 예측을 통한 편성 최적화 방안(모형) 도출**    
  → NS Shop+편성데이터(NS홈쇼핑) 를 활용하여 방송편성표에 따른 판매실적을 예측하고, 
  최적 수익을 고려한 요일별/ 시간대별 / 카테고리별 편성 최적화 방안(모형) 제시
<br/>
<br/>

## 📝 프로젝트 소개
### [Model Flow]
![image](https://user-images.githubusercontent.com/28949182/110498327-90a8cd00-813a-11eb-9361-034553780b92.png)

<br/><br>
- **판매실적 예측 모델**

  0️⃣ 상품군별로 다른 데이터 분포 → 각 상품군별로 다른 모델 fitting     
![image](https://user-images.githubusercontent.com/28949182/110498510-bdf57b00-813a-11eb-9e4b-bf0495b7b903.png)

  1️⃣ Tree-based model: LGBM, XGB, CATBOOST

    판매실적의 분포가 매우 치우쳐져 있음. 따라서 regression 트리 모델을 학습시킬 때 objective function을 tweedie, gamma 등으로 조정하여 모델이 Sales의 분포를 반영하여 학습하도록 함.

  2️⃣ Text CNN

    상품명에서의 정보를 추출해내기 위해 text cnn을 활용. 단순히 feature extractor로 활용하기보다는 regression 모델로 구축하여 바로 값예측에 활용할 수 있도록 함. 

  3️⃣ Bayesian Optimization: hyperopt

    베이지안 최적화를 통해 트리모델의 하이퍼파라미터 튜닝을 진행. 

  4️⃣ 앙상블

    전체 데이터 기반 트리 모델 + 상품군별 트리 모델 + Text CNN

<br/><br>
- **편성 최적화**
  - 예측된 판매실적을 통해 상품 판매 방송의 편성을 시간별, 상품별로 최적화.

  - 헝가리안 알고리즘

    : 판매실적이 극대화되는 시간별, 상품별 조합을 탐색함.   
![image](https://user-images.githubusercontent.com/28949182/110498600-d1084b00-813a-11eb-80f7-ce18ac64c00d.png)

<br/><br>
- **앙상블**
  - 앙상블을 통해 모델 간 Variance를 경감. 최종 성능은 개별 성능 대비 향상되었음. 
    (평가지표: MAPE)
![image](https://user-images.githubusercontent.com/28949182/110498674-e1b8c100-813a-11eb-96e4-67a6128b59a5.png)
<br/>
<br/>


## **🗂 Structure**

```
  📁 00_공휴일 API.ipynb
  📁 01_base_data_전처리.ipynb
  📁 01_2_base_data_전처리_(편성표용).ipynb
  📁 02_데이터합치기.ipynb
  📁 02_2_뉴스시청률_crawling.ipynb
  📁 03_EDA_FE.ipynb
  📁 04_FeatureSelection_test.ipynb
  📁 05_Tunning.ipynb
  📁 06_TextCNN_model.ipynb
  📁 07_앙상블실험_및_제출파일생성.ipynb
  📁 08_헝가리안.ipynb
```
<br/>
<br/>

## 🙂 참고 
![image](https://user-images.githubusercontent.com/28949182/110491249-6eac4c00-8134-11eb-999e-8d28ba6bd6e8.png)
- [빅콘테스트 홈페이지](https://www.bigcontest.or.kr/index.php)
- [빅콘테스트 대회 요강](https://www.bigcontest.or.kr/points/content.php)
- [빅콘테스트 공지사항](https://www.bigcontest.or.kr/community/board.php?gubun=notice)
