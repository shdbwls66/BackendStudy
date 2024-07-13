# DI (Dependency Injection)
객체 간의 의존성을 외부에서 주입하는 디자인 패턴

Car 클래스와 Engine 클래스가 있다고 해보자

```java
public class Car{
    private Engine engine;

    public Car() {
        this.engine = new Engine;
    }
}

public class Engine{

}
```

- 위 코드는 Engine 객체를 직접 생성하고 있음

- Car 객체를 생성하기 위해서 Engine 클래스가 필요하며, Engine의 내용이 바뀌면 Car에게 직접적으로 영향을 주기 때문에 Engine 클래스에 대한 의존도가 높다고 할 수 있음

- 즉, 강결합 상태이기 때문에 코드의 유연성과 확장성이 떨어지는 문제 발생

코드를 수정해보자

```java
public class Car{
    private Engine engine;

    public Car(Engine engine) {
        this.engine = engine;
    }
}

public class Engine{

}
```

- 위 코드는 new 키워드로 Engine 객체를 직접 생성하는 대신 외부로부터 객체를 받아오는 방식을(DI) 통해 구현되었음

- Car와 Engine 간 결합도가 앞의 코드에 비해 낮아 코드의 유연성과 확장성이 높음

## 스프링에서 DI 구현
한편 스프링에서는DI 구현할 때, 어노테이션을 이용할 수 있음

```java
// Autowired 이용할 때 Bean 정의할 것

@Component
public class Car {
	private final Engine engine;
	
	@Autowired
	public Car(Engine engine){
		this.engine = engine;
	}
}

@Component
public class Engine{

}
```

- 위 코드에서는 Car와 Engine을 `@Component` 어노테이션을 통해 Bean으로 정의하였고 `@Autowired` 어노테이션을 통해 Engine을 Car 객체에 주입

### `@Autowired`
스프링 프레임워크에서 제공하는 어노테이션이며, 의존성 주입에 사용

스프링 컨테이너에게 해당 객체의 의존성을 자동 주입

 객체 간 의존성을 컨테이너에서 자동으로 관리 해주기 때문에 개발자는 비즈니스 로직에 집중 가능

다이어그램으로 본 의존 관계
![image](https://github.com/shdbwls66/springStudy/assets/168792230/a5997bbf-c157-4876-9893-4e0ca52eb205)


### 같은 인터페이스를 구현한 Bean이 여러 개인 경우
구분자 사용을 하지 않으면

⇒ `NoUniqueBeanDefinitionException` 예외 발생

예외를 발생 시켜 보자

CarInterface 생성

```java
public interface CarInterface {
    void run();

}
```

CarInterface를 구현한 클래스, Car, Car2 생성

```java
@Component
public class Car implements CarInterface{
    @Override
    public void run() {
        System.out.println("Car가 달립니다.");
    }
}
```

```java
@Component
public class Car2 implements CarInterface {
    @Override
    public void run() {
				System.out.println("Car2가 달립니다.");
    }
}
```

Driver 클래스를 만들어 @Autowired 를 사용해보면

```java
@Component
public class Driver {
    private CarInterface carInterface;

    @Autowired
    public Driver(CarInterface carInterface) { // 에러 발생
        this.carInterface = carInterface;
    }
}
```

의존성 자동 주입 X

![image](https://github.com/shdbwls66/springStudy/assets/168792230/57f39b82-2c62-4422-89e0-593d7c6d8b81)

이 문제를 해결하기 위해 `@Primary`나 `@Qualifier`와 같은 어노테이션을 이용해 주입할 Bean을 선택할 수 있음

`@Qualifier` 어노테이션을 통해 Bean 선택

```java
@Component
public class Driver {
    private CarInterface carInterface;

    @Autowired
    public Driver(@Qualifier("car") CarInterface carInterface) {
        this.carInterface = carInterface;
    }
}
```
