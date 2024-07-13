# JPA 매핑
JPA에서는 어노테이션을 이용해 객체와 테이블을 매핑함

매핑 어노테이션을 분류하면

- 객체와 테이블 매핑: `@Entity`, `@Table`
- 기본 키 매핑: `@Id`
- 필드와 컬럼 매핑: `@Column`
- 연관 관계 매핑: `@ManyToOne`, `@JoinColumn`


매핑 어노테이션을 작성하면 JPA에서 데이터베이스 스키마를 자동으로 생성함

## 객체와 테이블 매핑

JPA를 통해 클래스와 테이블과 매핑하기 위해서는 @Entity 어노테이션을 붙여야 함

해당 어노테이션 달린 클래스는 JPA에서 관리하는 테이블이 되며, 데이터베이스 스키마를 자동 생성

### `@Entity`

속성: name

기능: JPA에서 사용할 엔티티 이름 지정, 클래스 이름이 기본값

### `@Table`

엔티티와 매핑할 테이블 지정

속성: name

기능: 매핑할 테이블 이름, 엔티티 이름이 기본값

Member 엔티티와 member 테이블 매핑

```java
import jakarta.persistence.*;
import lombok.AllArgsConstructor;
import lombok.Getter;
import lombok.NoArgsConstructor;

@Getter
@NoArgsConstructor
@AllArgsConstructor
@Entity
@Table(name = "member")
public class Member {
    @Id
    @Column(name = "id")
    private Long id;

    @Column(name = "name")
    private String userName;

    @Column(name = "age")
    private Integer age;
}
```

## 기본 키 매핑

@Id 어노테이션으로 지정

기본 키 매핑 방법은 크게 두 가지로 나눌 수 있는데

- 직접 할당: 기본키를 애플리케이션에서 직접 할당
- 자동 생성: 대리 키 사용 방식
    - IDENTITY: 기본 키 생성을 데이터베이스에 위임
    - SEQUENCE: 데이터베이스의 시퀀스를 사용해 기본키 할당
    - TABLE: 키 생성 테이블 사용

기본 키 직접 생성

```java
@Entity
public class Member {

		@Id
		@Column(name = "id")
		private Long id;
		
		(중략)
}
```

IDENTITY 전략

```java
@Entity
public class Member {

		@Id
		// 기본 키 생성을 DB에 위임
		@GeneratedValue(strategy = GenerationType.IDENTITY)
		@Column(name = "id")
		private Long id;
		
		(중략)
}
```

### 식별자 선택

기본 키 조건

- null이 아닌 값
- 중복되지 않는 유일한 값
- 변하면 안되는 값

이를 만족하는 식별자 선택 방법으로 총 두 가지가 있음

- 자연 키 전략
    - 비즈니스에 의미가 있는 키 선택
    - ex) 이메일, 전화번호, 주민등록번호 등

- 대리 키 전략
    - 비즈니스와 관련 없는 임의로 만들어진 키 선택
    - ex)  auto_increment, 키생성 테이블, 오라클 시퀀스
    - 외부 요인에 영향 받지 않아 권장되는 방법

Member 테이블 생성, 데이터를 삽입 한 후 조회

```java
// 테스트 파일에서 실행
@SpringBootTest
class MemberServiceTest {
    @Autowired
    private MemberService memberService;

    @Test
    public void insertMember() {
        Member member = new Member("김땡떙", 25);
        memberService.insertMember(member);
    }
}
```

