# while문
## while 반복문

조건이 참인 **동안** 코드 무한 반복

조건은 참 또는 거짓으로 판별 가능한 표현식 이어야 함

## 기본 구조

```java
while (조건) {
    // 조건이 참인 동안 실행되는 코드
}
```


## while 반복문 작성해보기

(증감식을 작성하지 않으면 코드가 무한 반복하므로 빼먹지 않도록 할 것!)

```java
// 10부터 0까지 카운트

int i = 10;
while (i >= 0) {
  System.out.println("현재 카운트 " + i);
  i--;
}
System.out.println("카운트 종료");
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/ad746063-4489-452b-90b9-fd6e067f65f7)

```java
// 1부터 100까지 합

int n = 0, sum = 0;
while (n <= 100) {
    sum += n;
    n++;
}
System.out.println(sum);
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/fc78d96b-92be-4185-9499-8df747d2889d)


```java
// 평균 계산

int[] numbers = {5, 2, 9, 1, 7, 4, 6, 3, 8};
int n = 0;
int sum = 0;
while (n < numbers.length) {
  sum += numbers[n];
  n++;
}
System.out.println(sum / numbers.length);
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/a69fae2e-3e6d-4212-90dd-67c5d377f4b2)


```java
// 3의 배수 출력

int i = 0;
while (i <= 300) {
  if (i % 3 == 0) {
    System.out.println(i);
  }
  i++;
}
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/04aec0a4-3a8b-4bcf-bc1f-ffcb3ad2b070)


## 문제
### 1번

주어진 배열에서 가장 큰 값을 찾아 출력하는 프로그램을 작성하세요.
    
```java
int[] numbers = {10, 5, 8, 20, 3, 15, 9, 2};
```
    
변수 max를 배열의 인덱스 0인 값으로 선언
    
if문으로 다른 인덱스 값과의 크기 비교를 반복하고, 이 때 숫자가 더 큰 쪽을 max로 만들기
    
```java
// 최대값 구하기
int[] numbers = {10, 5, 8, 20, 3, 15, 9, 2};
int max = numbers[0];
int n = 1;
while (n < numbers.length) {
  if (numbers[n]>max){
    max = numbers[n];
  }
  n++;
}
System.out.println(max);
```
    
![image](https://github.com/shdbwls66/backendJava/assets/168792230/246e7c73-f202-452a-9e88-3e0041c0ff2a)


### 2번

주어진 배열에서 양수의 합과 음수의 합을 각각 구하여 출력하는 프로그램을 작성하세요.
    
```java
int[] numbers = {4, -2, 9, -7, 5, 1, -3, 6, -1, 8};
```
    
if문으로 양수와 음수를 구분하여, 양수의 합과 음수의 합을 각각  구함
    
```java
// 양수 합, 음수 합 각각 구하기

int[] numbers = {4, -2, 9, -7, 5, 1, -3, 6, -1, 8};
int i = 0;
int sum1 = 0;
int sum2 = 0;
while (i < numbers.length) {
  if (numbers[i] > 0) {
    sum1 += numbers[i];
  } else {
    sum2 += numbers[i];
  }
  i++;
}
System.out.println("양수의 합: " + sum1);
System.out.println("음수의 합: " + sum2);
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/599b4dde-e0c9-44e7-99cf-a58b682917b0)
