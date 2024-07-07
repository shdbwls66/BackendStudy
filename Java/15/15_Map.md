# Map
키와 값의 쌍으로 구성된 객체를 저장하며 여기서 키와 값은 모두 객체

키는 중복 X, 값은 중복 가능

기존에 저장된 키 값과 동일한 키 값으로 저장하면 기존의 키 값은 사라지고 새로운 값으로 대치

## Map 인터페이스 메서드

Key로 객체들을 관리하므로 Key 값을 매개값으로 갖는 메서드들이 많음

- `V put(K key, V value)`: 주어진 key와 value 추가, 저장되면 value를 리턴

- `boolean containsKey(Object key)`: 주어진 키가 있는지 여부
- `boolean containsValue(Object value)`: 주어진 value가 있는지 여부
- `Set(Map.Entry<K,V>> entrySet()`: 키와 값의 쌍으로 구성된 모든 Map.Entry 객체를 Set에 담아서 리턴
- `V get(Object key)`: 주어진 키가 있는 value를 리턴
- `boolean isEmpty()`: 컬렉션이 비어 있는지 여부
- `Set<K> keySet()`: 모든 키를 Set 객체에 담아 리턴
- `int size()`: 저장된 키의 총 개수 리턴
- `Collection<V> values()`: 저장된 모든 value를 Collection에 담아 리턴

- `vold clear()`: 모든 Map.Entry(키와 값) 삭제
- `V remove(Object key)`: 주어진 키와 일치하는 Map.Entry 삭제하고 value 리턴

```java
Map<String, Integer> map = ...;
map.put("홍길동", 14); // 객체 추가
int age = map.get("홍길동"); // 객체 찾기
map.remove("홍길동"); // 객체 삭제, 14 리턴
```

저장된 객체 모두 하나씩 얻을 때

keySet() 메서드로 **모든 키를 Set 컬렉션으로** 얻은 후, 반복자를 통해 키를 하나씩 얻고 get() 메서드로 value를 얻음

```java
Map<K,V> map = ... ;
Set<K> keySet = map.keySet();
Iterator<K> keyIterator = keySet.iterator();
while(keyIterator.hasNext()){
	K key = keyIterator.Next();
	V value = map.get(key);
}
```

entrySet() 메서드로 **모든 Map.Entry를 Set 컬렉션으로** 얻은 뒤, 반복자를 통해  Map.Entry를 하나씩 얻어 getKey()와 getValue() 메서드로 키와 값을 얻음

```java
Set<Map.Entry<String, Object>> entries = map.entrySet();
for (Map.Entry<String, Object> entry : entries) {
	String key = entry.getKey();
	Object value = entry.getValue();
}
```

## HashMap

Map 인터페이스를 구현한 컬렉션

HashMap 생성은 키 타입과 값 타입을 파라미터로 줘 기본 생성자 호출하기

키와 값 타입은 원시 타입은 사용할 수 없고 클래스 및 인터페이스 타입만 가능

```java
Map<K, Y> map = new HashMap<>();
```

### HashMap 구현

학생 객체를 Key, 점수를 Value로 저장하기

```java
// HashMap 생성, Key 타입은 Student, Value 타입은 Integer
Map<Student, Integer> map = new HashMap<>();

// put() 메서드로 키, 값 추가
map.put(new Student(1, "김기역"), 50);
map.put(new Student(2, "김니은"), 64);
map.put(new Student(3, "김삿갓"), 88);

// 객체를 하나씩 처리하기 위해 entrySet() 메서드 이용
Set<Entry<Student, Integer>> entries = map.entrySet();

// 객체를 하나씩 처리
for (Entry<Student, Integer> entry:entries){
  String student = entry.getKey().getName();
  int no = entry.getKey().getNo();
  Integer score = entry.getValue();
  System.out.println("번호: " + no + " 이름: " + student + " 점수: " + score);
}
```

```
실행 결과

번호: 2 이름: 김니은 점수: 64
번호: 3 이름: 김삿갓 점수: 88
번호: 1 이름: 김기역 점수: 50
```

문자열 타입 키와 문자열 List 타입 Value 저장

```java
Map<String, List<String>> map = new HashMap<>();
List<String> stringList = new ArrayList<>();

// 키, 값 추가
map.put("홍길동", stringList);
stringList.add("홍길동"); // List에 요소 추가
stringList.add("홍길동");
stringList.add("홍길동");

// 갱신
map.put("홍길동", stringList); // 같은 키에 값을 넣으면 덮어쓰기 됨

// Map.EntrySet 얻기
Set<Entry<String, List<String>>> entries = map.entrySet();

// 하나씩 처리
for(Entry<String,List<String>> entry:entries){
  String key = entry.getKey();
  List<String> value = entry.getValue();
  System.out.println(key);
  System.out.println("=====");
  System.out.println(value);
}
```

```
실행 결과

홍길동
=====
[홍길동, 홍길동, 홍길동]
```


## Hashtable

HashMap과 동일한 내부 구조를 가짐

동기화된 메서드로 구성되어 있어 멀티 스레드가 동시에 이 메서드를 실행할 수 없고, 하나의 스레드가 실행을 완료해야 다른 스레드를 실행할 수 있음 

따라서 멀테 스레드 환경에서 데이터의 안전한 처리 가능(thread safe)

생성 방법

```java
Map<K, V> map = new Hashtable<>();
```

### 로그인 로직 구현

입력 받은 아이디와 비밀번호가 Hashtable에 존재 하면 로그인 성공! 없으면 실패!

```java
Map<String, String> map = new Hashtable<>();
Scanner scanner = new Scanner(System.in);

// Hashtable에 로그인 정보 입력
map.put("spring", "qwer");
map.put("summer", "qwer1234");
map.put("fall", "qwer123");
map.put("winter", "qwer123");

while(true){
  System.out.println("아이디와 비밀번호를 입력해주세요");
  System.out.println("아이디: ");
  String id = scanner.nextLine();

  System.out.println("비밀번호: ");
  String pw = scanner.nextLine();

  System.out.println("===================");

  if (map.containsKey(id)){ // 입력한 id가 map에 있는지 확인
    String mapPassword = map.get(id); // 입력한 id에 따른 value값 찾아내기
    if (mapPassword.equals(pw)){ // 입력한 pw와 같은지 확인
      System.out.println("로그인에 성공했습니다.");
      scanner.close();
      break;
    } else {
      System.out.println("비밀번호가 틀렸습니다.");
    }

  } else {
    System.out.println("입력하신 아이디가 존재하지 않습니다.");
  }
  
}
```

```
실행 결과

아이디와 비밀번호를 입력해주세요
아이디:
spring
비밀번호:
qwer
===================
로그인에 성공했습니다.
```