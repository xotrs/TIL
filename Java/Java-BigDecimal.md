## BigDecimal?
실수의 정확한 표현을 위해서 정의된 클래스이며, float, double에서 다룰 수 없는 부동소수점을 처리한다. 

전 회사에서는 정확한 실수 계산을 해야 하는 로직도 없었기 때문에 BigDecimal에 대해 자세히 알지 못했다. 하지만 이번 회사에서는 커머스에 대한 기능을 지속해서 추가하고 있기 때문에 BigDecimal을 자주 접하고 있다. 그러므로 이번 기회에 회사에서 자주 사용하는 것들 위주로 정리를 해보려고 한다.

## 선언?
아래와 같이 생성자를 만들면 근사치 값이 출력되기 때문에 string 형태로 사용해야 한다.
```java
BigDecimal number1 = new BigDecimal(4.7);
//4.70000000000000017763568334566345253453455345125
```
to
```java
BigDecimal number1 = new BigDecimal("4.7");
//4.7
```

## 사칙연산?
일반적인 산술연산자로 사칙연산이 되지 않고 각각의 함수를 활용해야 한다.
```java
BigDecimal number1 = new BigDecimal("4.7");
BigDecimal number2 = new BigDecimal("3.1");

number1.add(number2) // add value 7.8
number1.subtract(number2) // subtract value 1.6 
number1.multiply(number2) // multiply value 14.57

```
나누기는 아직 정리되지 않아 다음 기회에 추가해야겠다...

## compareTo?
BigDecimal은 일반적인 비교 연산자로 비교할 수 없다. compareTo 함수를 이용해야 하는데 예제로 정리하면 다음과 같다.

```java
BigDecimal number3 = new BigDecimal("...");
BigDecimal number4 = new BigDecimal("...");

// number3가 number4보다 클 경우
if(number3.compareTo(number4)) == 1){ 
    ...
}

// number3가 number4가 같을 경우
else if(number3.compareTo(number4)) == 0){
    ...
}

// number3가 number4보다 작을 경우
else if(number3.compareTo(number4)) == -1){
    ...
}
```
