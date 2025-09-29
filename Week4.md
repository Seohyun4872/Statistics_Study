# 통계학 4주차 정규과제

📌통계학 정규과제는 매주 정해진 분량의 『*데이터 분석가가 반드시 알아야 할 모든 것*』 을 읽고 학습하는 것입니다. 이번 주는 아래의 **Statistics_4th_TIL**에 나열된 분량을 읽고 `학습 목표`에 맞게 공부하시면 됩니다.

아래의 문제를 풀어보며 학습 내용을 점검하세요. 문제를 해결하는 과정에서 개념을 스스로 정리하고, 필요한 경우 추가자료와 교재를 다시 참고하여 보완하는 것이 좋습니다.

4주차는 `2부-데이터 분석 준비하기`를 읽고 새롭게 배운 내용을 정리해주시면 됩니다


## Statistics_4th_TIL

### 2부. 데이터 분석 준비하기

### 10. 데이터 탐색과 시각화

<!-- 10. 데이터 탐색과 시각화에서 10.1 탐색적 데이터 분석부터 10.4 비교 시각화 파트까지 진행해주시면 됩니다. -->



**(수행 인증샷은 필수입니다.)** 

<!-- 이번주는 확인 문제가 없고, 교재의 실습에 있는 부분을 따라해주시면 됩니다. 데이터셋과 참고자료는 노션의 정규과제란에 있는 깃허브를 활용해주시면 됩니다. -->



## Study ScheduleStudy Schedule

| 주차  | 공부 범위     | 완료 여부 |
| ----- | ------------- | --------- |
| 1주차 | 1부 p.2~46    | ✅         |
| 2주차 | 1부 p.47~81   | ✅         |
| 3주차 | 2부 p.82~120  | ✅         |
| 4주차 | 2부 p.121~167 | ✅         |
| 5주차 | 2부 p.168~202 | 🍽️         |
| 6주차 | 3부 p.203~250 | 🍽️         |
| 7주차 | 3부 p.251~299 | 🍽️         |

<!-- 여기까진 그대로 둬 주세요-->



---

# 1️⃣ 개념 정리 

## 10. 데이터 탐색과 시각화

```
✅ 학습 목표 :
* EDA의 목적을 설명할 수 있다.
* 주어진 데이터셋에서 이상치, 누락값, 분포 등을 식별하고 EDA 결과를 바탕으로 데이터셋의 특징을 해석할 수 있다.
* 공분산과 상관계수를 활용하여 두 변수 간의 관계를 해석할 수 있다.
* 적절한 시각화 기법을 선택하여 데이터의 특성을 효과적으로 전달할 수 있다.
```

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
**시각화 종류**
- 비교 시각화
- 분포 시각화
- 관계 시각화
- 공간 시각화

**10.1 탐색적 데이터 분석(EDA)**
~~~
#데이터 샘플 확인
df.head()
#각 칼럼별 속성 및 결측치 확인
df.info()
df.isnull().sum()
#각 칼럼의 통계치 확인
df.describe()
~~~
~~~
#각 수치형 컬럼별 왜도 확인
# Select only numerical columns
df_numeric = df.select_dtypes(include=['number'])
skewness = df_numeric.skew()

# Display the skewness
print("Skewness of numerical columns:")
print(skewness)
>> 왜도를 통해 분포의 비대칭성과 이상치를 확인 가능
~~~
~~~
# 각 칼럼의 첨도 확인
# Select only numerical columns and calculate kurtosis
kurtosis = df_numeric.kurtosis()

# Display the kurtosis
print("Kurtosis of numerical columns:")
print(kurtosis)
>> 첨도를 통해 분포의 뾰족함 정도와 데이터의 극단값이 많은지 적은지 확인가능
~~~
~~~
**시각화**
sns.displot(df['lead_time'])
#lead_time은 예약 날짜부터 투숙 날짜까지의 일수 차이 의미 
#호텔 구분에 따른 lead_time 분포 차이 시각화
sns.violinplot(x="hotel", y="lead_time", data=df, inner=None, color=".8")
sns.stripplot(x="hotel", y="lead_time", data=df, size=1)
~~~

**10.2 공분산과 상관성 분석**
공분산: 두 분산의 관계 - 변수 각 값의 편차들을 서로 곱한 값을 모두 더하고 (n-1)로 나눔  
상관계수: 공분산을 통해 나타내지 못했던 상관성의 정도를 나타냄  
~~~
**등간, 비율척도 데이터에서의 상관계수**
- 피어슨상관계수: X1,X2가 함께 변하는 정도(공분산)/ X1,X2가 변하는 전체 정도
- 산점도랑 함께 보면 명확함, 보통 프로그램에서 히트맵이나 상관분석 표로 확
- 해당 상관계수를 제곱한 값: 결정계수(회귀분석)
~~~

**서열척도, 명목척도 간의 상관관계 분석**
<img width="796" height="315" alt="image" src="https://github.com/user-attachments/assets/8b74618d-33e4-4a2f-a0cd-670ca0eb417c" />


**10.3 시간 시각화**
선그래프(연속형): 시간간격의 밀도가 높을 때 사용  
- 이동평균 방법: 데이터의 연속적 그룹의 평균 구하기   
막대그래프(분절형): 시간의 밀도가 낮은 경우 사용(ex: 1년 동안의 월 간격 단위흐름)  
- 막대그래프, 누적막대, 점 그래프

