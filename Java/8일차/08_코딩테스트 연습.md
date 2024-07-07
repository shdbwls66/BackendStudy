# 코딩테스트 맛보기 #2

## 1번
```
문자열 데이터를 전달 받으면 각각의 문자열 사이에 @ 표시를 집어 넣는 함수를 만들어 봅니다.
단, 재귀 함수를 이용하여 풀어보세요.

예시
System.out.println(printAt("hello")); // "h@e@l@l@o"
static String printAt(String str){

}
```

### 문제 풀이
```java
if(str.length() <= 1){
    return str;
}

return str.charAt(0)+"@" + printAt(str.substring(1));
```
- str 0번 값인 @ 반복 실행
- 입력되는 str 길이가 1 이하가 될 때 @결합 X

```
실행되는 방식

str = hello
str.length() = 5
h@+printAt(”ello”)

str = ello
str.length() = 4
h@+e@+printAt(”llo”)

str = llo
str.length() = 3
h@+e@+l@+printAt(”lo”)

str = lo
str.length() = 2
h@+e@+l@+l@+printAt(”o”)

str = l
str.length() = 1 이므로 o만 반환
h@+e@+l@+l@+o
```

---

**<코드실행>**
```java
public static void main(String[] args) {
    System.out.println(printAt("helloWorld")); // "h@e@l@l@o"
}
```
![alt text](image.png)


---
### 반복문 사용해서 풀어보기

```java
static String printAt(String str) {
    int i = 0;
    String result = "";

    while (i < str.length() - 1) {
    result += str.charAt(i) + "@";
    i++;
    }
    result += str.charAt(i);

    return result;
```

- 반복문을 사용하여 마지막 글자 제외한 문자열의 각 글자를 ‘@’와 결합

    - “(i번 글자)@” 반복

    - 마지막 글자 제외하므로 범위는 `i < str.length() - 1`

- 마지막은 해당하는 문자만 추가하기

---
**<코드실행>**
    
```java
public static void main(String[] args) {
    System.out.println(printAt("helloWorld")); // "h@e@l@l@o"
}
```



## 2번
```
경찰이 당신을 과속으로 잡았을 때 내야 할 벌금을 계산하는 코드를 작성해보겠습니다.
만약 당신의 속도가 60 이하라면 벌금은 없습니다.
속도가 61에서 80 사이(포함)라면 벌금은 100원입니다.
속도가 81 이상이라면 벌금은 200원입니다.
단, 휴일인 경우 속도 한도가 5 더 높아집니다.

속도가 60 이하라면 벌금은 0원입니다.
속도가 61 이상이라면 벌금은 100원입니다.
만약 휴일이라면 속도가 65라도 벌금은 0원입니다.
  
static int speedRacer(int speed, boolean isHoliday){

}
```

### 문제 풀이
```java
static int speedRacer(int speed, boolean isHoliday) {
  
  int tax = 0;
  int safeSpeed = 60;
  int dangerSpeed = 80;

  if (isHoliday) {
      safeSpeed += 5;
      dangerSpeed += 5;
  }

  if (speed <= safeSpeed) {
      tax = 0;
  } else if(speed <= dangerSpeed) {
      tax = 100;
  } else {
      tax = 200;
  }

  return tax;
  
}
```

- 속도 상태를 나타내주는 변수 선언 (정상 / 벌금 100원 / 벌금 200원 판별)
    - `safeSpeed` 정상 / 벌금 100원 커트라인 정의, `dangerSpeed` 벌금 커트라인 정의
- 벌금 계산용 변수 선언 (`tax`)
- `isHoliday` 일 때
    - 커트라인을 정의한 변수에다 +5
- `!isHoliday` 일 때
    - 각 조건에 따라 벌금 책정
- 책정한 벌금 `return`

---
**<코드실행>**
```java
System.out.println(speedRacer(100, true));
System.out.println(speedRacer(63, true));
```



## 3번
```
세 개의 정수 a, b, c가 주어졌을 때, 
두 개의 정수를 더해서 세 번째 정수를 만들 수 있으면 true를 반환하는 코드를 작성합니다. 
메서드 본문은 단 한 줄의 코드로 작성되어야 합니다.

public static boolean twoSumOne(int a, int b, int c) {

}
```

