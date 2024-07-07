# 이중 반복문과 break, continue
## 이중 반복문

자바에서는 여러 반복문을 중첩 해서 코드를 작성할 수 있음

### 기본 구조

바깥쪽 반복문이 실행될 때 안쪽 반복문 실행 시작

안쪽 반복문 실행이 끝난 후에 바깥쪽 반복문 실행

이게 반복됨

```java
for (초기식1; 조건식1; 증감식1) {
    // 바깥쪽 반복문의 본문
    for (초기식2; 조건식2; 증감식2) {
        // 안쪽 반복문의 본문
    }
}
```


### 이중 반복문 작성해보기

구구단 출력

i=2일 때, j는 1부터 9까지 출력

i=3일 때, j는 1부터 9까지 출력

이 과정을 i<10 결과가 거짓이 될 때까지 반복

```java
// 구구단

int i;
int j;
int result;

for (i = 2; i < 10; i++) {
  for (j = 1; j < 10; j++) {
    result = i * j;
    System.out.println(i + " * " + j + " = " + result);
  }
}
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/920287c2-6f55-4b34-b0bf-2d2f85e6acee)


### 문제

구구단 19단을 역방향으로 출력하는 프로그램을 작성하세요.

출력 형식은 "19 x 19 = 361"부터 "19 x 1 = 19"까지 역순으로 출력되어야 합니다.
    
    
19단부터 1단까지 출력하는 코드 작성

역순 출력 시키기 위해 i와 j값을 19에서 1씩 감소하도록 코드 작성

변수 result에 i와 j를 곱한 값을 선언
    
```java
// 구구단 19단
int i;
int j;
int result;

for (i = 19; i > 0; i--) {
  for (j = 19; j > 0; j--) {
    result = i * j;
    System.out.println(i + " * " + j + " = " + result);
  }
}
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/d89ae65b-a012-4d5b-90dc-b5e7ade48eb9)



## break

**반복문을 즉시 종료**하고 바로 다음 코드로 이동

### break문 작성해보기

5가 되었을 때 반복문 중단 하기

```java
int number = 0;
while (number < 10) {
  System.out.println("현재 숫자: " + number);
  if (number == 5) {
    System.out.println("5가 되었습니다.");
    break;
  }
  number++;
}
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/050eaab1-7d58-49ad-83c8-ecf48450a846)


for문에서 break 사용해보기

```java
for (int i = 0; i < 10; i++) {
  System.out.println("현재 숫자: " + i);
  if (i == 5) {
    break;
  }
}
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/76cb1d76-ad76-4768-b382-c78a274e7603)


j값이 5일 때 j값이 속한 반복문 중단

(i값 0, j값 0, 1, 2, 3, 4, 5, i값 1, j값 0, 1, 2, 3, 4, 5…. 이런식으로 반복 출력..)

```java
for(int i = 0; i < 10; i++) {
  System.out.println("현재 i의 값은 = " +i);
  for(int j = 0; j < 10; j++) {
    System.out.println("현재 j의 값은 = " +j);
    if (j == 5) {
      break;
    }
  }
}
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/9b8772a8-709f-4de6-bcb3-f4348d35acf9)


i가 50일 때 break, j가 80일 때 break

i가 1씩 증가할 때마다, j는 2~80까지 출력, i가 50일 때 반복문 중단 되면서 실행 끝!

```java
int i, j;
for(i = 1; i <= 100; i++) {
  System.out.println("현재 i값: " + i);
  if (i == 50) {
    break;
  }
  for(j = 2; j <= 100; j++) {
    System.out.println("현재 j값: " + j);
    if (j == 80) {
      break;
    }
  }
}
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/a995c255-c391-4fa2-a830-88ef634cac09)



## continue

현재 실행되는 코드를 즉시 중단하고 **다음 반복으로 넘김**

### continue문 작성해보기

0부터 9까지 출력, 이 때 3은 출력 x

```java
int number = 0;

while (number < 10) {
  number++;
  if (number == 3) {
    continue;
  } 
  System.out.println("현재 값은 :" + number);
}
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/ff2770ea-f551-41ae-a186-046391094d65)


for문으로 작성해보면..

```java
for (int i = 0; i < 10; i++) {
  if (i == 3) {
    continue;
  }
  System.out.println("현재 값은 :" + i);
}
```



💡 **주의: 증감식 위치에 신경 쓰기**
<aside>
  
    `number++;` 을 continue 밑에 작성하면
    
    숫자가 3이 되었을 때 continue 밑의 코드를 실행하지 않고
    
    바로 다음 반복으로 넘어가기 때문에 값이 3인 상태로 무한 반복 일어남

</aside>

![image](https://github.com/shdbwls66/backendJava/assets/168792230/c03a6157-7025-4622-818d-ae1a03c57f2a)


### break와 continue 활용

적절히 혼용하면 다양한 조건에 따른 반복문을 구현할 수 있음

i가 5일 때 반복문 중단, j값은 5를 제외하고 출력

```java
for (int i = 0; i < 10; i++) {
  if (i == 5) {
    break;
  }
  for (int j = 0; j < 10; j++) {
    if (j == 5) {
      continue;
    }
    System.out.println(j);
  }
}
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/93f3d872-a816-4d66-883b-61d2ba8e4658)


1부터 10까지 숫자 출력, 이 때 4와 7은 건너뛰기

4와 7, 모두 참으로 묶기 위해 or 연산자 사용

```java
for(int i = 1; i <= 10; i++) {
  if (i == 4 || i == 7) {
    continue;
  }
  System.out.println(i);
}
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/5375dcda-ea7a-4abb-b8e3-c65c640717ee)