**10.4 비교시각화**
그룹별 요소가 많아지게되면 더욱 효율적인 표현 기법이 필요함  
* 히트맵 차트 활용
- 하나의 변수(그룹) * N개의 각 변수에 해당하는 값들(수치형)
* 방사형차트(Radar chart)
- 하나의 그룹별 각 변수에 대한 값: 하나의 차트에 하나의 그룹을 시각화할 수도 있고 아래처럼 하나의 차트에 모든 그룹을 합쳐서 시각화할 수도 있다. 
<img width="866" height="609" alt="image" src="https://github.com/user-attachments/assets/44f35f17-1b3d-4c45-bc0c-e2e3fa88e8d7" />
* 평행 좌표 그래프(Parallel coordinates)

**10.5 분포시각화**
변수들이 어떤 요소로 어느정도의 비율로 구성되어 있는지를 확인하는 단계  
- 연속형(양적척도): 막대, 선 그래프, 히스토그램
  *히스토그램은 처음 20개 정도의 구간으로 나눈 뒤 조금씩 구간의 개수를 줄여가며 조정
- 명목형(질적척도): 파이차트, 도넛차트 사용 - 분포 정도를 면적으로 표현
또는 트리맵 차트(위계구조 표현 가능), 와플차트(위계구조 표현 X)등을 사용 가능
<img width="1066" height="349" alt="image" src="https://github.com/user-attachments/assets/23406ef0-0313-4bc1-8f49-5c124a558e1b" />

**10.6 관계 시각화**
~~~
**산점도**
- 두 개의 연속형 변수 간 관계를 나타낼 수 있는 것 
- 산점도는 극단치를 제거하고 그리는 것이 효율적임.
- 데이터가 많아 점들이 겹칠 경우, 점들의 투명도를 낮춰 밀도를 함께 표현
~~~
~~~
**버블차트**
- 3가지 요소의 상관관계 표현 가능(버블의 크기까지)
- 관측치가 너무 많게 되면 오히려 정보전달 효율이 떨어짐
~~~

**10.7 공간시각화**
데이터가 지리적 위치와 관련 있으면 실제 지도 위에 데이터를 표현하는 것이 효과적  
1) 도트맵(Dot Map): 지리적 위치에 동일한 크기의 작은 점을 찍어 해당 지역의 데이터분포나 패턴 표현
<img width="520" height="316" alt="image" src="https://github.com/user-attachments/assets/1ca910f1-5c44-4cd9-b737-193b3996df05" />

- 시각적인 개요를 파악하는 덴 유리, but 정확한 값을 전달하는덴 적합X

 2) 버블맵(Bubble map): 버블차트를 지도에 그대로 옮겨 둔 것
<img width="520" height="316" alt="image" src="https://github.com/user-attachments/assets/54c92565-f60d-45c0-8cb5-ad754ab2d25a" />

3) 코로플레스맵(Choropleth map): 단계구분도, 데이터 값의 크기에 따라 색상의 음영을 달리해 해당 지역에 대한 값을 시각화
<img width="532" height="295" alt="image" src="https://github.com/user-attachments/assets/ce7be254-12fe-4c01-a8f3-d13d7f6cb56e" />

4) 커넥션맵(Connection map)= 링크맵(link map): 지도에 찍힌 점들을 곡선이나 직선으로 연결해 지리적 관계를 표현, 연속적 연결을 통해 지도에 경로 표현 또한 가능
<img width="530" height="284" alt="image" src="https://github.com/user-attachments/assets/088a611f-2fb2-486f-b718-904a903d4281" />

- 지리적 관계의 패턴을 파악하기 위해 주로 사용함. (ex: 지역 간 무역, 항공경로 등)

+) 플로우맵, 카토그램 등 

**10.8 박스플롯**
하나의 그림으로 양적 척도 데이터의 분포 및 편향성, 평균, 중앙값 등 다양한 수치를 보기 쉽게 정리해줌  <img width="626" height="414" alt="image" src="https://github.com/user-attachments/assets/2524460c-f700-4290-9162-c0851abe8a3b" />




 
<br>
<br>

---

# 2️⃣ 확인 과제

> **교재에 있는 실습 파트를 직접 따라 해보세요. 실습을 완료한 뒤, 결과화면(캡처 또는 코드 결과)을 첨부하여 인증해 주세요.단순 이론 암기보다, 직접 손으로 따라해보면서 실습해 보는 것이 가장 확실한 학습 방법입니다.**
>
> > **인증 예시 : 통계 프로그램 결과, 시각화 이미지 캡처 등**

~~~
<img width="1015" height="1150" alt="image" src="https://github.com/user-attachments/assets/8f9daf21-8446-4454-a0c4-d0138ce8c2a1" />
<img width="1000" height="700" alt="image" src="https://github.com/user-attachments/assets/ecfa64d9-d8af-427a-8875-5708314769de" />
<img width="2000" height="900" alt="image" src="https://github.com/user-attachments/assets/6e8a711c-061b-4adc-b4c8-8ceb385f2ae7" />
<img width="1581" height="1198" alt="image" src="https://github.com/user-attachments/assets/8bfd366c-ee57-4c75-956b-2bdd965e1601" />
<img width="1000" height="600" alt="image" src="https://github.com/user-attachments/assets/3b749ecd-8eff-49b2-b253-e77e68c3d8a2" />
<img width="1273" height="994" alt="image" src="https://github.com/user-attachments/assets/39e0dbdf-9e37-423d-b102-3bc34a01e42f" />
<img width="1092" height="929" alt="image" src="https://github.com/user-attachments/assets/a3d37a54-1b5e-4a0f-b829-acf478f6ef64" />
~~~





### 🎉 수고하셨습니다.