### 문제 풀이
```java
public static boolean twoSumOne(int a, int b, int c) {
  return (a + b == c) || (b + c == a) || (a + c == b);
}
```
- 두 정수를 합했을 때 나머지 정수 하나 나오는 조건 작성
    - a + b == c / a + c == b / b + c == a ⇒ 이 조건들을 만족하여야 함

---
**<코드실행>**
```java
System.out.println(twoSumOne(10, 8, 2));
```



## 4번
```
세 개의 정수 first, second, third가 주어졌을 때, 
second가 first보다 크고 third가 second보다 크면 true를 반환하는 코드를 작성하세요. 
단, 마지막 opt 파라미터가 true인 경우에는 second가 first보다 크지 않아도 되지만, 
여전히 third보다는 작아야 합니다.
```

### 문제 풀이
```java
public static boolean isOrdered(int first, int second, int third, boolean opt) {
  if (!opt) {
    return (first < second) && (second < third);
  }
  return (second < third);
}
```
- opt 파라미터가 거짓이면
    - second가 first보다 크고 third가 second보다 클 때 true를 반환
- opt 파라미터가 참이면
    - second < third 일 때 true를 반환

---
**<코드실행>**
```java
System.out.println(isOrdered(3, 2, 3, false));
```



## 5번
```
어떤 숫자가 11의 배수이거나 11의 배수보다 1 큰 숫자라면, 그 숫자를 "cool"하다고 하겠습니다. 
주어진 0 이상의 숫자가 cool하다면 true를 반환하세요.
```

### 문제 풀이
```java
public static boolean isCool(int num) {
  if (num >= 0) {
    return (num % 11 == 0) || (num % 11 == 1);
  }
  return false;
}
```
- 0 이상의 정수
- 11의 배수, 11의 배수보다 1 정도 큼
    - 11로 나누었을 때 나머지가 0이거나 1인 정수 가려내기

---
**<코드실행>**
```java
System.out.println(isCool(22));
System.out.println(isCool(23));
System.out.println(isCool(24));
```



## 6번
```
정수 n이 주어졌을 때, 숫자를 문자열 형태로 변환하고 뒤에 "!"를 붙여 반환하세요. 
예를 들어, 정수가 13인 경우 이 메서드는 "13!"을 반환해야 합니다. 
하지만, 숫자가 3으로 나누어 떨어지면 숫자 대신 "새콤!"를 반환하고, 
5로 나누어 떨어지면 "달콤!"를 반환하며, 3과 5 모두로 나누어 떨어지면 
"새콤달콤!"를 반환해야 합니다.

secomDalcom(1)   ---> "1!" 
secomDalcom(2)   ---> "2!"
secomDalcom(3)   ---> "새콤!"
```

### 문제 풀이
```java
static String secomDalcom(int n) {

  boolean secom = n % 3 == 0;
  boolean dalcom = n % 5 == 0;

  if (secom && dalcom) return "새콤달콤!";
  if (secom) return "새콤!";
  if (dalcom) return "달콤!";

  return n + "!";
}
```
- 3으로 나누어 떨어지는 상태를 `secom` , 5로 나누어 떨어지는 상태를 `dalcom` 으로 선언
- secom과 dalcom을 동시에 만족하면 “새콤달콤!” 반환
    - if (secom && dalcom) return "새콤달콤!";
- secom 만족 ⇒ “새콤!”
    - if (secom) return "새콤!";
- dalcom 만족 ⇒ “달콤!”
    - if (dalcom) return "달콤!";
- 이외의 정수 ⇒ “정수!”
    - return n + "!";
    - 숫자랑 문자랑 결합할 때 문자로 자동 형변환 됨

---
**<코드실행>**
```java
System.out.println(secomDalcom(15));
System.out.println(secomDalcom(3));
System.out.println(secomDalcom(5));
System.out.println(secomDalcom(2));
```