![image](https://github.com/shdbwls66/BackendStudy/assets/168792230/b2535970-61ba-47f7-97c5-000187368a01)

![image](https://github.com/shdbwls66/BackendStudy/assets/168792230/71254b2e-1afa-494d-a447-7552c07065fd)

id가 자동 생성된 것을 볼 수 있음

![image](https://github.com/shdbwls66/BackendStudy/assets/168792230/0870115c-e71e-435b-be3a-9f263023c089)

## 필드, 컬럼 매핑

필드와 컬럼 매핑하는 어노테이션

- `@Column`: 컬럼 매핑
- `@Enumerated`: 자바의 enum 타입 매핑
- `@Temporal`: 날짜 타입 매핑

### `@Column`

객체 필드를 테이블 컬럼에 매핑

속성 중에 name, nullable이 주로 사용

`@Column` 속성

name: 필드와 매핑할 컬럼명, 필드 이름이 기본값

nullbale: null 허용 여부, true가 기본값

unique: 유일한 값 여부, false가 기본값

columnDefinition: 컬럼 정보 설정, default 값 줄 수 있음

```java
@Entity
public class Member {

		@Id
		@Column(name = "id")
		private Long id;
		
		@Column(name = "name", nullable = false
		private String name;
		
		(중략)
}
```

### `@Enumerated`

자바 enum 타입의 상수값을 테이블 컬럼에 매핑

- EnumType.STRING: enum 이름 그대로 ADMIN은 ‘ADMIN’, USER는 ‘USER’ 라는 문자로 데이터베이스에 저장
- EnumType.ORDINAL: enum에 정의된 순서대로 ADMIN은 0, USER은 1 값이 데이터베이스에 저장

```java
import lombok.NoArgsConstructor;

@NoArgsConstructor
public enum RoleType {
    ADMIN, USER
}
```

```java
import jakarta.persistence.*;
import lombok.AllArgsConstructor;
import lombok.Getter;
import lombok.NoArgsConstructor;

import java.util.Date;

@Getter
@NoArgsConstructor
@AllArgsConstructor
@Entity
@Table(name = "member")
public class Member {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    @Column(name = "name")
    private String userName;

    @Column(name = "age")
    private Integer age;

    @Enumerated(EnumType.STRING)
    private RoleType roleType;
}
```

테이블을 생성하여 데이터 삽입 해보면 enum 타입 상수값이 그대로 나오는 것을 볼 수 있음

![image](https://github.com/shdbwls66/BackendStudy/assets/168792230/88d91854-ec47-4712-a3bf-79ff71fe43cd)

### `@Temporal`

날짜 타입을 매핑할 때 사용

- TemporalType.DATE: 날짜, 데이터베이스 date 타입과 매핑
- TemporalType.TIME: 시간, 데이터베이스 time 타입과 매핑
- TemporalType.TIMESTAMP: 날짜와 시간, 데이터베이스와 timestamp 타입과 매핑

timestamp 타입과 매핑

```java
import jakarta.persistence.*;
import lombok.AllArgsConstructor;
import lombok.Getter;
import lombok.NoArgsConstructor;

import java.util.Date;

@Getter
@NoArgsConstructor
@AllArgsConstructor
@Entity
@Table(name = "member")
public class Member {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    @Column(name = "name")
    private String userName;

    @Column(name = "age")
    private Integer age;

    @Enumerated(EnumType.STRING)
    private RoleType roleType;

    @Temporal(TemporalType.TIMESTAMP)
    private Date createAt;
}
```

![image](https://github.com/shdbwls66/BackendStudy/assets/168792230/df9939b5-047b-484e-ab57-5f989c9120d4)

## 실습

Students 테이블 생성, 데이터 삽입해보기

```java
import jakarta.persistence.*;
import lombok.AllArgsConstructor;
import lombok.Getter;
import lombok.NoArgsConstructor;

@Getter
@NoArgsConstructor
@AllArgsConstructor
@Entity
public class Students {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "student_id")
    private Long id;

    @Column
    private String name;

    @Column
    private int age;

    @Column
    private String address;

    public Students(String name, int age, String address) {
        this.name = name;
        this.age = age;
        this.address = address;
    }

}
```

테이블 생성

![image](https://github.com/shdbwls66/BackendStudy/assets/168792230/00f6dea7-5dd8-4ecc-891b-f76c1970ac6a)

insert문 실행

![image](https://github.com/shdbwls66/BackendStudy/assets/168792230/599d4b3a-2669-4acc-afbd-f4432f961e53)

students 테이블 조회

![image](https://github.com/shdbwls66/BackendStudy/assets/168792230/3fde980e-16f8-4c70-8bcc-c29e13a817a0)
