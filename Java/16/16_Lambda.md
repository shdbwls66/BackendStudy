# Lambda

## 람다 표현식

함수형 프로그래밍 개념을 자바에 도입한 것

익명 함수를 생성하기 위한 표현식

## 람다 표현식 구조

```java
(매개변수) -> {실행문}
```

## 람다 표현식 사용

number 리스트 내의 숫자로부터 짝수를 제거한 후 출력하는 코드

`removeIf()`는 조건에 해당하는 것만 제거하는 메서드

```java
List<Integer> numbers = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10));

numbers.removeIf((integer) -> integer % 2 == 0);
System.out.println(numbers);
```