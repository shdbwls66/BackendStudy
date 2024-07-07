# 부모 생성자 - `super`
자바에서 객체를 생성할 때 `new`를 통해 생성자를 호출함

자식 객체를 메인 메서드에 생성하기 위해 자식 생성자를 호출 해야하며, 상속 관계에 있는 부모 객체도 마찬가지임

이전 페이지에서 자식 객체 생성 후 해당 객체의 변수와 메서드를 이용할 때, 부모 객체를 생성하는 코드는 따로 작성하지 않았는데 어떻게 된거냐!! 하면..


## 부모 생성자 호출 과정

자바 컴파일러에서는 생성자를 따로 선언하지 않았을 때 자체적으로 기본 생성자를 생성함

```java
public Dog {
	super();
}
```

이전 페이지의 코드의 경우도 마찬가지

부모자식 모두 생성자를 따로 선언하지 않은 상태에서, 자식 객체만 불러왔을 때 밑의 코드처럼 기본 생성자를 생성 하였을 것임

```java
public InheritB {
	super(); // 부모 생성자 호출 담당
}
```

여기서 맨 첫 줄에 있는 `super();` 가 부모의 기본 생성자 호출을 담당함

`super();` 키워드는 자식 클래스 호출 후 바로 부모의 기본 생성자 호출 시키는 모습을 명시적으로 나타냄


## super() 키워드 활용

부모 클래스에 **파라미터가 포함된 생성자**가 있다면

**반드시 자식 생성자에서 super()를 통해 부모 생성자 호출을 하여야 함** (이 때 부모 생성자와의 파라미터 타입도 맞아야 함)

또한 `super()`문은 자식 생성자에서 가장 먼저 선언되어야 함

- **부모클래스 Animal**

  부모 생성자 선언할 때 파라미터 name, gender 추가

  ```java
  public class Animal {
    String name;
    String gender;
    
    public Animal(String name, String gender) {
      this.name = name;
      this.gender = gender;
    }

    public void setName(String name) {
      this.name = name;
    }

    public void sleep() {
      System.out.println(this.name + "Zzzzzz..");
    }
  }
  ```

- **자식클래스 Dog**

  `super()` 로 부모 생성자를 호출
  
  이 때 파라미터로 설정한 name과 gender에 각각 알맞은 인자값을 넣기

  ```java
  public class Dog extends Animal {
    int age;

    public Dog(int age){
    super("뽀삐", "남"); // new Animal();
    this.age = 6;
  }

    void sleep(int times) {
      System.out.println(name + "zzzz..." + times + " hours");
    }
    
  }
  ```

- **코드 실행**

  new로 자식 생성자 호출 후 변수와 메서드 실행
  
  부모로부터 변수와 메서드를 상속 받은 모습을 볼 수 있음

  ```java
  public class Test {
    public static void main(String[] args) {
      Dog dog = new Dog(12);

      System.out.println(dog.name); // 뽀삐 출력
      
      dog.setName("용팔이"); 
      System.out.println(dog.name); // 용팔이 출력
      
      dog.sleep(100); // 용팔이zzzz...100 hours 출력

    }
    
  }
  ```

  ```
  실행 결과
  뽀삐
  용팔이
  용팔이zzzz...100 hours
  ```