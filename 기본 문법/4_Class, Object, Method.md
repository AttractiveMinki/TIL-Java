## Java 기본 문법 응용 Array



오늘의 포인트

- Java의 OOP 기본
- 코로나 연구실





#### OOP 4대 특징

- Encapsulation 캡슐화
  - 하나의 클래스 안에 데이터와 기능을 담아 정의하고, 중요한 데이터나 복잡한 기능 등은 숨기고, 외부에서 사용에 필요한 기능만을 공개하는 것.
- Inheritance 상속
  - 객체 정의 시 기존에 존재하는 객체의 속성과 기능을 상속받아 정의하는 것
- Polymorphism 다형성 [접두사 Poly: 다양한, 많다라는 뜻. mono{하나}와 반대되는 개념] 
  - 같은 타입 또는 같은 기능의 호출로 다양한 효과를 가져오는 것
- Abstraction 추상화 <-> 구체화
  - 현실 세계에 존재하는 객체의 주요 특징을 추출하는 과정
  - (버릴 건 버리고 필요한 부분만 특징지어주는 부분.. 구분 어렵쥬)



OOP 3대 특징이라 하면 Encapsulation을 버린다.





#### 주제 #01 Class vs Object

- Object [현실 세계에 존재하는 실체들간의 관계에서 파악되는 구체적인 것]
  - 시스템의 대상이 되는 모든 것. 시스템이 포함하고자 하는 대상
  - 구체적인 표현 대상이 있다. 학생 Object는 A학생, B학생 등을 표현
- Class
  - 구체적인 Object들을 분석해보고 공통적인 내용들을 **추상화**해서 Programming 언어로 표현한 것
  - 저 학생은 굉장히 많은 특징을 갖고 있지만, 학사관리 시스템에서는 이러이러한 것들만 관리하면 되겠군!
  - 구체적인 Object가 가지고 있는 많은 것들 중에서 나의 관점의 추상화를 통해 걸러냄



현실 세계의 Object들을 분석해서 Class로 정의한다.

시스템의 대상이 되는 현실 세계의 Object들을 분석한 다음, 그들을 어떤 기준에 의해, 분류(Classify)를 하는 것이 먼저 해야 할 일

면티, 바지, 아이폰, 삼성 PC, HP PC

분류하기

옷, 전자제품

2개의 class!



#### 주제 #02 Class 만들기

Class 만들기 전에 생각해야 하는 것 2가지

- 정적인 특성(attribute), 동적인 특성(behavior)



핸드폰(object) - 아이폰 프로 12

쇼핑몰 -> 이름, 색상, 가격, 할부원금

제조관리 -> Serial No, 재질, 조립 상태, 불량 확인



동일한 object라도 관점에 따라 파악하고자 하는 게 다르다.



##### Java로 Class 만드는 법

```java
package com.ssafy;

public class Phone {
    public String name;
    public char color;
    public int price;
    
    public int getRealDebt() { // 할부원금
        return 10000;
    }
}
```

public -> Modifier

Phone -> **Class Name**

4 ~ 6번째 줄 [name, color, price] -> attributes **(member variables)**

8 ~ 10번째 줄 [getRealDebt] -> behavior **(methods)**



OOP -> attributes, behavior

Java -> member variables, methods [클래스가 가지고 있는 것이기 때문에 function이라 부르지 않고 메소드라 부른다.]





#### 주제 #03 Class 사용하기

Class 사용하는 코드 작성

```java
package com.ssafy;

public class PhoneTest {
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		Phone phone = new Phone();
		
	    phone.name = "Galaxy Note";
	    phone.color = 'B';
	    phone.price = 10000;
	    
	    System.out.println( phone.getRealDebt());
	}
}
```



PhoneTest란 Class를 만든다.

main method도 class 안에 들어가야 한다.

Phone, PhoneTest 별도의 클래스(파일) 만들 예정



##### public static void main(String[] args) {

- JVM이 시작되는 Entry Point
- PhoneTest란 이름을 가지고 메모리에 load
- main method 찾아서 호출 -> VM이 수행하는 코드들이 하나씩 실행



##### Phone phone = new Phone(); [ Object new Constructor]

- 타입(Phone)이 클래스 이름

- primitive type이 아닌 reference type을 본격적으로 학습
- Phone class 타입의 변수 선언
- Constructor - 객체를 생성해주는 녀석(나중에 자세히)



방송사고

36:34 -> 1:20:20 이동

대충 36:34, 2:10:04 비슷



int i = 10;

-> i 사용하는건 10쓰는 것과 같다.

##### phone p = new Phone();

p 안에 phone 넣을 수 없다.

바로 p 쓸 순 없고, p. 이라고 해야 Phone 안에 있는 name같은 애들에 접근 가능

p.name, p.color. p.price

멤버 변수들에게 값 할당



##### phone.getRealDebt()

메소드 호출











