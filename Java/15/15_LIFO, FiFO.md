# LIFO, FiFO
## LIFO (Last in First out)

후입 선출

마지막에 들어간 것이 제일 먼저 빠져 나가는 자료구조

**Stack** 인터페이스가 LIFO 자료구조 제공

Stack 객체 생성

```java
Stack<E> stack = new Stack<>();
```

### 스택 메서드

`push(E item)` : 주어진 객체를 스택에 넣음

`pop()` : 마지막으로 들어간 객체를 가져오고, 스택에서 제거

`peek()` : 마지막으로 들어간 객체를 가져오고, 스택에서 제거 안함

동전 케이스를 Stack 클래스로 구현

마지막으로 들어간 객체부터 나오는 것을 볼 수 있음

```java
Stack<Coin> coinStack = new Stack<>();

coinStack.push(new Coin(100));
coinStack.push(new Coin(500));
coinStack.push(new Coin(10));
coinStack.push(new Coin(50));

while(!coinStack.isEmpty()){ // 객체가 있을 때 계속 실행
  Coin pop = coinStack.pop();
  System.out.println(pop.getValue());
}
```

## FIFO(First in First out)

선입 선출

먼저 들어간 것이 먼저 빠져나가는 자료구조

**Queue** 인터페이스가 FIFO 자료구조 제공 (1인큐 4인큐할 때 그 큐, 큐 돌리기 할 때 그 큐임)

Queue 인터페이스를 구현한 대표적인 클래스는 LinkedList

```java
Queue<E> queue = new LinkedList<>();
```

### Queue 메서드

`offer(E e)`: 주어진 객체를 넣음

`peek()`: 객체 하나를 가져오고, 큐에서 제거 안 함

`poll()`: 객체 하나를 가져오고, 큐에서 제거

메세지 큐 구현

LinkedList로 큐를 만들어 메세지 하나씩 꺼내보기

```java
Queue<Message> messageQueue = new LinkedList<>();

messageQueue.offer(new Message("sendMail", "홍길동"));
messageQueue.offer(new Message("sendSms", "자바"));
messageQueue.offer(new Message("sendKakaoTalk", "파이썬"));
messageQueue.offer(new Message("sendWeeklyQuiz", "노션"));

while(!messageQueue.isEmpty()){ // 메시지 큐가 비었는지 확인
  Message message = messageQueue.poll(); // 메세지 큐에서 하나의 메시지 꺼냄
  switch (message.getCommand()){
    case "sendMail":
      System.out.println(message.getTo() + " 에게 메일을 보냅니다.");
      break;
    case "sendSms":
      System.out.println(message.getTo() + " 에게 Sms를 보냅니다.");
      break;
    case "sendKakaoTalk":
      System.out.println(message.getTo() + " 에게 카카오톡을 보냅니다.");
      break;
    default:
      System.out.println(message.getTo() + " 에게 아무거나 보냅니다.");
  }
}
```