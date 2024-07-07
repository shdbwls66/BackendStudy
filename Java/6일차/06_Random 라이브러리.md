# Random 라이브러리
## 자바 라이브러리

미리 작성된 코드의 모음으로 개발자가 특정 기능을 쉽게 구현할 수 있도록 돕는 역할을 함

**클래스, 인터페이스, 메서드** 등으로 구성

라이브러리 사용하려면 import 문을 통해 해당 라이브러리를 불러와야 함


## random 라이브러리

`java.util` 패키지에 포함되어 있음

`Random` 클래스의 인스턴스를 생성하여 사용 가능


### 난수를 생성하는 여러 메서드

`nextInt()`: int 타입의 난수 생성

`nextInt(int bound)`: 0부터 bound 미만의 난수 생성

`nextLong()`: long 타입의 난수 생성

`nextFloat()`: float 타입의 난수 생성

`nextDouble()`: double 타입의 난수 생성

`nextBoolean()`: boolean 타입의 난수 생성


### 문제 1
로또 번호 생성기 프로그램을 작성하세요. 이 프로그램은 1부터 45까지의 숫자 중 중복되지 않는 6개의 숫자를 무작위로 선택하여 출력합니다.

- random 객체 생성

- `ArrayList`를 사용하여 정수형만 추가할 수 있는 리스트 만들기 (`ArrayList`는 요소 추가하거나 빼기 가능)

- while문을 이용해 `list.size()`가 6이 될 때까지 값 추가

- `random.nextInt(45) + 1`을 통해 랜덤 값 생성

- list 내부 값의 존재는 `list.contains`로, 값 추가는 `list.add(num)`로 하기

```java
Random random = new Random();

// 정수형만 추가할 수 있게 리스트 만들기, 요소 추가, 빼기 가능
ArrayList<Integer> list = new ArrayList<Integer>();

// 리스트 사이즈가 6이 되기 전까지 값 추가
while (list.size() != 6) {
  int num = random.nextInt(45) + 1;

  // list에 값이 없으면 추가
  if (!list.contains(num)) {
    list.add(num);
  }
}

for (int data : list) {
  System.out.println("[" + data + "]");
}
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/47ae6059-a86a-438f-afbc-b8592fea2114)


### 문제 2
숫자 맞추기 게임

random 객체 생성

- `random.nextInt(100) + 1;`을 이용해 1부터 100 사이의 난수 생성

- scanner 객체 생성

- while문을 작성하여 계속 숫자를 입력 받다가

- if문으로 입력 숫자와 랜덤 숫자가 다르면 랜덤 숫자가 입력 숫자보다 큰지 작은지 알려주고, 같으면 반복문을 중단하는 조건 추가

```java
Random random = new Random();

int randomNum = random.nextInt(100) + 1;

Scanner scanner = new Scanner(System.in);

while(true) {
  System.out.println("숫자를 입력하세요");
  int num = scanner.nextInt();

  if (num > randomNum) {
    System.out.println("입력한 숫자보다 낮습니다");
  } else if (num < randomNum){
    System.out.println("입력한 숫자보다 높습니다");
  } else {
    System.out.println("정답입니다");
    break;
  }
}

scanner.close();
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/476cffad-85ad-41b8-b4f5-8f2d7da1aab4)