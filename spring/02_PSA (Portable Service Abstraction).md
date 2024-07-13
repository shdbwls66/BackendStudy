# PSA (Portable Service Abstraction)
이동식 서비스 추상화

스프링에서 제공하는 추상화 (하위 시스템의 공통적인 부분을 뽑아내 분리하는 것)

서비스 객체를 구현할 때 특정 기술에 종속되지 않게 해줌

PSA를 사용하면 서비스 객체 코드를 수정하지 않아도 다양한 기술을 적용할 수 있어 코드의 유지 보수와 확장에 용이

## 이메일 발송 서비스

### PSA 적용 X

EmailService 클래스 생성

- 이메일을 발송하는 sendMail() 메서드 생성

```java
public class EmailService {
    public void sendMail(String to, String subject, String body){
        System.out.println("SMTP로 이메일 발송합니다");
    }
}
```

- 위 코드와 같이 서비스를 구현하였을 때 이메일을 발송할 때 사용하는 프로토콜이 바뀔 때마다 sendMail() 메서드의 내용도 같이 바꾸어 주어야 함

### PSA 적용

이메일 발송 기능을 인터페이스로 구현

```java
public interface EmailSender {
    void sendEmail(String to, String subject, String body);

}
```

인터페이스를 구현할 클래스 생성 (SmtpEmailSender 클래스, AwsSesEmailSender 클래스)

- 사용하는 프로토콜에 따라 다른 내용을 출력

```java
// SMTP 사용
public class SmtpEmailSender implements EmailSender{

    @Override
    public void sendEmail(String to, String subject, String body) {
        System.out.println("Sending SMTP email to " + to);
    }
}

// AWS, SES 사용
public class AwsSesEmailSender implements EmailSender{

    @Override
    public void sendEmail(String to, String subject, String body) {
        System.out.println("Sending AWS SES email to " + to);
    }
}
```

EmailService 클래스

- 인터페이스에 의존하고 있음

```java
@Service
public class EmailService {
    private final EmailSender emailSender;

    public EmailService(EmailSender emailSender) {
        this.emailSender = emailSender;
    }

    public void sendMail(String to, String subject, String body){
        emailSender.sendEmail(to, subject, body);
    }
}
```

PSA를 적용하였을 때 EmailService 의 코드를 수정하지 않고도 여러가지 프로토콜을 적용하여 메일 발송 서비스를 구현할 수 있게됨

따라서 PSA를 적용하면 유연성, 유지보수성, 테스트 용이성의 측면에서 유용함

하지만 추상화 계층으로 인해 코드의 복잡성이 증가할 수 있으며, 성능 오버헤드가 발생할 수 있다는 단점도 존재