## 7번
```
3개의 정수 인자 a, b, c가 주어졌을 때, 이들의 합을 반환하세요. 
하지만, 인자 중 하나가 다른 인자와 동일하면, 그 숫자는 합산에서 제외합니다. 
기본적으로 중복되지 않는 숫자만 합산합니다.

System.out.println(sumUnique(1, 2, 3)); // 6
System.out.println(sumUnique(3, 2, 3)); // 2
System.out.println(sumUnique(3, 3, 3)); // 0
```

### 문제 풀이
```java
public static int sumUnique(int a, int b, int c) {

  if (a == b && b == c) return 0;

  if (a == b) return c;
  if (b == c) return a;
  if (a == c) return b;

  return a + b + c;
}
```
- 정수 모두 일치할 때 0 반환
    - if (a == b && b == c) return 0;
- 정수 두 개만 일치할 때, 나머지 하나만 반환
    - if (a == b) return c;
    - if (b == c) return a;
    - if (a == c) return b;
- 그 외의 경우 세 정수의 합 반환
    - return a + b + c;

---
**<코드실행>**
```java
System.out.println(sumUnique(3,3,3));
System.out.println(sumUnique(1,2,3));
System.out.println(sumUnique(3,2,3));
```



## 8번
```
주어진 문자열에서 각 문자마다 동일한 문자를 한 번 더 추가한 문자열을 반환하세요.

System.out.println(repeatChar("The")); // "TThhee"
System.out.println(repeatChar("AAbb")); // "AAAAbbbb"
System.out.println(repeatChar("Hi-There")); // "HHii--TThheerree"
```

### 문제 풀이
```java
public static String repeatChar(String str) {
  int i = 0;
  String result = "";

  while (i < str.length()) {
    String character = String.valueOf(str.charAt(i));
    result += character + character;
    i++;
  }

  return result;
}
```
- 변수 초기화
    - int i = 0;
    - String result = "";
- 반복문을 이용해 문자열에서 한 글자씩 불러오기
    - 문자열 길이만큼 반복
    - 한 글자씩 불러올 때 str.charAt(i) 사용
    - char 타입을 String 타입으로 형변환 (`String,valueOf(변환할거)`)
    - 문자열 중복시켜 result에 축적 (`result += character + character;`)
- result 반환

---
**<코드실행>**
```java
System.out.println(repeatChar("The"));
System.out.println(repeatChar("AAbb"));
System.out.println(repeatChar("Hi-There"));
```



## 9번
```
주어진 문자열에서 모든 별표(*)와 별표 바로 왼쪽 및 오른쪽에 있는 문자를 제거한 버전을 반환하세요. 
예를 들어, "abcd"는 "ad"를 반환하고, "ab**cd"도 "ad"를 반환합니다.

System.out.println(starSideDel("cd*zq")); // "cq"
System.out.println(starSideDel("ab**cd")); // "ad"
System.out.println(starSideDel("wacy*xko")); // "wacko"
```

### 문제 풀이
```java
public static String starSideDel(String str) {
  String result ="";
  for(int i = 0; i < str.length(); i++) {
    // 현재 문자가 *일 때
    if (str.charAt(i)=='*'){
      continue;
    }

    // 현재 문자가 *이 아닐 때
    // 현재 인덱스 앞의 값이 *이 아니거나 현재 인덱스 뒤의 값이 *이 아닐 때 result에 값을 추가 해준다
    if ((i == 0 || str.charAt(i-1) != '*') && ( i == str.length()-1 || str.charAt(i+1) != '*')){
      result += String.valueOf(str.charAt(i));
    }
  }

  return result;
}
```
- 문자열에서 한 글자씩 불러오기
- 불러온 글자가 *일 때 ⇒ 바로 제끼기
    - 무시하고 다음 반복으로 넘어감 (continue)
- 불러온 글자가 *이 아닐 때 ⇒ *의 앞뒤 값 제끼기
    - i가 맨 앞이거나 불러온 글자 앞의 값이 *가 아닐 때: result에 값 추가
    - i가 맨 뒤거나 불러온 글자 뒤의 값이 *가 아닐 때: result에 값 추가
- result 반환

---
**<코드실행>**
```java
System.out.println(starSideDel("ab*c*d"));
System.out.println(starSideDel("ab**cd"));
System.out.println(starSideDel("a*bc*d"));
```