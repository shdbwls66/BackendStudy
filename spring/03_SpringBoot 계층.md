# SpringBoot 계층
## Presentation Layer (표현 계층)

사용자 인터페이스와 상호작용을 담당하여, 사용자 요청을 처리하고 결과를 반환하는 계층

MVC 패턴의 C가 표현 계층임

- UI 구성 요소, 컨트롤러, 뷰 템플릿 등
- 사용자 입력 유효성 검사, 응답 생성
- 다른 계층과의 통신 담당

### UserController
- UserService에 연결
- UserService의 getUser() 메서드를 호출하고 max 유저 정보에 맵핑
- 유저 정보에 맵핑

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController // 표현 계층 역할
public class UserController {
    private final UserService userService;

    @Autowired
    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping("/user/max")
    public String getUserResult() {
        return userService.getUser();
    }

    @GetMapping("/user")
    public String getUser() {
        return "Hello";
    }

}
```

## Service Layer (서비스 계층)
비즈니스 로직 구현하는 계층으로, 표현 계층과 데이터 액세스 계층 사이의 중간 계층 역할을 수행
특징
- 트랜잭션 관리, 보안, 비즈니스 규칙 등 처리
- 도메인 모델과 밀접한 관련
- 표현 계층과 데이터 액세스 계층을 분리하여 유지보수성을 향상 시킴

### UserService
- UserRepository로부터 유저 데이터 가져오기

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service // 서비스 계층 역할
public class UserService {
		
    private final UserRepository userRepository;
		
		// 데이터 접근 계층 의존
    @Autowired
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public String getUser(){
        User user = userRepository.getUser();
        System.out.println("오오오오오징어");
        return user.getName(); // 이름(키 값) 리턴
    }
}
```

## Data Access Layer (데이터 접근 계층)
데이터 저장소와 상호작용하는 계층
특징
- 데이터 조회, 저장, 수정, 삭제 등 작업 수행
- ORM 프레임워크나 데이터 액세스 기술 활용
- 데이터 액세스 로직을 캡슐화 하여 다른 계층으로부터 분리

### UserRepository
- 맵에다 유저 정보 넣고 리턴
- 데이터베이스로부터 값 가져옴

```java
import org.springframework.stereotype.Repository;
import java.util.HashMap;
import java.util.Map;

@Repository // 데이터 접근 계층 역할
public class UserRepository {

    Map<String, User> users = new HashMap<>();

    public User getUser() {
        users.put("max", new User("max@gmail.com", "Max", 20));
        return users.get("max");
    }
}
```

### 정리
- 표현 계층 - 서비스 계층 호출,  비즈니스 로직 실행 

- 서비스 계층 - 데이터 접근 계층을 통해 데이터 조회 및 변경

- 계층 간의 의존성은 인터페이스를 통해 이루어짐

<hr>

실행하면 컨트롤러에서 맵핑한대로 나옴
localhost:8080/user/max 에는 Max 출력

![image](https://github.com/shdbwls66/springStudy/assets/168792230/b8ddac30-7737-4364-8455-b652f1c1e8ec)

localhost:8080/user 에는 Hello 출력

![image](https://github.com/shdbwls66/springStudy/assets/168792230/e6564fc2-361c-479a-b1bd-5f9232acfe03)

## Spring MVC와 세 계층

### Presentation Layer

Spring MVC 에서 컨트롤러와 뷰 템플릿이 해당 (@Controller)

- 컨트롤러: 사용자의 요청을 받아 처리하고 적절한 모델과 뷰 반환
- 뷰 템플릿: 컨트롤러에서 전달 받은 모델 데이터 사용하여 사용자 인터페이스 렌더링
- `DispatcherServlet` : 표현 계층의 중심 역할, 요청을 적절한 컨트롤러에게 전달하고 응답 처리

### Service Layer

서비스(@Service) 클래스가 해당

- 비즈니스 로직 구현, 트랜잭션 관리와 보안 등의 기능 처리
- 컨트롤러는 서비스 클래스 호출하여 필요한 비즈니스 로직 실행, 결과 받아옴
- Spring MVC 에서는 서비스 클래스를 Bean으로 등록, 컨트롤러에 주입하여 사용

### Data Access Layer

리포지토리(@Repository) 가 해당

- 데이터베이스나 외부 저장소와의 상호작용
- 데이터 조회, 저장, 수정, 삭제 등 작업 수행
- 주로 JPA, MyBatis 등 프레임워크 사용하여 리포지토리 구현
- 리포지토리 사용하여 데이터 액세스 작업 수행
