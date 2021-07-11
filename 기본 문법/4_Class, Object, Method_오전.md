## 4_Class, Object, Method 오전



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
package com.minki;

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
package com.minki;

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



##### 방송사고

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





##### 클래스 만들어보기

```java
package com.minki;

public class Phone {
    public String name = "Iphone12 Pro";
    public char color;
    public int price;
    
    public int getRealDebt() {
        // return 10000;
        return price + 200;
    }
}
```



```java
package com.minki;

public class PhoneTest {
    
    public static void main(String[] args) {
        Phone phone = new Phone();
        phone.name = "Iphone12 Mini";
        phone.color = 'B';
        phone.price = 20000;
        
        int i = phone.getRealDebt();
        System.out.println(i);
        
        Phone phone2 = new Phone();
        phone2.name = "Iphone11 Pro";
        phone2.color = 'P';
        phone2.price = 10000;
        
        System.out.println(phone2.getRealDebt());
    }
}
```





#### PhoneTest in Memory

```java
package com.minki;

public class PhoneTest {
    
    public static void main(String[] args) {
        
        Phone phone = new Phone();
        
        phone.name = "Iphone12 Mini";
        phone.color = 'B';
        phone.price = 20000;
        
        int i = phone.getRealDebt();
        System.out.println(i);
    }
}
```



##### stack 

- Phone phone = new Phone();

  ​	phone -> `1000`



##### heap

- phone.name = "Iphone12 Mini";

  1000 -> name -> `2000`

  2000 -> `Iphone12 Mini`



- phone.color = 'B';

  1000 -> color -> `'B'`



- phone.price = 10000;

  1000 -> price -> `10000`





#### 주제 #03 Class 사용하기

Class로 Object 만드는 과정 `Phone phone = new Phone();`

Class Type으로 변수를 선언하고, new라는 keyword를 사용하는데, 

그 뒤에는 생성자(Constructor)가 온다.



new -> 뒤의 생성자를 보고 그에 맞게 memory allocation을 수행한다.

memory allocation -> heap이란 공간에 위치를 잡아준다.



질문) 앞의 Phone을 보고 나서 생성자(Phone)을 만드는 건가요?

답변) 아님! memory allocation은 뒤의 Phone을 보고 만든다.



생성자(Constructor)는 Class 이름 + () 구조를 가지고 있다.

method와 비슷하게 생겼다. 근데 우리는 생성자를 만들지는 않았다.



그럼 Phone()이라는 생성자는 어떻게 호출되는 것일까?





#### 주제 #04 생성자 이해하기

만약 Class가 제공하는 생성자가 없을 경우, 즉 Class를 만들 때, 아무런 생성자를 만들지 않으면, Compiler가 기본생성자(Default Constructor)를 자동으로 만들어준다. 기본 생성자는 Parameter가 없는, 특별한 작업을 수행하지 않는 가장 단순한 생성자이다. ` new Phone () { X }`



if) 내가 생성자를 만들어주면? -> Compiler는 아무런 생성자를 만들어주지 않는다.



생성자는 Parameter를 가질 수 있다. 그리고, Parameter를 달리 하는 여러 개의 생성자를 만들 수 있다. 생성자가 여러 개 제공되면, 외부에서는 다양한 방법으로 객체를 만들 수 있게 된다. Class는 생성자의 Parameter를, 객체를 생성할 때 사용한다. 보통은 member variable들의 값을 설정한다.





#### 주제 #05 생성자 추가하기

Phone Class에 생성자 추가하기

name Parameter를 가지고, 생성자 안에서 member variable name에 Parameter name을 넣도록 한다. 그렇게 하면 Phone Class를 외부에서 만들 때, 적절한 이름(name)을 제공할 수 있다.



```java
package com.minki;

public class Phone {
    public String name = "Iphone12 Pro";
    public char color;
    public int price;
    
    public int getRealDebt() {
        return 10000;
        // return price + 200;
    }
    
    public Phone(String name) {
        this.name = name;
    }    
}
```



```java
public Phone(String name) {
    this.name = name;
}   
```
public -> modifier

Phone class에서 사용할 parameter를 String 으로 name 으로 준다.

this.name = name

this: 자기 자신(만들어진 객체 자신) 

[this가 쓰이기 위해선 객체가 먼저 만들어져야 한다.]

[객체는 PhoneTest에서 만들었쥬?]

[객체가 만들어짐 -> 객체 메모리공간 할당이 이루어짐 -> this.을 쓸 수 있다.]

앞 name: Object Reference. 만들어진 객체의 이름

뒤 name: Parameter. 파라미터로 전달된 이름





##### name parameter 생성자 추가하기

위 위 코드를 입력 -> PhoneTest에서 오류 발생





#### 주제 #05 생성자 추가하기

