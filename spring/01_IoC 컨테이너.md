# IoC 컨테이너
## IoC 컨테이너

IoC(Inversion of Control): 제어의 역전

객체를 생성하고 관리하는 역할 수행

개발자가 IoC 컨테이너에게 필요한 객체를 요청하면, 컨테이너 쪽에서 해당 객체를 만들어 제공

객체를 다루는 행위를 개발자가 아닌 컨테이너가 직접 수행하는 것을 보고 제어가 역전되었다고 함

### 장점

- 느슨한 결합도: 객체 간의 의존성을 줄여주기 때문에 코드 수정이 용이하고 테스트하기 쉬운 코드를 작성할 수 있음
- 코드 재사용성 증가: 같은 객체를 여러 곳에서 쉽게 사용할 수 있음
- 개발 생산성 향상: 객체 관리를 컨테이너에게 맡겨 개발자는 비즈니스 로직에 더 집중할 수 있음


### 단점

- 사용하기 위해 스프링의 방대한 개념을 이해해야 하므로 어려움
- 런타임 오버헤드가 발생할 가능성이 있음


### IoC 컨테이너 구현

일반 자바 코드와의 차이점은 객체 생성에 있음

일반 자바 코드는 new 키워드를 사용하여 객체를 생성하지만 IoC 컨테이너는 어노테이션을 달아서 Bean을 정의하면 됨 (new 필요 X)



## Spring Bean
IoC 컨테이너에 의해 관리되는 객체

Java 객체와 Bean의 차이점은

- 생성 주체: 일반 객체는 개발자가 new 키워드로 생성하지만 Bean은 Spring IoC 컨테이너가 생성
- 관리 주체: 일반 객체는 개발자가 관리, Bean은 Spring IoC 컨테이너가 생성, 의존성 주입, 소멸 등의 생명 주기 관리
- 의존성 주입: 일반 객체는 의존 객체를 직접 생성하거나 찾아야 하나 Bean은 컨테이너가 의존성을 줌

### 특징

- 객체 생성과 관리: IoC 컨테이너에 의해 관리됨
- 싱글턴 패턴: Bean은 기본적으로 Singleton 패턴으로 생성되므로 단 하나의 인스턴스만 존재
- 의존성 주입: 생성자, Setter 메서드, field 주입 등을 통해 다른 Bean을 주입 받을 수 있음

Bean의 정의는 어노테이션을 통해 이루어짐

```java
@Service
public class UserService {
	private UserRepositoryInterface userRepository;
	
	public UserService(UserRepositoryInterface userRepository){
		this.UserRepository = useRepository;
	}
	
	public void createUser(User user) {
		userRepository.save(user);
	}
}
```

```java
@SpringBootApplication
public class SpringStudyApplication {
  public static void main(String[] args) {
  
    SpringApplication.run(SpringStudyApplication.class, args);
  }

}
```

```java
@Repository
public class UserRepository implements UserRepositoryInterface {
	@Override
	public void save(User user){
		
	}
}
```

![image](https://github.com/shdbwls66/springStudy/assets/168792230/e73ebe1e-4725-40a4-93a0-adeed73defe0)


userService 생성자 위에 @Autowired 달면 의존성 주입이 일어남

인터페이스를 통해 서비스와 레포지토리가 연결되어 해당 클래스는 서로를 인식하지 못한 상태

그러다가 @Autowired를 통해 의존성 주입 되면 서로를 인식하게 되므로 두 클래스에 대한 의존성이 생기는 것

![image](https://github.com/shdbwls66/springStudy/assets/168792230/8853eff3-01f9-4ead-8abd-e95e3a3ea0df)


<hr>

## 참고

```
스프링에서 변수 이름 인식해 의존 관계를 바꿀 수 있음

userService와 userRepository가 인터페이스를 통해 종속 관계를 형성하고 있는데..

userRepository 클래스를 복사하여 userRepository2 클래스 생성 후

userService 클래스의 생성자 함수에서 userRepository를 userRepository2로 바꾸면

userService가 userRepository2를 바라보게 됨
```
