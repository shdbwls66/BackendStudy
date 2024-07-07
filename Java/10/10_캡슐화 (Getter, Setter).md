# 캡슐화(Getter, Setter)
객체 지향 프로그래밍에서 외부에서 객체 데이터로의 직접적인 접근은 지양하고 있음

객체의 데이터를 외부에서 마음대로 접근하여 수정하면 객체의 무결성이 깨지는 문제점이 있음 (ex. 외부에서 자동차 속도를 음수로 바꾸는 경우)

이러한 이유로 인해 객체 지향 프로그래밍에서는 메서드를 통해 데이터를 변경하는 것을 선호

## Setter 메서드

객체 지향 프로그래밍에서 객체의 무결성을 지키기 위해 직접적이지 않은 방법으로 데이터에 접근할 때 사용하는 메서드

객체 데이터는 private로 만들어 외부 접근은 막고, 메서드는 public으로 만들어 메서드를 통해 데이터를 변경

### Setter 사용

private를 통해 speed로의 접근은 막고, setSpeed 메서드를 통해 speed를 변경하도록 해당 메서드는 공개

speed가 0일 때 0, 0 이상일 때 인자로 받은 값을 멤버 변수에 적용

전달 받은 속도에 따라 기어를 변환

```java
public class Car {
	private int speed;
	
	public void setSpeed(int speed) {
		// speed 반영
    this.speed = speed < 0 ? 0 : speed;

    // 조건 따라 gear 변경
    if (speed <= 30) {
      this.gear = 1;
      System.out.println("현재 속도는 " + speed +", " + this.gear + "단 입니다.");
    } else if(speed <= 70){
      this.gear = 2;
      System.out.println("현재 속도는 " + speed +", " + this.gear + "단 입니다.");
    } else {
      this.gear = 3;
      System.out.println("현재 속도는 " + speed +", "+ this.gear + "단 입니다.");
    }
	}
}
```


## Getter 메서드

외부에서 객체 데이터를 읽을 때 사용하는 메서드

객체 데이터는 private로 만들어 외부 접근은 막고, 메서드는 public으로 만들어 메서드를 통해 데이터를 읽음

### Getter 사용

getSpeed() 메서드가 통해 멤버 변수 speed로 접근하여 km를 계산 후 반환

```java
public class Car {
	private int speed;
	
	public double getSpeed() {
		double km = speed * 1.6;
		return km;
	}
}
```


### setSpeed(), getSpeed() 실행

```java
public class Test {
  public static void main(String[] args) {
    Car car = new Car();
    car.setSpeed(120); // 현재 속도는 120, 3단 입니다. 출력
    System.out.println(car.getSpeed()); // 192.0 출력

  }
}
```