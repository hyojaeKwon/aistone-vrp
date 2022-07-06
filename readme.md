# VRP

## 사용 툴

1. 시간 계산
    - Kakao navigation api
2. 지도
    - OpenStreetMap
3. VRP
    - OR tools
4. Clustering
    - Scikit-learn(Kmeans)
    - matplotlib
    - pandas

## 가설 수립

⇒ 클러스터를 나누고, 그 클러스터 안에서 목적지를 학사기숙사 B동으로 한 vrp를 수행하면 연산 횟수를 더 줄일 수 있을 것이다.

## AI 모델, 알고리즘

1. 클러스터를 나누기 위해 intertia를 측정한다. 클러스터의 수는 1~100으로 설정한다. (100이상이 되면 클러스터링을 하는 의미가 없어진다고 판단)

![Untitled](VRP%20fa418cd45394450eac7b85ffbf896f2c/Untitled.png)

1. 이를 바탕으로 클러스터의 수를 정한다. (50)
2. 클러스터링을 하고 결과를 확인한다.
    
    ```python
    from sklearn.cluster import KMeans
    from sklearn.preprocessing import MinMaxScaler
    
    scaler = MinMaxScaler()
    data_scale = scaler.fit_transform(bm_data_latlng)
    
    k = 50
    
    model = KMeans(n_clusters=k,random_state=10)
    
    model.fit(data_scale)
    bm_data_latlng['cluster'] = model.fit_predict(data_scale)
    
    bm_data_latlng
    ```
    

![Untitled](VRP%20fa418cd45394450eac7b85ffbf896f2c/Untitled%201.png)

1. 각 클러스터 별 중심점을 정하고, vrp를 수행한다. 
    
    ![Untitled](VRP%20fa418cd45394450eac7b85ffbf896f2c/Untitled%202.png)
    
    수행 결과 :
    
    ![Untitled](VRP%20fa418cd45394450eac7b85ffbf896f2c/Untitled%203.png)
    
2. 이 결과를 바탕으로 연결되어있는 클러스터에 해당하는 상점 끼리 vrp를 다시 수행한다. 이 때 드라이버의 수는 3명으로 고정한다.
3. 

## 결과

가장 많이 이동한 드라이버 거리 ⇒ 약 7.66km

평균 드라이버 이동 거리 ⇒ 약 5.61km

드라이버 수 : 39명

최종 vrp 연산시간 약 20분

누락된 상점 수  : 0

## 피드백

1. 완벽하게 거리 구하는 방법이 제시되면 좋겠다.
2. 거리 이외에도 시간을 같이 구할 수 있는 방법이 있었으면 좋겠다.
3. 데이터 전처리 과정을 겪는다면 오류를 피할 수 있을 것이다.

## 향후 계획

1. 데이터 전처리를 통해 지도에 깔끔하게 표기