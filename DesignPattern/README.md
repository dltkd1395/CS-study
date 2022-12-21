# CS-study

# Design Pattern

## Design Patter이란?

- 디자인 패턴은 주로 객체 지향 프로그래밍 설계에서 공통적으로 발생하는 문제를 피하기 위해 자주 쓰이는 설계 방법을 패턴화한 것입니다. 디자인 패턴은 의사소통 수단이 될 수 있고, 이를 참고하여 개발할 경우 유지보수성, 효율성, 운용성, 성능 최적화에 유리합니다.

---

### 1. 생성 패턴

- [Builder](https://github.com/dltkd1395/CS-study/tree/main/DesignPattern#buillder)
- Prototype
- Factory Method
- Abstract Factory
- Singleton

---

### **2. 구조 패턴**

- Bridge
- Decorator
- Facade
- Flyweight
- Proxy
- Composite
- Adapter

---

### **3. 행위 패턴**

- Interpreter
- Template Method
- Chain of Responsibillity
- Command
- Iterator
- Mediator
- Memento
- Observer
- Strategy
- State
- Visitor

## 1. 생성패턴

## Buillder
- 복잡한 객체에 대해 `생성(contruction)과 표현(representation)을 분리`함으로써 **똑같은 생성 과정으로 서로 다른 객체 표현**을 가능하게 하는 생성 디자인 패턴입니다.

### Builder패턴을 사용해야 하는 이유는 ?

1. Immutability - 객체의 불변성을 유지
2. Named Parameter with Chaining - 체이닝을 통한 명명된 매개변수 사용으로 가독성 증진
3. Design Flexibility - 필수적인 변수와 선택적인 변수를 각각 생성 가능
4. Easy Maintenance - 새로운 멤버가 추가되더라도 기존의 객체 생성 코드를 수정할 필요 없음
5. Avoid RuntimeException - 객체 생성 과정에서 유효성 검사를 통해 논리적인 에러를 막을 수 있음

>💡  불변적인 객체로 구현해야하는 이유는 ? 
>- 불변성 - 객체가 초기에 한번 생성된 이후에는 절대 상태를 바꾸지 않는 것을 말한다. 객체 생성시에 모든 정보가 주어지고 객체의 생애 주기 동안에는 상태가 바뀌지 않는 것이 특징이다.
>- 사용하기 쉽다
>- Thread Safe하다. 동기화할 필요가 없다
>- 자유롭게 공유할 수 있다.


### Builder 패턴의 한계

- 코드를 2배정도 많이 사용하게 된다. 따라서 설정해야 할 `매개 변수가 적을 경우`에는 일반 생성자를 통한 생성이 더욱 편할 수 있다.
  
## 구현

### Builder 패턴 적용 전

- 일반적으로 생성자(Constructor)를 통해 객체를 생성할 것이다. 생성자를 사용할 경우 멤버를 선택적으로 생성하기 어렵다.
1. **생성자를 사용한 생성 - 자바빈즈 패턴(JavaBeans Pattern)**
- 매개변수가 없는 기본 생성자를 통해 객체를 생성한 뒤, setter 메서드를 통해 멤버를 설정하는 방식이다.

[클래스 정의]

```java
public User() {
}

public User(String firstName, String lastName, int age, String phone, String address) {
	this.firstName = firstName;
	this.lastName = lastName;
	this.age = age;
	this.phone = phone;
	this.address = address;
}
```

[객체 생성]

```java
User user1 = new User("nabi", "Kim", 6, "02-6666-6666, "서울시 강남구 테헤란로");
User user2 = new User("pobi", "Lee", 4, null, null);

User user3 = new User();
user3.setFirstName("nabi")
user3.setLastName("Choi")
```

1. **생성자를 사용한 생성 - 점층적 생성자 패턴(Telescoping Constructor Pattern)**
- 필수 매개변수만을 가진 생성자를 만들고 선택 매개변수를 하나씩 추가한 생성자를 만든다. 수많은 `생성자 오버로딩`을 통해 원하는 형태의 객체를 생성하도록 하는 방식이다.

[객체생성]

```java
public User(String firstName, String lastName, int age) {
	this.firstName = firstName;
	this.lastName = lastName;
	this.age = age;
	this.phone = null;
	this.address = null;
}

public User(String firstName, String, lastName, int phone) {
	this.firstName = firstName;
	this.lastName = lastName;
	this.age = null;
	this.phone = phone;
	this.address = null;
}
```

> 위 예제와 같이 생성자를 통한 객체 생성 시 필수 매개변수와 선택 매개변수를 구분하여 구현하기가 어렵다. 특히 매개변수가 많아진다면 일일히 setter를 부르는 일도, 매개변수 자리를 세주는 것도 일이다. 생성자를 경우의 수 별로 구현하는 것은 더욱 끔찍할 것이다.
> 

### Builder 패턴 적용 후

[클래스 정의]

```java
// 클래스를 Final로 설정하여 확장이 불가능하며 불변성이 유지됨
public final class User {
	private final String firstName; //필수 변수
	private final String lastName; //필수 변수
	private final int age; //필수 변수
	private final String phone; //필수 변수
	private final String address; //필수 변수

	private User(UserBuilder builder) {
		this.firstName = builder.firstName;
		this.lastName = builder.lastName;
		this.age = builder.age;
		this.phone = builder.phone;
		this.address = builder.address;
	}

	// Setter를 구현하지 않음으로써 불변성 유지
  public String getFirstName() {
      return firstName;
  }
  public String getLastName() {
      return lastName;
  }
  public int getAge() {
      return age;
  }
  public String getPhone() {
      return phone;
  }
  public String getAddress() {
      return address;
  }
	
	@Override
  public String toString() {
      return "User: "+this.firstName+", "+this.lastName+", "+this.age+", "+this.phone+", "+this.address;
  }

  // 객체 내부에 Builder 정의(중첩 클래스)
  public static class UserBuilder 
  {
      // 필수적인 변수만 final로 설정
      private final String firstName;     // 필수 변수
      private final String lastName;      // 필수 변수
      private int age;                    // 선택 변수
      private String phone;               // 선택 변수
      private String address;             // 선택 변수

      // Builder 생성자 매개변수는 필수 변수만을 포함
      public UserBuilder(String firstName, String lastName) {
          this.firstName = firstName;
          this.lastName = lastName;
      }
      // 선택적인 변수는 추가적인 메서드를 구현하여 생성
      public UserBuilder age(int age) {
          this.age = age;
          return this;
      }
      public UserBuilder phone(String phone) {
          this.phone = phone;
          return this;
      }
      public UserBuilder address(String address) {
          this.address = address;
          return this;
      }
      // Builder로 생성된 객체 반환
      public User build() {
          User user =  new User(this);
          if (!validateUserName(user)) throw new NoNameException();
          if (!validateUserAge(user)) throw new InvalidAgeException();
          return user;
      }
      private boolean validateUserName(User user) {
          if (user.firstName==null || user.lastName==null) {
              if (user.age!=null || user.phone!=null || user.address!=null) return false;
          }
          return true;
      }
      private boolean validateUserAge(User user) {
          if (user.age<0) return false;
          return true;
      }
  }
}
		
```

[객체 생성]

```java
User user1 = new User.UserBuilder("nabi", "Kim")
                     .age(6)
                     .phone("02-666-6666")
                     .address("서울시 강남구 테헤란로")
                     .build();

User user2 = new User.UserBuilder("pobi", "Lee")
                     .age(5)
                     // no phone
                     // no address
                     .build();

User user3 = new User.UserBuilder("nabi", "Choi")
                     // no age
                     // no phone
                     // no address
                     .build();
```

> 빌더 패턴을 이용해 위와 같이 하나의 생성자만으로 여러 상태의 객체를 생성할 수 있게 된다.
> 
- 멤버를 `final로 설정`하여 불변성을 유지할 수 있다.
- 선택적인 변수의 경우 `null로 설정`할 필요가 없다. 또한 생성자 오버로딩을 하지 않아 선택적인 변수를 가진 객체도 동일한 방법으로 생성할 수 있다.
- 각 변수의 이름에 해당하는 메서드를 chaining방식으로 접근하여 초기화할 수 있다. 따라서 **생성자의 매개변수 순서를 기억할 필요가 없고, 생성 과정에서의 가독성이 훨씬 좋아진다.**
- 만약 **새로운 멤버 변수가 추가되더라도 기존 객체 생성 코드를 수정하지 않아도 된다.** 새롭게 추가된 멤버 변수도 선택적인 매개변수와 동일하게 처리하기 때문이다.
- 추가적으로 **빌더 클래스 내부에 유효성 검사 매서드를 추가**한다면 멤버 생성 과정에서의 논리적인 에러를 사전에 차단할 수 있다.

---

## Factory Method
- 팩토리 메소드 패턴(Factory Method Pattern) - 상위 클래스에 알려지지 않은 구현 클래스를 생성하는 패턴이다. 또한 하위 클래스가 어떤 객체를 생성할지 결정하도록 하는 패턴이기도 한다. 그리고 상위 클래스 코드에 구체적인 클래스 이름을 감추기 위한 방법으로도 사용한다.
<img src="/dltkd1395/CS-study/raw/main/DesignPattern/image/factory1.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">
- 팩토리 메소드 패턴은 무언가를 위한 공장이라고 생각하면 된다.
  [신발 매장 코드 예시]
  ```java
  // 해당 이름의 신발을 찾아서 특정 구상 객체 생성
  Shoes orderShoes(String name) {
    // 해당 이름의 신발을 찾아서 특정 구상 객체 생성
    Shoes shoes;

    if (name.equals("blackShoes"))        shoes = new BlackShoes();
    else if (name.equals("brownShoes"))   shoes = new BrownShoes();
    else if (name.equals("redShoes"))     shoes = new RedShoes();

    // 신발을 준비하고 포장하는 메서드
    // 모든 신발 고용 메서드
    shoes.prepare();
    shoes.packing();

    return shoes
  }
  ```
- 현재 이 신발 매장에는 3개의 신발만 팔고 있다. 그리고 앞으로 판매되는 제품이 늘어나가거나 지금 있는 제품이 더 이상 판매되지 않을 수 도 있다. 이 부분은 언제나 변경이 가능한 부분이다.
- 그러나 밑에 있는 prepare()과 packing() 두 메서드는 제품에 변화가 생기더라도 변하지 않는 부분이다.
- 위 코드를 간단하게 캡슐화하여 ShoesFactory라는 클래스로 만들면
  ```java
  public class ShoesFactory {
    public Shoes makeShoes(String name) {
        Shoes shoes = null;
        if (name.equals("blackShoes"))      shoes = new BlackShoes();
        else if (name.equals("brownShoes")) shoes = new BrownShoes();
        else if (name.equals("redShoes"))   shoes = new RedShoes();

        return shoes;
    }
  }
  ```
  - 위 코드처럼 만들 수 있다. 그리고 아래처럼 할 수 있다.
  ```java
  public class ShoesStore {
    ShoesFactory factory;

    public ShoesStore(ShoesFactory factory) {
        this.factory = factory;
    }

    Shoes orderShoes(String name) {
        Shoes shoes = factory.makeShoes(name);
        shoes.prepare();
        shoes.packing();

        return shoes;
    }
  }
  ```
 - 고객에게 득정 신발에 대한 주문이 들어 왔을 때 매장에서는 공장에 해당 신발 오더를 넣고 받으면 되고, 판매하는 신발이 늘어나거나 단종되면 신발 매장이 아닌 신발 공장에서 그 변화를 처리할 수 있다.
 - 위의 예시 코드는 디자인 패턴까지 아니고 프로그래밍에 사용하는 관용구정도로 보면 된다.
 - 위에서 봤던 신발 매장은 점점 성장하여 다른 나라로 진출하기 시작했다. 일본과 프랑스에도 진출을 하여 매장을 지었다고 하자.
```java
JapanShoesStore jpStore = new JapanShoesStore(new JapanShoesFactory());
jpStore.order("blackShoes");

FranceShoesStore  frStore = new FranceShoesStore (new FranceShoesFactory());
   frStore.order("blackShoes");
```
- 그런데 이 해외 매장들이 본사에서 준 가이드라인 그대로 똑같이 만들지 않고, 현지 상황에 맞춰 일본에서는 약간 굽을 높게 만들고 프랑스에서는 신발 옆에 패턴을 넣기 시작했다. 뿐 만아니라 포장까지도 자기 마음대로 하였다.
- 그래서 본사는 매장과 신발 생산 과정 전체를 묶어주는 아래와 같은 프레임 워크를 만들어 모든 매장에서 이를 따르게 하였다.
```java
 public abstract class ShoesStore {
 
    public ShoesStore orderShoes(String name) {
        Shoes shoes = makeShoes(name);
        shoes.prepare();
        shoes.packing();
 
        return shoes;
 
    }
 
    abstract Shoes makeShoes(String name);
 
}
```

- ShoesStore 추상 클래스를 선언하면, 달라지는 부분은 추상메서드인 신발 제작 뿐이다. 각 현지 상황에 맞춰 makeShoes 메서드를 오버라이드하여 일본에서는 약간 굽을 높게 만들고, 프랑스에서는 패턴을 넣어 신발을 제작하면 된다.
- 그 대신 제작, 분비, 포장하는 공정은 ShoesStore를 상속하는 전 세계 모든 매장들에서 똑같은 시스템이 적용 될 수 있다.
```java
class JapanShoesStore extends ShoesStore {
 
    @Override
    Shoes makeShoes(String name) {
        if (name.equals("blackShoes")) return new JPStyleBlackShoes();  
        else if (name.equals("brownShoes")) return new JPStyleBrownShoes();
        else if (name.equals("redShoes")) return new JPStyleRedShoes();
        else return null;
   }

}
```

```java
class FranceShoesStore extends ShoesStore {
 
    @Override
    Shoes makeShoes(String name) {
        if (name.equals("blackShoes")) return new FRStyleBlackShoes();  
        else if (name.equals("brownShoes")) return new FRStyleBrownShoes();
        else if (name.equals("redShoes")) return new FRStyleRedShoes();
        else return null;
   }

}
```
- 여기서 가장 중요한 점은 하위 클래스에서 메서드를 오버라이딩 하였기 때문에, 슈퍼클래스에 있는 orderShoes 메서드에서는 어떤 신발이 만들어 지는지 전혀 모르고 있다는 것이다. 동적 바인딩되는 그 메서드에서 주는 신발을 받아서 준비하고 포장할 뿐이다.
  <img src="/dltkd1395/CS-study/raw/main/DesignPattern/image/factory3.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">
  - 신발을 주고 받고 생성하는 생성자 클래스
    <img src="/dltkd1395/CS-study/raw/main/DesignPattern/image/factory4.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- ***생성자 클래스에서 생산되는 제품 클래스***
- 팩토리 메소드 패턴의 클래스들은 크게 생산자 클래스와 제품 클래스로 구분할 수 있다.
- 이제 생산자 클래스인 ShoesStore 클래스에서 사용될 제품 클래스 Shoes 클래스를 작성해보자.
```java
abstract class Shoes {
 
    String name;
    String bottom;
    String leather;
    boolean hasPattern;
 
    void prepare() {
        System.out.println("주문하신 신발을 준비중입니다.");
    }
 
    void packing() {
        System.out.println("준비 완료된 신발을 포장중입니다.");
    }
 
    public String getName() {
        return name;
    }
 
}
```

```java
class JPStyleBlackShoes extends Shoes {
 
    public JPStyleBlackShoes() { 
        name = "일본 스타일의 검은 구두";
        bottom = "굽이 높은 밑창";
        leather = "스웨이드";
        hasPattern = false;
    }
 
}
```

```java
class FRStyleBlackShoes extends Shoes {
 
    public FRStyleBlackShoes() { 
        name = "프랑스 스타일의 검은 구두";
        bottom = "일반 굽높이 밑창";
        leather = "스웨이드";
        hasPattern = true;
    }
 
}
```
추상 클래스로 Shoes 클래스를 설계하고, JPStyleBlackShoes, FRStyleBlackShoes에서 멤버변수를 초기화하며 구현해주었다.
>추상 메소드가 없는 추상 클래스가 여기서 등장한다.</br>
Shoes 클래스는 추상 메소드가 존재하지 않지만 추상 클래스로 선언되었기 때문에 new Shoes();로> 직접 객체 생성은 불가능하고,</br>
Shoes 클래스를 상속받는 클래스에서 Shoes를 참조변수로하여 객체 생성을 할 수 있다.</br>
추상 메소드 존재 O -> 무조건 클래스도 추상 클래스로 선언</br>
추상 메소드 존재 X -> 현재 클래스로 다이렉트 객체 생성을 막고 싶을 때, 추상 클래스로 선언
- 여기까지 UML에 설계된 클래스들의 구현이 마무리 되었다. 이제 메인 클래스에서 위에서 설계한 팩토리 메소드 패턴이 어떻게 사용되는지 살펴 보자.
```java
public class Main {
 
    public static void main(String[] args) {
        
        // 일본과 프랑스에 현지 트렌드에 맞춰 매장을 열었음
        ShoesStore jpStore = new JapanShoesStore();
        ShoesStore frStore = new FranceShoesStore();
      
        // 일본 매장에서 검은 신발 주문
        Shoes shoes = jpStore.orderShoes("blackShoes");
        System.out.println("일본 매장에서 주문한 검은 신발 : " + shoes.getName());
        
        System.out.println();
        
        // 프랑스 매장에서 검은 신발 주문
        shoes = frStore.orderShoes("blackShoes");
        System.out.println("프랑스 매장에서 주문한 검은 신발  : " + shoes.getName());
 
    }
 
}
```
- 위 코드를 실행해보면 아래와 같이 출력될 것이다.
```
> 주문하신 신발을 준비중입니다.
> 준비 완료된 신발을 포장중입니다.
> 일본 매장에서 주문한 검은 신발 : 일본 스타일의 검은 구두
> 
> 주문하신 신발을 준비중입니다.
> 준비 완료된 신발을 포장중입니다.
> 프랑스 매장에서 주문한 검은 신발 : 프랑스 스타일의 검은 구두
```
- 위 메인 메소드의 프로세스는 아래와 같다. 참고로 일본 매장과 프랑스 매장에서의 프로세스는 동일하니 공통적인 프로세스로 묶어서 설명하겠다.

>1. 현지 신발 매장이 문을 열었음. (ShoesStore를 참조변수로 하는 현지 ShoesStore 객체 생성)
>2. 매장에 신발 종류를 통해 신발을 주문함. (ShoesStore의 orderShoes메소드)
>3. ShoesStore의 orderShoes 내부에서 생성된 객체에 맞게 동적바인딩되어 오버라이딩된 makeShoes 메소드가 실행됨
>4. 오버라이딩된 makeShoes 메소드에서 주문에 맞는 신발객체를 호출된 orderShoes메소드로 리턴함
>5. prepare(), packing() 메소드가 실행됨
>6. make, prepare, packing이 완료된 Shoes 객체를 리턴함
>7. 주문한 신발이 어떤 객체인지 출력하여 확인
- 마무리로 다시 한번 팩토리 메소드 패턴을 정리하자면, 팩토리 메소드 패턴은 객체를 만들어내는 부분을 자식 클래스에 위임하는 패턴이다.

- new 키워드를 호출하는 부분을 서브 클래스에 위임하였기 때문에, 상위 클래스인 ShoesStore 클래스 내부에는 new 라는 키워드가 존재하지 않는다.

- 즉, 상위 클래스가 아닌 하위 클래스에서 어떤 클래스를 만들지 결정하게 하도록 하는 것이다.

- 하위 클래스에서 추상 메소드인 makeShoes메소드를 오버라이딩 하였기 때문에, 상위 클래스에 있는 orderShoes 메소드에서는 어떤 신발이 만들어 지는지 전혀 모르고 있다.

- 동적 바인딩된 그 메소드에서 주는 신발을 받아서 준비하고 포장해서 내놓을 뿐 이다.
> 객체 지향 프로그래밍 세계에서 자식은 부모를 알아도, 부모는 자식을 모른다.