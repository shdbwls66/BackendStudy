# for문
## for 반복문

특정 횟수만큼 코드 반복 실행

조건식이 true면 코드 블록 실행, false면 반복문 종료

### 기본 구조

```java
for (초기식; 조건식; 증감식) {
    // 조건식이 참일 때 실행되는 코드
}
```

실행 순서는..

초기식 실행 → 조건식 확인 → 코드 블록 실행 → 증감식 → 조건식 → 코드 블록 실행 → (증감식 → 조건식 → 코드 블록 실행 반복…) 

조건식이 false일 때 반복문 종료


### for 반복문 작성해보기

1부터 4까지 출력

```java
for (int i = 1; i < 5; i++) {
  System.out.println("현재 i의 값은 = " + i);
}
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/f098d5e8-fb3e-4564-b78b-041f96bac3c1)


1부터 100까지 숫자 중에서 모든 짝수의 합

if문으로 2로 나눈 나머지가 0이 나오는 숫자들을 판별하고 해당 숫자들의 합을 구하기

```java
// 1부터 100까지 짝수의 합

int sum = 0;
for (int i = 1; i <= 100; i++) {
  if (i % 2 == 0) {
    sum += i;
  }
}
System.out.println(sum);
```


이런 방법으로도 짝수 합을 구할 수 있음

rangeClosed()에 범위 작성, filter()에 조건 작성

```java
int hap = IntStream.rangeClosed(1, 100).filter(i -> i % 2 == 0).sum();
System.out.println(hap);
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/7415dfc4-b07d-4d0e-9fa3-c16547bab3f1)


### 문제 1

사용자로부터 정수 n을 입력받아, 1부터 n까지의 정수 중에서 3의 배수이면서 5의 배수인 수의 합을 계산하여 출력하는 프로그램을 작성하세요.
    
    
and 연산자로 3의 배수이자 5의 배수인 정수를 구함

```java
// 3의 배수이면서 5의 배수인 수의 합

int sum1 = 0;
for (int n = 1; n <= 20; n++) {
  if (n % 3 == 0 && n % 5 == 0) {
    sum1 += n;
  }
}
System.out.println(sum1);
```
    
![image](https://github.com/shdbwls66/backendJava/assets/168792230/dbb1b4e2-0a36-40dc-ada3-4b4eab90e48f)


### 문제 2

피보나치 수열의 첫 10개 항을 출력하는 프로그램을 작성하세요.
    
피보나치 수열

- 첫 번째 항과 두 번째 항은 1
- 세 번째 항부터는 이전 두 항의 합으로 정의

첫 10개의 항

`1, 1, 2, 3, 5, 8, 13, 21, 34, 55`

배열 arr 생성 후 인덱스 0번 값과 1번 값을 1로 초기화

for문으로 수열 계산 후 배열 arr에 담기 (0번과 1번은 값을 이미 선언 했으므로 2번부터 선언)

배열 값 출력

```java
int[] arr = new int[10];
arr[0] = 1;
arr[1] = 1;
    
for(int n = 2; n < arr.length; n++) {
  arr[n] = arr[n-2] + arr[n-1];
}

for(int i : arr) {
 System.out.println(i);
} // 값 출력
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/f31293b5-5e55-4218-820b-47a92eae7bd1)



## 향상된 for문

배열이나 컬렉션의 요소를 순차적으로 처리하는 반복문

기존 for문에 비해 가독성이 좋음

**요소에 직접 접근**

### 기본 구조

```java
for (요소타입 변수명 : 배열 또는 컬렉션) {
    // 반복할 코드
}
```