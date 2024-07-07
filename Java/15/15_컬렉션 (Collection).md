# 컬렉션(Collection)

요소를 수집해서 저장하는 것

여러 객체를 저장하고 필요할 때마다 꺼낼 때 아래의 코드 처럼 배열을 이용할 수 있음

```java
// 배열 생성
Product[] products = new Product[5];

// 객체 저장
products[0] = new Product("상품 1");
products[1] = new Product("상품 2");
products[2] = new Product("상품 3");

// 객체 가져오기
System.out.println(products[0]);
System.out.println(products[0]);
System.out.println(products[0]);

// 객체 삭제
products[0] = null;
products[1] = null;
products[2] = null;
```

하지만 배열은 객체를 삭제 하였을 때 인덱스에 저장된 값이 듬성듬성 존재하게 됨

따라서 만약 새로운 객체를 추가한다고 하면 인덱스 값의 존재를 확인하는 과정을 따로 거쳐야 함

이러한 점을 개선하기 위해 자바에 컬렉션과 관련된 인터페이스와 클래스들이 나왔고 이들을 **컬렉션**이라고 함

## 주요 컬렉션 인터페이스

### List 인터페이스
  - 구현 클래스로 ArrayList, LinkedList 등 있음
  - 자료 순서를 유지하고 저장하며 중복 저장 가능
### Set 인터페이스
  - 구현 클래스로 HashSet 등 있음
  - 자료 순서를 유지하지 않고 저장하며 중복 저장 불가
### Map 인터페이스
  - 구현 클래스로 HashMap, Hashtable 등 있음
  - 키와 값의 쌍으로 저장하며 키는 중복 저장 불가