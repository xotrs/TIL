## 점근적 표기

알고리즘은 입력 크기가 아주 작으면 알고리즘의 효율성에 상관없이 금방 끝난다. 알고리즘의 효율성이 문제가 되는 것은 입력의 크기가 충분히 클 때다. 그래서 알고리즘의 수행 시간은 항상 입력의 크기가 충분히 클 때 분석한다. 즉, 점근적 분석을 한다.


알고리즘의 분석에 사용하는 대표적인 세 가지 점근적 표기법을 하나씩 알아보자.



1. Θ-표기법

알고리즘의 소요 시간이 입력의 크기 n에 대해 Θ(n^2)이라면 대략 n^2에 비례하는 시간이 소요됨을 뜻한다. Θ(f(n))은 점근적 증가율이 f(n)과 일치하는 모든 함수의 집합이다. 다시 말하면, Θ(f(n))은 최고차항의 차수가 f(n)과 일치하는 함수의 집합이다. 점근적 상한과 점근적 하한의 교집합이다.



2. O-표기법

알고리즘의 소요 시간이 입력의 크기 n에 대해 O(n^2)이라면 기껏해야 n^2에 비례하는 시간이 소요됨을 뜻한다. O(f(n))은 점근적 증가율이 f(n)을 넘지 않는 모든 함수의 집합이다. 다시 말하면, O(f(n))은 최고차항의 차수가 f(n)과 일치하거나 더 작은 함수의 집합이다. 점근적 상한을 나타낸다.



3. Ω-표기법

알고리즘의 소요 시간이 입력의 크기 n에 대해 Ω(n^2)이라면 적어도 n^2에 비례하는 시간이 소요됨을 뜻한다. Ω(f(n))은 점근적 증가율이 적어도 f(n)이 되는 모든 함수의 집합이다. 다시 말하면, Ω(f(n))은 최고차항의 차수가 f(n)과 일치하거나 더 큰 함수의 집합이다. 점근적 하한을 나타낸다.