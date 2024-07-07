# StringBuffer / StringBuilder
- 문자열을 추가하거나 변경할 때 주로 사용하는 자료형

- StringBuffer와 StringBuilder 내장메서드는 동일

```
String 클래스도 문자열 추가 가능하나 String은 새로운 객체를 생성하고 String 공간을 할당하기 때문에 메모리 공간이나, 속도 측면에서 비효율적이라는 단점이 있음
```

Hello java World 나타내기

문자열이 합쳐져서 출력 되는 것을 볼 수 있음

```java
String result = "";
result += "Hello ";
result += "java";
result += "World";
System.out.println(result);

StringBuilder sb = new StringBuilder();
sb.append("Hello ");
sb.append("java");
sb.append("World");
System.out.println(sb);

StringBuffer sf = new StringBuffer();
sf.append("Hello ");
sf.append("java");
sf.append("World");
System.out.println(sf);
```


## 내장 메서드
### `append`
- 문자열을 생성 / 추가

‘hello’ 와 ‘!’ 생성하기
```java
StringBuffer result = new StringBuffer();
result.append("Hello");
result.append("!");
System.out.println(result);
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/82274b26-40eb-4b57-b6d4-f947ddb8b77a)


### `insert`
- 특정 위치에 원하는 문자열 삽입

0번 인덱스에 World 끼워 넣기
```java
StringBuffer sb = new StringBuffer();

sb.append("Hello");
sb.insert(0, "World");
sb.insert(0, "World");
sb.insert(0, "World");
sb.insert(0, "World");

System.out.println(sb);
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/cc678c7d-9607-441f-a25b-6efc95cd727a)

5번에 넣으면
```java
sb.insert(5, "World");
System.out.println(sb);
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/36fb1965-f5da-4ba6-bad5-3405ed81f85c)


### `substring`
- `String` 자료형의 `substring` 과 동일한 역할

- 인덱스 값 범위 지정할 때 주의!! (마지막 인덱스 값+1)

Hello 문자열에서 특정 문자열 추출 하기
```java
StringBuffer sb = new StringBuffer();
sb.append("Hello");
System.out.println(sb.substring(2,5));
```

![image](https://github.com/shdbwls66/backendJava/assets/168792230/90c2a002-5892-4a4f-9ac9-13161112f9e9)


```
StringBuffer: 멀티스레드 환경에서 안정적인 이용이 가능
StringBuilder : 속도 등의 측면에서 우수
```