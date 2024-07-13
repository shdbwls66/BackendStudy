# MVC (Model-View-Controller) 패턴
웹 애플리케이션 개발에 널리 사용되는 아키텍처 패턴

Model, View, Controller의 컴포넌트로 나누어 애플리케이션을 개발하는 방식

각 M, V, C를 레이어 계층 이라고 부름

## MVC 패턴 실습

### Model 계층

- 사용자의 데이터를 보관하는 곳

- 비즈니스 로직과 데이터 표현 담당

- 데이터 상태 관리, 조작

User 클래스

- 사용자의 정보가 담겨 있음

```java
import lombok.AllArgsConstructor;
import lombok.Getter;
import lombok.Setter;

@Setter // Setter 메서드 대체
@Getter // Getter 메서드 대체
@AllArgsConstructor // 생성자 대체
public class User {
    private String email;
    private String name;
    private int age;

}
```

### View 계층

- 사용자의 요청을 처리하는 곳

- 화면에 정보 표시

- Model의 데이터를 사용해 사용자 인터페이스 나타냄

UserView 클래스

- 유저 정보 조회하는 printUserDetails() 메서드

- 사용자 입력 받아 유저 이름 설정하는 inputUserDetails() 메서드

```java
import java.util.Scanner;

public class UserView {
    public void printUserDetails(User user){
        System.out.println("User details: ");
        System.out.println("Name: " + user.getName());
        System.out.println("Email: " + user.getEmail());
    }

    public void inputUserDetails(User user){
        Scanner sc = new Scanner(System.in);

        System.out.println("Enter your name: ");

        user.setName(sc.nextLine());
        
        sc.close();
    }
}
```

### Controller 계층

- Model과 View 간의 상호작용 제어

- 데이터 업데이트 → View로 전달

- 사용자의 요청을 받는 곳

UserController 클래스

- 사용자 정보 조회하는 updateView() 메서드

- 이름 수정하는 setUserName() 메서드

- 나이 수정하는 setUserAge() 메서드

```java
import lombok.AllArgsConstructor;

@AllArgsConstructor
public class UserController {
    private User model;
    private UserView view;

    public void updateView() {
        view.printUserDetails(model);
    }

    public void setUserName(String name) {
        model.setName(name);
    }

    public void setUserAge(int age) {
        model.setAge(age);
    }
}
```

### Main

- Model, View, Controller 객체 생성

- Controller로 값 업데이트, 값 출력 (Model과 View에 접근 하지 않아도 값을 조회, 수정할 수 있음)

```java
public class MainApplication {
    public static void main(String[] args) {
        SpringApplication.run(MainApplication.class, args);

        User model = new User("max@gmail.com", "노유진", 25);
        UserView userView = new UserView();
        UserController userController = new UserController(model, userView);

        userController.updateView();
        userController.setUserName("김삿갓");
        userController.setUserAge(24);
        System.out.println("===========================");
        userController.updateView();
    }
}
```

![image](https://github.com/shdbwls66/springStudy/assets/168792230/9f7dfe17-712e-4411-90be-dcc81acf3f14)

<hr>

각 계층별로 코드를 나누어 작성하였는데

MVC 패턴을 사용하여 코드를 작성함으로써

- 코드의 재사용성이 향상되고 모듈화 구조를 유지
- 유지보수성의 향상
    - 각 계층의 역할이 명확하게 분리되어 있어 가독성과 유지보수성이 향상
    - 한 컴포넌트 변경이 다른 컴포넌트에 영향 주지 않음
- 협업, 병렬 개발이 용이
    - 각 컴포넌트를 독립적으로 개발 가능해 개발자 간 역할 분담을 확실히 할 수 있음
- 테스트 용이성
    - 각 컴포넌트 단위로 테스트 가능
- 유연성과 확장성의 향상
    - 컴포넌트 간 결합이 느슨함
    

하지만 단점도 존재하는데,

- 복잡성 증가
    - 각 컴포넌트 간 상호작용과 데이터 흐름을 관리해야 하기 때문에 초기 설계와 구현이 복잡해질 수 있음
- 개발 시간 증가
    - 컴포넌트 간 인터페이스를 정의하고 데이터 흐름을 설계하는데 시간이 소요
- 과도한 추상화
    - 과도하게 추상화 하였을 때 코드의 복잡성이 향상
    - 소규모의 프로젝트나 단순한 애플리케이션에서는 MVC 패턴의 적용이 오히려 비효율적
 
## 퀴즈

MVC 패턴을 사용하여 퀴즈 만들기!!

Model 클래스

```java
import lombok.AllArgsConstructor;
import lombok.Getter;

@AllArgsConstructor
@Getter
public class Quiz {
    private String question;
    private String answer;

}
```

View 클래스

```java
import lombok.AllArgsConstructor;

import java.util.Scanner;

@AllArgsConstructor
public class QuizView {
    public void displayQuestion(String question){
        System.out.println(question);
    }

    public String getUserAnswer(){
        Scanner sc = new Scanner(System.in);
        System.out.println("답변을 입력하세요");
        String answer = sc.nextLine();
        sc.close();

        return answer;
    }

    public void displayResult(boolean isCorrect){
        if (isCorrect) {
            System.out.println("정답입니다!");
        } else {
            System.out.println("오답입니다!");
        }
    }
}
```

Controller 클래스

```java
import lombok.AllArgsConstructor;

@AllArgsConstructor
public class QuizController {
    private Quiz quiz;
    private QuizView quizView;

    public void startQuiz(){
        quizView.displayQuestion(quiz.getQuestion());
        boolean result = quizView.getUserAnswer().equals(quiz.getAnswer());
        quizView.displayResult(result);
    }

}
```

![image](https://github.com/shdbwls66/springStudy/assets/168792230/07a61edf-e658-48e3-985f-6666d6a03426)
