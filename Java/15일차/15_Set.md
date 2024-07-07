# Set
List 컬렉션과 다르게 Set 컬렉션은 저장 순서가 유지되지 않음

객체를 중복 저장할 수 없음

저장 순서가 유지되지 않아 인덱싱 X

## Set 인터페이스의 메서드

- `boolean add(E e)`: 주어진 객체 저장, 성공적으로 저장되면 true 리턴하고 중복 객체면 false 리턴

- `boolean contains(Object o)`: 주어진 객체가 저장되어 있는지 여부
- `isEmpty()`: 컬렉션이 비어있는지 조사
- `Iterator<E> iterator()`: 저장된 객체를 한 번씩 가져오는 반복자 리턴
- `int size()`: 저장되어 있는 전체 객체 수 리턴

- `void clear()`: 저장된 모든 객체 삭제
- `boolean remove(Object o)`: 주어진 객체 삭제


### Iterator 인터페이스의 메서드

- `hasNext()`: 가져올 객체가 있으면 true 리턴, 없으면 false 리턴
- `next()`: 컬렉션에서 하나의 객체를 가져옴
- `remove()`: Set 컬렉션에서 객체 제거

```java
Set<String> set = ...;

Iterator<String> iterator = set.iterator();
while (iterator.hasNext()) { // 저장된 객체 수 만큼 반복함
	String str = iterator.next(); // 객체 하나씩 가져옴
}
```

향상된 for문으로 전체 객체를 대상으로 반복 가능

```java
Set<String> set = ...;
for(String str : set) {

}
```

Set 컬렉션에서 Iterator의 next() 메서드로 가져온 객체를 제거하려면 remove() 메서드 사용

```java
Set<String> set = ...;
Iterator<String> iterator = set.iterator();
while (iterator.hasNext()) { // 저장된 객체 수만큼 반복
	iterator.remove(); // 삭제
}
```

## HashSet

Set 인터페이스의 구현 클래스

HashSet 생성은 기본 생성자 호출하면 됨

```java
Set<E> set = new HashSet<>();
```

Set 컬렉션이므로 HashSet 역시 객체들을 순서 없이 저장하고 중복 저장 불가능함

동일한 객체를 판별하기 위해서 객체 저장하기 전에 객체의 hashCode() 메서드를 호출해 해시코드를 얻어냄

얻은 해시코드와 이미 저장되어있는 객체들의 해시코드와 비교해 동일한 해시코드가 나오면 다시 equals() 메서드로 두 객체를 비교

여기서 true가 나오면 동일한 객체로 판별하여 저장 X

### HashSet에 객체를 추가, 검색, 제거해보자

```java
// HashSet 생성
Set<Integer> integerSet = new HashSet<>();

// 객체 추가
integerSet.add(1);
integerSet.add(2);
integerSet.add(3);
integerSet.add(4);
integerSet.add(5);

// 검색을 위한 반복자 얻기
Iterator<Integer> iterator = integerSet.iterator();

// 저장되어있는 객체 출력
while(iterator.hasNext()){
  System.out.println(iterator.next());
}

System.out.println("===================");

// 저장된 객체 수 출력
System.out.println(integerSet.size());

System.out.println("===================");

// 객체 삭제
integerSet.remove(2); // 삭제
iterator = integerSet.iterator(); // iterator 다시 선언하기!!

while(iterator.hasNext()){
  System.out.println(iterator.next());
}
```

```
실행 결과

1
2
3
4
5
===================
5
===================
1
3
4
5
```

```java
Set<String> stringSet = new HashSet<>();

stringSet.add("Java");
stringSet.add("Spring");
stringSet.add("JSP");
stringSet.add("Java"); // 중복되어 저장X
stringSet.add("DBMS");

System.out.println(stringSet.size()); // 4 출력

System.out.println("==================");

Iterator<String> iterator = stringSet.iterator();
while(iterator.hasNext()){
  System.out.println(iterator.next());
}

System.out.println("==================");

stringSet.remove("Java"); // 자바 제거

iterator = stringSet.iterator();
while(iterator.hasNext()){
  System.out.println(iterator.next());
}

System.out.println("==================");

if (stringSet.isEmpty()){
  System.out.println("비었습니다.");
}else{
  System.out.println("비지 않았습니다.");
}
```

```
4
==================
Java
JSP
DBMS
Spring
==================
JSP
DBMS
Spring
==================
비지 않았습니다.
```

데이터 내용은 같지만 인스턴스가 달라 객체 둘 다 저장

```java
Set<Member> set = new HashSet<>();

set.add(new Member("홍길동", 30));
set.add(new Member("홍길동", 30));

System.out.println("총 객체 수 : " + set.size());
```

이 때 중복처리 하도록 만들기 위해서는 Member 클래스에서 hashCode()와 equals() 메서드 오버라이딩 하여 데이터 값이 동일할 때 동일한 객체로 간주하도록 함

```java
public class Member {
  private String name;
  private int age;

  public Member(String name, int age) {
    this.name = name;
    this.age = age;
  }

  @Override
  public boolean equals(Object o) {
    if (o instanceof Member) {
      Member member = (Member) o;
      return member.name.equals(this.name) && member.age == this.age;
    } else {
      return false;
    }
  }

  @Override
  public int hashCode() {
    int i = name.hashCode();
    System.out.println(i);
    return i;
  }
}
```

name 값의 hashCode를 반환하도록 오버라이딩

매개값이 Member 객체의 인스턴스면 매개값을 Member 타입으로 형변환 후 저장되어있는 데이터와 이름이 같고, 나이도 같을 때 true 반환하도록 오버라이딩

```
실행 결과

54150062
54150062
총 객체 수 : 1
```