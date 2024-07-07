# this
현재 객체를 참조하는 키워드

`this` 키워드를 통해 현재 객체의 멤버 변수와 메서드에 접근할 수 있음

## `this` 키워드 사용

`this` 로 인해 `Person` 클래스의 멤버 변수에 접근

`buyFood` 메서드를 실행할 때 외부 클래스 Food의 멤버 객체를 끌어와 현재 객체의 멤버 변수에 반영

```java
public class Person {
  int weight;
  int money;
  boolean fat;

  public Person(int weight, int money, boolean fat) {
      this.weight = weight;
      this.money = money;
      this.fat = false;
  }
  
  public void buyFood(Food food) {
    this.money -= food.cost;
	}
  
}
```

외부 클래스 `Food` , 세 가지의 멤버 변수를 선언

여기도 `this` 를 통해 `Food` 의 멤버 변수에 접근하고 있음

```java
public class Food {
    int cost;
    int weight;
    String name;

    public Food(int cost, int weight, String name) {
        this.cost = cost;
        this.weight = weight;
        this.name = name;
    }

}
```

**main 메서드**

실행하면 객체 Person의 멤버 변수를 참조하여 값을 가져옴

1. 인스턴스 person, food 생성
2. person의 메서드 buyFood 실행되면서 person의 money가 food의 cost 만큼 깎임
3. person의 weight와 person의 money 출력

```java
public class MainPerson {
  public static void main(String[] args) {
    Person person = new Person(100, 5000, false);
    Food food = new Food(50, 30, "사탕");

    person.buyFood(food);

    System.out.println(person.weight); // 100 출력
    System.out.println(person.money); // 4950 출력
  }
}
```