Phone Class에 생성자 추가 -> Default Constructor를 compiler가 넣지 않았다.

-> `Phone phone = new Phone();`에서 사용하는 Parameter가 없는 생성자는 Phone class에 없다.



#### 주제 #05 생성자 추가하기 - 기본 생성자

```java
public Phone() {}
```

오류 해결!





#### 주제 #06 다른 생성자로 객체 만들기

Phone Class에 생성자 2개 있쥬? 각각의 생성자를 이용해서 Phone 객체를 만들어 보자.



PhoneTest.java

```java
		Phone phone = new Phone("S21");
		Phone phone2 = new Phone();
```



Phone.java

```java
    public String name = "Iphone 12 Pro";
    public char color;
    public int price;
    
    public int getRealDebt() { // 할부원금
//      return 10000;
    	return price + 200;
    }
       
    public Phone(String name) {
    	this.name = name;
    	System.out.println("A");
    	System.out.println(this.name);
    }
    
    public Phone() {
    	System.out.println("B");
    	System.out.println(this.name);
    }
```



result

```
A
S21
B
Iphone 12 Pro
```





#### 주제 #07 생성자 앞 public

생성자 앞의 pubblic modifier -> 외부에서 생성자를 호출할 때, 아무런 제한이 없다는 의미.

특별한 경우 modifier를 이용하여 생성자 호출 제한 가능 [Access Modifier]





#### 주제 #08 member variables

Phone Class의 예시로 보면, Iphone12 Pro와 S20은 이름이 다른 객체가 될 수 있고, 같은 폰 객체 중에서도 색상이 다를 수 있으며, 가격은 수시로 변동될 수 있다.



Class를 이용해서 Object들을 만든다는 건, 표현해야 할 대상이 존재한다는 것이다.

member variables를 통해 그 대상의 다양한 상태를 표현한다.



결국, 객체는 처음 만들어질 때, member variables들이 값을 가지게 되고, 프로그램 안에서 필요에 따라 그 값은 변할 수도, 변하지 않을 수도 있다.



#### 주제 #08 member variables Set

member variables 값을 부여하는 방법엔 여러 가지가 있다.



Class를 정의하면서 할 수도 있고,

```java
    public String name = "Iphone 12 Pro"; // -> 요거!
    public char color;
    public int price;
```



생성자의 Parameter에 값을 전달하는 방법도 있고,

```java
Phone phone = new Phone("A");
```

```java
public Phone(String name) {
    this.name = name;
}
```



객체를 만든 후에 직접 값을 부여할 수도 있다.

```java
Phone phone = new Phone();
```

```java
phone.name = "Galaxy Note";
phone.color = 'B';
phone.price = 20000;
```



##### 만약 member varibales 값을 설정하지 않으면?

- {} 안에 선언된 Local Variable은 사용 전에 값을 설정해야만 했다.
- Class 안에 선언된 member variable은 new를 통한 객체가 생성될 때 기본 값(Default Value)이 자동으로 부여된다. [0이나 0에 준하는 값. String같은 Object type은 null]



##### 그런데...

member variables 값을 외부에서 직접 Set할 수 있다?

OOP는 Object 중심인데, 외부에서 Object의 member variables를 맘대로 바꾼다?



OOP에서 member variables의 Set은 외부에서 마음대로 할 수 없도록, Class 내부에서 제어할 수 있는 구조를 가지는 게 일반적이다.



##### By 생성자 
-> 좋다.

```java
Phone phone = new Phone("A");
```

```java
public Phone(String name) {
    this.name = name;
}
```



##### By Direct 
-> 외부에서 바로 바꿔버리는 건 OOP적 관점에서 좋지 않다.

```java
Phone phone = new Phone();
```

```java
phone.name = "Galaxy Note";
phone.color = 'B';
phone.price = 10000;
```





#### Encapsulation

OOP의 특징 중 하나로, Class를 구성할 때, 기본적으로 멤버 변수와 메소드를 외부에 노출하지 않도록 가정하고, 필요한 경우에 한해, 외부에 노출하는 것을 의미한다.

외부에 노출할 경우, Setters & Getters를 제공하여 외부와 소통한다.

접근제한자(Access Modifier)를 이용하여 외부에 어느 정도 노출할 것인지를 결정한다.





#### 주제 #09 member variables Setters

member variables 값을 외부에서 마음대로 접근할 수 없도록 하고, 대신 member variables 하나에 대해 값을 Set할 수 있는 특별한 method를 제공할 수 있다.

이를 통해, 외부에서는 member variables의 값을 변경 요청하게 되고, Class 내부에서는 이 method 안에서 요청에 대한 처리를 수행하면 된다.

이러한 method들을 Setters라고 부른다.



##### By 생성자 

