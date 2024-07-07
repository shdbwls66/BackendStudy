# final과 static final

## final

final 필드를 이용해 초기값을 지정하면 그 값이 최종적인 값이 되면서 수정 불가능

초기값은 **필드 선언할 때** 혹은 **생성자에서 초기화할 때** 줄 수 있음

### final 필드의 이용

필드 선언할 때 초기값을 주었을 때, 생성자에서 초기화 X

```java
public class Human {
	final String name = "인간";
	int age;
	
	public Human(String name, int age) {
		// this.name = name; 에러 발생
		this.age = age;
	}
	
  public void sayHello() {
    System.out.println("Hello my name is " + this.name);
  }
	
  public void introduce() {
  // this로 현재 객체 메서드, 멤버 변수를 불러옴
    this.sayHello();
    System.out.println("I am " + this.age + " years old.");
  }

}
```

**main 메서드**

final 이 적용된 name은 인스턴스 생성 때 값을 넣어도 반영 X

반면, final이 적용되지 않은 age는 각 인스턴스에 따른 값이 반영된 것을 볼 수 있음

```java
public class MainHuman {

  public static void main(String[] args) {
    Human human1 = new Human("유진", 25);
    Human human2 = new Human("인간", 22);

    human1.introduce(); // Hello my name is 인간 I am 25 years old. 출력
    human2.introduce(); // Hello my name is 인간 I am 22 years old. 출력
    
  }
}
```

이렇게 `final`로 선언만 하고

```java
public class Human {
	final String name;
	int age;
	
	public Human(String name, int age) {
		this.name = name;
		this.age = age;
	}
	
	...(생략)...

}
```

이 코드를 실행 시키면..

각 인스턴스의 생성, 초기화 과정에서 정해진 name 값이 그대로 유지

```java
public class MainHuman {

  public static void main(String[] args) {
    Human human1 = new Human("유진", 25);
    Human human2 = new Human("yu", 22);

    human1.introduce(); // Hello my name is 유진 I am 25 years old. 출력
    human2.introduce(); // Hello my name is yu I am 22 years old. 출력
    
  }
}
```



## static final (상수)

상수는 객체마다 저장되지 않고 클래스에만 포함

한 번 초기값이 저장되면 변경 불가능하며 생성자 에서의 초기화도 불가능

상수 선언 시, 상수 이름은 모두 대문자로 작성하고(컨벤션) 다른 단어가 혼합되면 언더바로 단어들을 연결

```java
public class Human {

	static final int BIRTH_YEAR = 2000;
	static final String NATION = "Korea";
	static final boolean SURVIVE = true;
	
	// 정적 블록에서 초기화도 가능
	static final String GENDER;
	static {
	  GENDER = "Female";
	}

}
```

상수 사용 할 때 별도의 인스턴스를 생성할 필요 없이 클래스로 상수를 가져옴

```java
System.out.println(Human.GENDER); // Female 출력
System.out.println(Human.BIRTH_YEAR); // 2000 출력
System.out.println(Human.NATION); // Korea 출력
System.out.println(Human.SURVIVE); // true 출력
```