# VRP

## Tools

- python
- jupyter notebook (or tools, matplotib)
- OR Tools

## File desc

- vrp_test <br />
  가장 기본적인 vrp 문제 해결

- time vrp <br />
  매장 방문 조건이 있을 때 vrp 문제 <br />
  : (VRP_with_load_time) = 적재 시간이 있을 때 vrp 문제, 적재 시간은 상수(3)로 해결 => 차후 회귀를 통해 계산 예정 <br />
  : (VRP_with_timeWindow) = 매장에 방문해야하는 시간을 고려 <br />

- VRP_test_common <br />
  vrp중 다시 돌아와야 하는 factor를 해결한 문제 <br />
  => 0번 정점(depot)에서 다른 정점으로 가는 시간(거리)를 0으로 설정함으로서 해결 <br />

- VRP 2000 +
- ### 2000개 set vrp test

방법

1. 2000개의 dots(상점들) 분포 파악
2. sklearn로 kmeans inertia계산.
3. 그래프가 완만해지는 지점에서 군집 갯수 선정 (35)
4. 군집 갯수가 선정되면, 군집을 나누고 그 군집들의 mean lat,lng을 구한다.
5. 이를 바탕으로 각 cluster별 이동 시간 계산. kakao navigation api사용
6. 이후, time matrix(distance matrix)를 이용하여 vrp계산.

결과 :

Objective: 167288
Route for vehicle 0:
 35 ->  19 ->  24 ->  6 ->  12 ->  17 -> 35
Distance of the route: 16.0m

Route for vehicle 1:
 35 ->  10 ->  16 ->  7 ->  26 -> 35
Distance of the route: 25.5m

Route for vehicle 2:
 35 ->  1 ->  9 ->  20 ->  27 ->  3 -> 35
Distance of the route: 21.266666666666666m

Route for vehicle 3:
 35 ->  15 ->  25 ->  22 ->  2 -> 35
Distance of the route: 26.0m

Route for vehicle 4:
 35 ->  4 ->  32 ->  30 ->  31 ->  0 ->  28 -> 35
Distance of the route: 22.9m

Route for vehicle 5:
 35 ->  29 ->  21 ->  5 ->  33 ->  18 -> 35
Distance of the route: 25.866666666666667m

...

35 ->  11 ->  13 ->  14 -> 35
Distance of the route: 24.633333333333333m

Maximum of the route distances: 26.0m

### 개선 방향:

- cluster에서 각 상점 Pick up시간 계산 요망