```java
Phone phone = new Phone("A");
```

```java
public Phone(String name) {
    this.name = name;
}
```



##### By Setters

```java
Phone phone = new Phone();
```

```java
public void setName(String name) {
    this.name = name;
}
```



바꿔 줄래? 하고 물어보는 거랑, 바꿔버리는 거랑 다르다.



Getter, Setter -> 아주 보편화된 Encapsulation의 방법 중 하나

외부에서 Getter, Setter를 통해 의뢰를 할 수 있고, 결정은 코드 내에서 하는 구조를 가져간다.





#### 주제 #09 member variables Setters

값을 가져갈 때



외부에서 값을 읽고자 할 때, 직접 읽지 않고 별도의 method를 제공하는 데 이러한 method들을 Getters라고 부른다.



Getters를 통해 외부에서는 Object의 member variables의 값을 읽을 수 있다.



##### By Getters

```java
public String getName() {
    return name;
}
```

```java
Phone phone = new Phone();
System.out.println( phone.getName() );
```

##### phone.name(X)

이렇게 사용할 수 없도록 만들어야 한다.

 getters를 통해서만 값을 가져갈 수 있도록 해야





#### 주제 #10 private member variables

Setters를 제공했따고 모두 끝난 건 아니다.

여전히 member variables에 대해 외부에서 직접 Access할 수 있다.



이제 Setters를 제공하므로 외부에서 member variables에 직접 접근할 수 없도록 막아야 한다.



member variables 앞에 있는 modifier를 public -> private로 변경해주면 된다.



##### private member variables

```java
public class Phone {
    private String name;
    private char color;
    private int price;
}
```



##### Direct Set Error

```java
phone.name = "Galaxy Note";
phone.color = 'B';
phone.price = 10000;
```



#### Setters & Getters 포함 코드

```java
public class Phone {

	private String name = "Galaxy Note";
	private char color;
	private int price;

	public int getRealDebt() { return 1000; }

	public Phone(String name) { this.name = name; }      
	public Phone() {}

	public String getName() { return name; }
	public void setName(String name) { this.name = name; }

	public char getColor() { return color; }
	public void setColor(char color) { this.color = color; }

	public int getPrice() { return price; }
	public void setPrice(int price) { this.price = price; }
}  


public class PhoneTest {
	public static void main(String[] args) {

		Phone phone = new Phone();
			
		phone.setName("Galaxy Note");
		phone.setColor('B');
		phone.setPrice(10000);

		System.out.println( phone.getRealDebt() );
		System.out.println( phone.getName() );
		System.out.println( phone.getColor() );
		System.out.println( phone.getPrice() );
  }
}
```



result

```java
1000
Galaxy Note
B
10000
```





#### 똑같은 거 아닌가요?

Phone Class에서는 Setters와 Getters를 통해서 외부에서 모든 멤버변수에 접근할 수 있다.

결과적으로 직접 노출하는 것과 동일해 보인다.

-> Phone Class가 매우 단순한 구조이기 때문이다.



외부에서는 Setters와 Getters를 통해서만 변경되도록 코드를 작성해야, 이후에 처리 로직이 변경되는 경우에 쉽게 대응할 수 있다.



setㅁ

getㅁ



Phone class     | A | B | C

public name 	 p.name = " "

-> private            setㅁ



A, B, C가 name을 막 바꾸는게 아니라 setters, getters를 통해 의뢰를 한다. [setters, getters의 역할]



##### Cilent <-> Controller Layer <-> Service Layer <-> DAO[Data Access Layer]  <-> DB[Database]



##### Service Layer의 비즈니스 로직 구현

팀마다 하나씩 맡겠쥬?

A, B...

DAO는 C, D팀이 맡으십쇼

이 팀들이 다양하게 얽히겠쥬?



이 때 코드 레벨의 디커플링이 굉장히 중요하다.

서로 의존도가 지나치게 높아버리면..한 쪽이 수정되면 수정된 내용에 영향을 받아 나도 무언가 해야 한다.) ㅠㅠ



플젝 커지면..

Client 엄청나게 다양한 요청 -> controller가 처리해야  -> Service Layer 에서 A, B가 만든 서비스 호출

이 Service Layer의 메소드들은 public으로 되어있어야 하고`public method(){ X }`, 메소드 안에서 모든 것들을 처리

멤버 변수같은 것들은 Encapsulation. 숨겨놔야 함.

그래야 메소드 호출을 통해서만 값 변경, 호출.

이런 구조로 되어 있어야 한 쪽에서의 변경 사항이 다른 쪽에 영향을 최소로 미친다.





-> Setters와 Getters의 구조를 가져가야 한다.

-> 서로간의 영향도를 줄일 수 있다.

-> 변화에 대응하기 쉬워진다.



