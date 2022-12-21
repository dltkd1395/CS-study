# CS-study

# Design Pattern

## Design Patter이란?

- 디자인 패턴은 주로 객체 지향 프로그래밍 설계에서 공통적으로 발생하는 문제를 피하기 위해 자주 쓰이는 설계 방법을 패턴화한 것입니다. 디자인 패턴은 의사소통 수단이 될 수 있고, 이를 참고하여 개발할 경우 유지보수성, 효율성, 운용성, 성능 최적화에 유리합니다.

---

### 1. 생성 패턴

- [Builder](https://github.com/dltkd1395/CS-study/tree/main/DesignPattern#buillder)
- Prototype
- [Factory Method](https://github.com/dltkd1395/CS-study/tree/main/DesignPattern#factory-method)
- [Abstract Factory](https://github.com/dltkd1395/CS-study/tree/main/DesignPattern#abstract-factory)
- [Singleton](https://github.com/dltkd1395/CS-study/tree/main/DesignPattern#singleton)

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
</br></br>
[맨위로](https://github.com/dltkd1395/CS-study/tree/main/DesignPattern#design-pattern)
---

## Factory Method
- 팩토리 메소드 패턴(Factory Method Pattern) - 상위 클래스에 알려지지 않은 구현 클래스를 생성하는 패턴이다. 또한 하위 클래스가 어떤 객체를 생성할지 결정하도록 하는 패턴이기도 한다. 그리고 상위 클래스 코드에 구체적인 클래스 이름을 감추기 위한 방법으로도 사용한다.
<img src="https://github.com/dltkd1395/CS-study/blob/main/DesignPattern/image/factory1.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">
- 팩토리 메소드 패턴은 무언가를 위한 공장이라고 생각하면 된다.</br>
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
  <img src="https://github.com/dltkd1395/CS-study/blob/main/DesignPattern/image/factory3.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">
  - 신발을 주고 받고 생성하는 생성자 클래스
    <img src="https://github.com/dltkd1395/CS-study/blob/main/DesignPattern/image/factory4.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

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
</br></br>

[맨위로](https://github.com/dltkd1395/CS-study/tree/main/DesignPattern#design-pattern)

---

## Abstract Factory
- 추상 팩토리 패턴(Abstract-Factory Pattern)이란 - 인터페이스를 이용하여 서로 연관된, 또는 의존하는 객체를 구현 클래스를 지정하지 않고도 생성할 수 있는 패턴이다.
- 바로 위 팩토리 메소드 편에 보았던 JPStyleBrownShoes, FRStyleRedShoes와 같이 추상 클래스에 의존하는 구현 클래스를 만들지 않고도 생성할 수 있다.

```java
class DependentShoesStore {
 
    public Shoes makeShoes(String style, String name) {
        Shoes shoes = null;
        if (style.equals("Japan")) {
            if (name.equals("blackShoes")) shoes = new JPStyleBlackShoes();
            else if (name.equals("brownShoes")) shoes = new JPStyleBrownShoes();
            else if(name.equals("redShoes")) shoes = new JPStyleRedShoes();
        }
        else if(style.equals("france")) {  
            if (name.equals("blackShoes")) shoes = new FRStyleBlackShoes();
            else if (name.equals("brownShoes")) shoes = new FRStyleBrownShoes();
            else if(name.equals("redShoes")) shoes = new FRStyleRedShoes(); 
        }
        shoes.prepare();
        shoes.packing();
        return shoes;
    }

}
```

- 만약 위와 같이 스타일과 신발 이름을 입력받아 해당 신발을 제작하고 준비, 포장해서 돌려주는 클래스가 있다고 하자.
- 직접 팩토리 메서드 패턴을 정리할 때 이미 한번 생각해본 적이 있었는데,</br>
 <img src="https://github.com/dltkd1395/CS-study/blob/main/DesignPattern/image/AbFactory2.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

 - 지금 코드는 몇 줄 되지 않는데도 이와 같이 복잡하고 관리하기 힘든 모습인데, 만약 나라가 수십개국에 신발종류도 각 나라마다 무수히 많다면 어떻게 될까??
 - 그리고 나중에 이것들을 수정해야 할 일이 생긴다면 정말 생각만해도 끔찍할 것이다.
 - 구두를 만드는 스토어 객체는 구두 객체들을 가지고 있으면서, 이 객체들을 사용해서 구두를 준비하고, 포장하게 된다.
 - 이때 스토어 객체는 고수준 컴포넌트라고 하고, 구두 객체들을 저수준 컴포넌트라고 한다. 고수준 컴포넌트(스토어)는 저수준 컴포넌트(구두들)를 가지고 사용할 수 있다.
 - 그래서 위에 있는 다이어그램을 보면, 고수준의 컴포넌트가 저수준의 컴포넌트에 심하게 의존한다는 것을 볼 수 있다.
 - 의존한다는 것은 나중에 새로운 구두가 추가되면, 스토어 객체까지 손봐야 할 일이 생긴다는 의미라서 이 의존관계를 뒤집을 필요가 있다.
 - 그래서 위 설계는 객체지향 설계 5대 원치 SOLID중, 5번째 DIP를 따르는 설계가 필요하다.
> DIP(Dependency-Inversion Principle) : 구상 클래스에 의존하도록 만들지 않고, 추상화 된 것에 의존하도록 만들어야 한다.
- 이 원칙을 제대로 적용하려면, 구현 클래스처럼 구체적인 것이 아니라 추상 클래스나 인터페이스같이 추상적인 것에 의존하는 코드를 만들어서 고수준 컴포넌트와 저수준 컴포넌트 모두에 적용하여야한다.
- 그래서 방금 말한 의존관계 역전 원칙을 구두 가게에 다시 적용해보자면 아래와 같은 UML처럼 설계가 가능하다.</br>
 <img src="https://github.com/dltkd1395/CS-study/blob/main/DesignPattern/image/AbFactory3.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">
- 이렇게 하면 고수준 컴포넌트 ShoesStore와 저수준 컴포넌트인 각종 구두 객체들 모두 추상클래스인 Stores에 의존하게 된다.
- 하지만 설계를 하다보면 의존관계 역전 원칙을 지키도록 설계하기가 쉽지 않다.
- 그래서 의존 관계 역전원칙을 지키는데 도움이 될만한 가이드 라인을 가져왔다.
> 1. 어떤 변수라도 구상 클래스에 대한 레퍼런스를 저장하지 말것
> - new 연산자 사용하면 구상 클래스 레퍼런스를 저장하는 것, 이것 대신 팩토리를 사용하라!!
> 2. 구상 클래스에서 유도된 클래스를 만들지 말 것.
> - 구상 클래스에서 유도된 클래스를 만들면 특정 구상 클래스에 의존하게 된다.
> 3. 베이스 클래스에서 이미 구현되어 있던 메서드를 오버라이드 하지 말 것.
> - 이미 구현되어 있는 메서드를 오버라이드 하는 것은 애초부터 베이스 클래스가 잘 추상화되어 있는 것이 아니다!
> - 베이스 클래스에서 메서드를 정의 할때는 모든 서브클래스에서 공유할 수 있는 것들만 정의 해야한다.
- 하지만 위 가이드 라인들은 지향하면 좋다는 것이고, 꼭 지켜져야 하는 것은 아니다.
- 실제로 자바 프로그램 가운데 이것을 완벽하게 지키는 것은 거의 없다!!
- 위와 같이 설계하는 것이 바람직하다는 것은 알고 넘어가는 것이 좋다.
</br></br>
다시  구두 가계로 돌아와서, 우려했던 대로 신발매장이 더 많은 나라에 진출해서 인도, 이태리, 중국 등등 많은 곳에 매장이 생긴다고 가정해보자.</br></br>
하지만 몇몇 분점에서는 각 현지 공장에서 싸구려 재료들을 몰래 사용해서 본사에서 의도하지 않은 마진을 몰래 올리고 있다는 소식을 듣고 무언가 조치를 취하려고 한다.</br></br>
그래서 본사에서 원재료를 사용해서 신발을 만들어서 분점으로  배송하려고 했는데 지난 팩토리 메서드를 정리한 부분에서 먼저 보았듯이, 같은 검은 구두라고 하더라도 일본매장의 검은 신발과 프랑스매장의 검은 신발의 밑창은 서로 다르게 만들어야하고 따라서 재료들도 달라져서 문제가 생긴다.</br></br>
그래서 다시 생각해낸 해결 방법이 지역 별로 소규모 신발재료 공장을 나누어서 신발을 만드는 것이다.</br>

```java
interface ShoesIngredientFactory {
 
    public Bottom makeBottom();
    
    public Leather makeLeather();
 
    public boolean hasPattern();
 
}
```
그래서 위와 같은 공통 기능을 제공할 신발재료 공장 인터페이스를 만들어 주었다.

```java
class JPShoesIngredientFactory implements ShoesIngredientFactory {
 
    @Override
    public Bottom makeBottom() return new RubberBottom();
 
    @Override
    public Leather makeLeather() return new LeatherOfCows();
    
    @Override
    public boolean hasPattern() return false;
 
}
```

```java
class FRShoesIngredientFactory implements ShoesIngredientFactory {
 
    @Override
    public Bottom makeBottom() return new PlasticAndRubberBottom();
 
    @Override
    public Leather makeLeather() return new LeatherOfSheeps();
 
    @Override
    public boolean hasPattern() return true;
 
}
```
이번에도 지난 팩토리 메서드떄와 동일하게 일본과 플랑스를 기준으로 설명하려고 한다.
일본 매장으로 가는 신발재료 공장 클래스와 프랑스 매장으로 가는 신발재료 공장 클래스처럼 재료 공장 인터페이스를 구현하는 클래스를 만들었다.</br>
그리고 공장에서 각 메서드들이 return해주는 각가의 신발 재료들이 구현해야하는 인터페이스는 아래와 같다.
```java
interface Bottom {
 
    public String getName();
 
}
```

```java
interface Leather {
 
    public String getName();
 
}
```
위 재료 인터페이스를 구현한 클래스는 아래와 같다.
```java
// 고무 밑창
class RubberBottom implements Bottom {
 
    @Override
    public String getName() return "고무";
 
}
```

```java
// 플라스틱과 고무 혼한 밑창
class PlasticAndRubberBottom implements Bottom {
 
    @Override
    public String getName() return "플라스틱, 고무";
 
}
```

```java
// 소가죽
class LeatherOfCows implements Leather {
 
    @Override
    public String getName() return "소가죽";
 
}
```

```java
// 양가죽
class LeatherOfSheeps implements Leather {
 
    @Override
    public String getName() return "양가죽";
 
}
```
이제는 공장은 완성됐고, 공장에서 만드는 신발 클래스를 살펴보도록 하자.
```java
abstract class Shoes {
 
    String name;
    Bottom bottom;
    Leather leather;
    boolean hasPattern;
 
    abstract void assembling(); // 신발을 조립하는 추상 메소드
 
    void prepare() {
        System.out.println("완성된 신발을 준비 중입니다.");
    }
 
    void packing() {
        System.out.println("준비된 신발을 포장 중입니다.");
    }
 
    public String getName(){
        return name;
    }
 
    public void setName(String name) {
        this.name = name;
    }
 
}
```
위 Shoes 클래스에서 주목할 점은 원재료들을 조립하는 assembling이라는 추상 메서드이다.
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
지난번 팩토리 메소드에서 사용했던 Shoes.class에서는 존재하지 않는 메서드이다.
```java
class BlackShoes extends Shoes {
 
    ShoesIngredientFactory shoesIngredientFactory;
 
    public BlackShoes(ShoesIngredientFactory shoesIngredientFactory) {
        this.shoesIngredientFactory = shoesIngredientFactory;
    }
 
    @Override
    void assembling() { 
        System.out.println("신발을 제작중입니다. " + name);
        leather = shoesIngredientFactory.makeLeather();
        bottom = shoesIngredientFactory.makeBottom();
        System.out.println("신발 정보 : 밑창은 " + bottom.getName() + " 사용 하였으며, 가죽은 " + leather.getName() + " 사용하였습니다.");
    }
 
}
```

```java
class BrownShoes extends Shoes {
 
    ShoesIngredientFactory shoesIngredientFactory;
 
    public BrownShoes(ShoesIngredientFactory shoesIngredientFactory) {
        this.shoesIngredientFactory = shoesIngredientFactory;
    }
 
    @Override
    void assembling() {
        System.out.println("신발을 제작중입니다. " + name);
        leather = shoesIngredientFactory.makeLeather();
        bottom = shoesIngredientFactory.makeBottom();
        System.out.println("신발 정보 : 밑창은 " + bottom.getName() + " 사용 하였으며, 가죽은 " + leather.getName() + " 사용하였습니다.");
    }
 
}
```

```java
class RedShoes extends Shoes {
 
    ShoesIngredientFactory shoesIngredientFactory;
 
    public RedShoes(ShoesIngredientFactory shoesIngredientFactory) {
        this.shoesIngredientFactory = shoesIngredientFactory;
    }
 
    @Override
    void assembling() { 
        System.out.println("신발을 제작중입니다. " + name);
        leather = shoesIngredientFactory.makeLeather();
        bottom = shoesIngredientFactory.makeBottom();
        System.out.println("신발 정보 : 밑창은 " + bottom.getName() + " 사용 하였으며, 가죽은 " + leather.getName() + " 사용하였습니다.");
    }
 
}
```
위 클래스들은 보다시피 Shoes 추상 클래스를 구현한 각 컬러들의 Shoes 클래스이다.</br>
이제는 더 이상 국가별로 BlackShoes, BrownShoes, RedShoes 각각 다 만들어주지 않아도 된다.</br>
이 클래스들은 ShoesIngredientFactory 인스턴스를 생성자로 받아서 이 인스턴스로부터 원재료를 직접 받게된다.</br>
추상 메서드여서 오버라이딩하여 구현해준 assembling 메서드를 보면 가죽과 밑창을 각각 공장 인스턴스에서 받아 조립하고 있음을 볼 수 있다.</br>
여기에서 주목할점은 Shoes 클래스는 그냥 공장에서 건네주는 재료로 신발을 조립만하기 떄문에, 어떤 지역의 팩토리를 사용하든 Shoes 클래스는 언제든 재활용할 수 있다는 것이다.
```java
abstract class ShoesStore {
 
    public Shoes orderShoes(String name) {
 
        Shoes shoes;
 
        shoes = makeShoes(name);
        shoes.assembling();
        shoes.prepare();
        shoes.packing();
 
        return shoes;
 
    }
 
    abstract Shoes makeShoes(String name);
 
}
```
고객에게 주문을 받을 수 있는 Store 클래스를 만들어 보았다.</br>
각 나라의 스토어들은 이 Store 추상 클래스를 상속받아 추상 메서드인 makeShoes 메서드를 각 나라에 맞게 오버라이드하여 구현해주면 된다.</br>
orderShoes는 전세계 공통 프레임워크이고, orderShoes안에 있는 makeShoes단계만 각 나라의 특징에 맞게 바뀌는 것뿐이다.
```java
class JPShoesStore extends ShoesStore {
 
    @Override
    Shoes makeShoes(String name) { 
        Shoes shoes = null;
        ShoesIngredientFactory shoesIngredientFactory = new JPShoesIngredientFactory();
        
        if(name.equals("blackShoes")) {
            shoes = new BlackShoes(shoesIngredientFactory);
            shoes.setName("일본 스타일의 검은 신발");
        }
        else if(name.equals("brownShoes")) {
            shoes = new BrownShoes(shoesIngredientFactory);
            shoes.setName("일본 스타일의 갈색 신발");
        }
        else if (name.equals("redShoes")) {
            shoes = new RedShoes(shoesIngredientFactory);
            shoes.setName("일본 스타일의 빨간 신발");
        }
 
        return shoes;
    }
 
}
```

```java
class FRShoesStore extends ShoesStore {
 
    @Override
    Shoes makeShoes(String name) { 
        Shoes shoes = null;
        ShoesIngredientFactory shoesIngredientFactory = new FRShoesIngredientFactory();
        
        if(name.equals("blackShoes")) {
            shoes = new BlackShoes(shoesIngredientFactory);
            shoes.setName("프랑스 스타일의 검은 신발");
        }
        else if(name.equals("brownShoes")) {
            shoes = new BrownShoes(shoesIngredientFactory);
            shoes.setName("프랑스 스타일의 갈색 신발");
        }
        else if(name.equals("redShoes")) {
            shoes = new RedShoes(shoesIngredientFactory);
            shoes.setName("프랑스 스타일의 빨간 신발");
        }
 
        return shoes;
    }
 
}
```
일본과 프랑스 신발 매장을 ShoesStore클래스를 상속받아 만들어주었다.</br>
각 매장은 makeShoes를 오버라이딩하여 현지 상황에 맞게 재정의한다.</br>
makeShoes내부 프로세스를 살펴보면, 먼저 매장으로 신발 주문이 들어오면 현지 공장 인스턴스를 생성한다.</br>
그리고 매장에서 신발 재료 팩토리 인스턴스를 보내서 원재료 공장으로부터 재료들을 모두 받아오는 것이다.</br>
makeShoes 메서드에서 재료를 공장에서 모두 받아왔다면, 이제는 매장에서 받은 재료를 가지고 조립하고, 준비, 포장하여 작업을 마무리 하는 것이다.</br>
위 고정이 전세계 공통 orderShoes 프레임워크이다.</br>
이제는 신발공장과 매장, 신발까지 모든 설계가 마무리 되었다.</br>
실제 주문을 하는 과정을 살펴보며 이번 추상 팩토리 패턴을 마무리하려고 한다.
```java
public class Main {
 
    public static void main(String[] args) {
 
        JPShoesStore jpStore = new JPShoesStore();
        jpStore.orderShoes("blackShoes");
 
        FRShoesStore frStore = new FRShoesStore();
        frStore.orderShoes("redShoes");
 
    }
 
}
```
위 주문 코드를 실행해보면 출력은 아래와 같을 것이다.
```
> 신발을 제작중입니다. 일본 스타일의 검은 신발
> 신발 정보 : 밑창은 고무 사용 하였으며, 가죽은 소가죽 사용하였습니다.
> 완성된 신발을 준비 중입니다.
> 준비된 신발을 포장 중입니다.
> 신발을 제작중입니다. 프랑스 스타일의 검은 신발
> 신발 정보 : 밑창은 플라스틱, 고무 사용 하였으며, 가죽은 양가죽 사용하였습니다.
> 완성된 신발을 준비 중입니다.
> 준비된 신발을 포장 중입니다.
```
>일본 매장과 프랑스 매장으로 가서 신발를 주문을 한다고 하자.</br>
>먼저 주문하는 일본 매장에서 검은 신발을 주문하면, 매장에서는 주문을 받고 (orderShoes)</br>
>주문을 받은 직원은 일본 매장을 담당하는 원재료 공장에 해당 신발에 알맞는 재료를 요청한다. (makingShoes)</br>
>원재료 공장이 가동되고, 구두의 재료를 제작하여 보내준다.</br>
>매장에서 재료들을 받아서 조립을 해서 구두를 만든다.</br>
>준비, 포장을 해서 고객들에게 제공한다.</br>
>프랑스 매장도 마찬가지로 일본 매장과 완전히 동일한 프로세스를 거쳐 고객에게 신발을 제공한다.
 
 <img src="https://github.com/dltkd1395/CS-study/blob/main/DesignPattern/image/AbFactory1.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

 마지막으로 위 이미지를 그동안 예시를 들었던 신발 매장 패턴을 대입하여 추상 팩토리 패턴을 이해하고 정리하면 좋을 것같다.</br></br>
결과적으로, 추상 팩토리 패턴을 사용하면 DIP 원칙을 준수하게되어 객체들 간의 결합도 낮아져서 유지 보수가 아주 용이해진다.

[맨위로](https://github.com/dltkd1395/CS-study/tree/main/DesignPattern#design-pattern)

---

## Singleton
- 싱글톤 패턴(Singleton Pattern)이란 - 여러 차례 호출되더라도 실제로 생성되는 객체는 하나이고 최초 생성 이후에 호출된 생성자는 최초의 생성자가 생성한 객체를 리턴하는 생성패턴이다.
> - 클래스 내에서 인스턴스가 단 하나뿐임을 보장하므로, 프로그램 전역에서 해당 클래스의 인스턴스를 바로 얻을 수 있고, 불필요한 메모리 낭비를 최소화한다.
> - 키보드 리더, 프린터 스풀러 또는 공통된 객체를 여러개 생성해서 사용하는 DBCP(Database Connection Pool)등 클래스의 객체를 하나만 만들어야 하는 상황에서 사용한다.
> - 싱글톤 패턴을 사용하기 위해서는 반드시 접근제한자를 이용하여 외부의 접근을 막건, final로 reference를 변경 불가능하게 설정하여야 한다.

```java
public class Singleton1 {

    private static final Singleton1 instance = new Singleton1();

    private Singleton1() {}

    public static Singleton1 getInstance() {
        return instance;
    }
}
```

```java
public class Singleton2 {
    private static Singleton2 instance;

    private Singleton2() {}

    public static Singleton2 getInstance() {
        if (instance == null) {
            instance = new Singleton2();
        }
        return instance;
    }
}
```

[맨위로](https://github.com/dltkd1395/CS-study/tree/main/DesignPattern#design-pattern)