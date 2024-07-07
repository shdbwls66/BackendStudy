# `Scanner` 클래스

자바에서 사용자의 입력을 받고자 할 때 `Scanner` 클래스를 사용

`Scanner` 클래스는 `java.util` 패키지에 포함되어 있어, 사용할 때 해당 패키지를 임포트 해야 함


### 사용자로부터 정수를 입력 받기

`Scanner` 객체인 `sc` 생성

`nextInt()` 메소드를 사용하여 정수를 입력 받아 변수 a에 저장

사용 후 자원 해제를 위해 `sc.close();` 사용

```java
import java.util.Scanner;

public class day6_Test2 {
  public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);

    System.out.println("정수를 입력해주세요.");
    int a = sc.nextInt();

    System.out.println("제가 입력한 값은 " + a + " 입니다.");
    
    sc.close();
  }
}
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/180bc283-8ca0-49af-8ac6-27161dad33e1)

![image](https://github.com/shdbwls66/backendJava/assets/168792230/9080682d-e020-48ca-96a1-14160e7a469b)


### 문자열 입력 받기

문자열을 입력 받으려면 `nextLine()` 메소드 사용

```java
System.out.println("메세지를 입력하세요");
String b = sc.nextLine();

System.out.println(b + "입력");

sc.close();
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/7c5e0e24-9050-42fa-b303-dea2cb455770)


💡 **스트림**
<aside>

    사용자의 입력을 받고 무언가를 출력하는 과정
    
    이 때 값을 출력할 때 사용하는 `System.out` 을 표준 출력(output),
    
    `System.in` 을 표준 입력(input) 이라고 부름

</aside>


### 유의 사항

`nextLine()` 메서드를 `nextInt()`와 같은 다른 메서드와 함께 사용할 때 개행 문자(\n)로 인해 원하는 결과를 얻지 못할 수 있기 때문에 `nextLine()`을 한번 더 호출하여 ‘\n’을 제거해야 함

- `nextInt()` 메서드와 함께 사용할 때:

  - `Scanner`를 통해  `nextInt()`가 호출되고, 사용자는 정수를 입력, Enter 키(\n)를 누름

  - `nextInt()`가 정수만 읽어 들이고 Enter 키만 입력 버퍼에 남음

  - Enter 키는 이 후에 호출된 `nextLine()`로 인해 빈 문자열로 읽혀지면서 사용자는 문자열 입력을 못하게 됨


`Scanner` 는 입력 값의 유효성을 검사하지 않아 잘못된 타입의 데이터가 입력되면 예외(InputMismatchException)가 발생


### 문제 1
"계절을 맞춰보세요!" 라는 자바 프로그램을 작성해보세요.

- 객체 생성 후 `nextInt()`로 숫자 입력 받아 number에 저장

- number 값에 따라 계절이 출력 되도록 `swtich` 문 작성

```java
Scanner sc = new Scanner(System.in);

System.out.println("계절을 맞춰보세요!");
int number = sc.nextInt();

switch (number) {
  case 1:
    System.out.println("봄");
    break;
  case 2:
    System.out.println("여름");
    break;
  case 3:
    System.out.println("가을");
    break;
  case 4:
    System.out.println("겨울");
    break;
  default:
    System.out.println("잘못된 입력입니다!");
    break;
}

sc.close();
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/ca15954b-c941-47bd-8696-58d93f2f70d5)

![image](https://github.com/shdbwls66/backendJava/assets/168792230/2e2ece48-6022-4f60-ab0c-99cacd1968f2)


### 문제 2
영화 티켓 예매 시스템

- scanner 객체 생성 후 각 항목마다 적절한 타입으로 입력 받기

- 관람 인원 수 입력 받고 `scanner.nextLine();`로 개행 문자 처리

- 티켓 가격은 미리 변수로 정의 하고 입력 받은 값들을 모두 출력

```java
Scanner scanner = new Scanner(System.in);

System.out.println("영화 제목");
String movie = scanner.nextLine();

System.out.println("관람 인원 수");
int num = scanner.nextInt();
scanner.nextLine();

System.out.println("예매자의 이름");
String name = scanner.nextLine();

System.out.println("예매자의 전화번호");
String phone = scanner.nextLine();

int price = 10000;

System.out.println("===== 영화 티켓 예매 정보 =====");
System.out.println("영화 제목: " + movie);
System.out.println("관람 인원: " + num + "명");
System.out.println("예매자 이름: " + name);
System.out.println("예매자 전화번호: " + phone);
System.out.println("총 결제 금액: " + num * price + "원");

scanner.close();
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/b9c54945-4a8d-40f1-95b0-68c2e3fdcdf1)


### 문제 3
학생 성적 관리 시스템

- `scanner.nextInt()`으로 학생 수 입력 받음

- for문을 이용하여 학생 수 만큼 값을 넣기

- if문으로 평균 점수에 따라 등급을 부여

- 입력 받은 정보 출력 (이 때 평균은 소수점 둘째 자리까지 출력해야 하므로 `System.out.printf()` 사용)

```java
Scanner scanner = new Scanner(System.in);

System.out.println("학생 수를 입력하세요");
int student = scanner.nextInt();
scanner.nextLine();

String grade = "";

for (int i = 1; i <= student; i++) {
  System.out.println("학생 이름 입력하세요");
  String name = scanner.nextLine();

  System.out.println("국어 점수");
  int lang = scanner.nextInt();

  System.out.println("영어 점수");
  int eng = scanner.nextInt();

  System.out.println("수학 점수");
  int math = scanner.nextInt();
  scanner.nextLine();

  int score = lang + eng + math;
  double avg = (double) score / 3;

  if (avg >= 90) {
    grade = "A";
  } else if (avg >= 80) {
    grade = "B";
  } else if (avg >= 70) {
    grade = "C";
  } else if (avg >= 60) {
    grade = "D";
  } else {
    grade = "F";
  }

  System.out.println("===== 학생 성적 정보 =====");
  System.out.println("이름: " + name);
  System.out.println("국어 점수: " + lang);
  System.out.println("영어 점수: " + eng);
  System.out.println("수학 점수: " + math);
  System.out.println("총점: " + score);
  System.out.printf("평균: %.2f%n", avg);
  System.out.println("등급: " + grade);
  System.out.println("========================");
}
scanner.close();
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/0226aa30-e40b-4bfc-9bbf-3eb461ef61a2)

![image](https://github.com/shdbwls66/backendJava/assets/168792230/1f708d7c-d66c-4443-b261-0913319003d9)

![image](https://github.com/shdbwls66/backendJava/assets/168792230/ef869e7a-0eb1-4575-913c-bb83938f7ba5)