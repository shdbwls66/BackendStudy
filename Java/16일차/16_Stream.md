# Stream

## Stream API

Java 8에서 도입

컬렉션, 배열 등의 데이터를 함수형 프로그래밍 스타일로 처리하는 기능 제공

데이터의 흐름을 나타내며, 중간 연산과 최종 연산을 통해 데이터를 처리할 수 있음

원본 데이터 변경 X, 내부 반복을 통해 코드의 가독성과 유지보수성을 향상시킴

## Stream 생성

컬렉션에서 생성

```java
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
Stream<Integer> stream = list.stream();
```

배열에서 생성

```java
int[] array = {1, 2, 3, 4, 5};
IntStream stream = Arrays.stream(array);
```

직접 생성

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5);
```

## 중간 연산

Stream을 변환하고 필터링 등의 작업 수행

최종 연산이 호출될 때까지 실행 X

### `filter()`

조건에 해당하는 요소만 포함하는 새로운 Stream 생성

```java
// 홀수만 필터링
// 결과를 보기 위해 forEach() 메서드 사용
List<Integer> number = Arrays.asList(1, 2, 3, 4, 5);
number.stream()
  .filter(integer -> integer % 2 != 0)
  .forEach(integer -> System.out.println(integer));
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/62d00e75-2533-400a-a526-f1555efa08f6/Untitled.png)

### `map()`

각 요소에 주어진 함수를 적용한 결과로 이루어진 새로운 Stream 생성

```java
// 홀수만 필터링
// 필터링한 요소에 각각 2배 계산해 저장
List<Integer> number = Arrays.asList(1, 2, 3, 4, 5);
number.stream()
  .filter(integer -> integer % 2 != 0)
  .map(integer -> integer * 2)
  .forEach(integer -> System.out.println(integer));
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/c3e35a3b-34a9-4faf-80a4-c4f14560497e/Untitled.png)

### `sorted`

요소를 정렬한 새로운 Stream 생성

```java
// 오름차순으로 정렬
List<Integer> number = Arrays.asList(5, 3, 4, 2, 1);
number.stream()
	.sorted()
  .forEach(integer -> System.out.println(integer));
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/a173dafb-4a34-4c2d-bcee-748c8dface04/Untitled.png)

## 최종 연산

Stream에서 결과 생성

최종 연산이 호출되면 Stream이 닫히며, 더 이상 이용 X

최종 연산 코드까지 작성하였을 때 지역 변수가 삽입 되는 것을 볼 수 있음

### `forEach()`

각 요소에 주어진 동작 수행

forEach() 메서드 사용은 앞에서 하였으므로 생략

### `collect()`

요소를 수집하여 컬렉션이나 다른 형태로 변환

```java
// 홀수 요소만 모아서 리스트 형태로 출력
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
List<Integer> result = numbers.stream()
    .filter(integer -> integer % 2 != 0)
    .collect(Collectors.toList());

System.out.println(result);
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/e87f5ea5-2076-4860-9cae-8a808d3b0dbb/Untitled.png)

### `reduce()`

요소를 결합하여 하나의 값으로 만듦

```java
// 홀수 요소의 합
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
  int result = numbers.stream()
    .filter(integer -> integer % 2 != 0)
    .reduce(0, (a, b) -> a + b);

System.out.println(result);
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/a0b6e666-2276-4d4c-a4c2-ad490b6390a7/Untitled.png)

## 문제

### 문제 1
홀수 필터링하기

list 컬렉션 number 생성, stream() 메서드로 Stream 생성

filter() 메서드로 홀수 필터링

forEach() 메서드로 필터링된 요소를 출력

```java
List<Integer> numbers = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10));

numbers.stream()
        .filter(integer -> integer % 2 != 0)
        .forEach(integer -> System.out.println(integer));
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/d22154aa-1234-4b74-b6ac-359a60f5dcbf/Untitled.png)

### 문제 2

문자열 길이 매핑하기

list 컬렉션 words 생성, stream() 메서드로 Stream 생성

map() 메서드로 각 요소로 접근해 str.length() 구함

collect() 메서드로 리스트 형태로 요소값 저장

```java
List<String> words = Arrays.asList("Java", "Stream", "API", "Example");

List<Integer> list = words.stream()
        .map(str -> str.length())
        .collect(Collectors.toList());
System.out.println(list);
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/8edd934f-b930-4ed8-94f5-f32a8b4c7817/Untitled.png)

### 문제 3

단어 수 세기

```java
String sentence = "Java Stream API Example";

// 공백을 기준으로 문자열을 나누어 배열로 저장
// 따옴표 띄어야 함!!
String[] arr = sentence.split(" ");

// count() 메서드를 이용해 단어 개수 구함
long count = Arrays.stream(arr).count();
System.out.println(count);
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/fc554cfa-1f1b-467c-901c-119b41af9792/Untitled.png)

### 문제 4

문자열 길이가 5 이하인 문자열만 출력

```java
List<String> fruits = new ArrayList<>(Arrays.asList("apple", "banana", "melon", "a", "bb"));
List<String> list =
    fruits.stream()
            .filter(str -> str.length() <= 5)
            .collect(Collectors.toList());

System.out.println(list);
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/c3ca03dd-a65f-42ac-8238-9b16c5d1ae1d/Untitled.png)