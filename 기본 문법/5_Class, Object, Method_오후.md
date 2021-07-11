## 5_Class, Object, Method 오후





#### Getters와 Setters 만들기

eclipse 실행

오른쪽 클릭 -> Source -> Generate Getters and Setters

세 개의 멤버 변수들 자동으로 표시가 되죠? [color, name, price]

Select All

Access modifier도 public으로 설정한 뒤 Generate



getName

setName

대문자 앞에 위치하는거 보이쥬 [Naming Convention, 표기법]

클래스같은 경우는 맨 앞도 대문자(PhoneTest)



만약 getNameValue, setNameValue 이런 식으로 만들었다면?

코드 바깥에서는 이를 알 수 없다,,

외부에서 Phone이란 녀석의 객체를 만듦 [Property]

멤버 변수 name은 hide되어 있고, 외부로 노출되는 이름은 

getNameValue, setNameValue

-> Phone이란 녀석의 Property는 NameValue가 된다.

모듈간 인식하는 과정에서 Setter, Getter 대충 만들면 이런 오류 발생할수도

실제 네임 != Property -> 혼선





#### 주제 #11 methods

Object의 동적인 특징을 표현하는 **methods**에 대해 조금 더 살펴보자.

앞에서 본 Setters & Getters도 methods이다.



동적인 특성은 뭔가 움직인다 라는 의미가 아니라, 수행 또는 처리되는 **Code Block**을 가질 수 있다는 의미입니다. Class 내부에서, 또는 Class 외부에서 호출(**Call**)할 수 있다.



member variables에 비해, methods는 조금 더 복잡한 구조를 가진다.



멤버 변수는 정적인 상태 값을 표현한다고 하면, 메소드는 주로 어떤 기능을 수행하는 부분을 감당한다.





#### 주제 #11 methods 구성

- return type
  - int, char, ..., String, Phone, Array, void
  - 없거나, 하나
- parameter type
  - int, char, ..., String, Phone, Array, ()
  - 없거나, 하나, 여러 개
- {} block
  - 수행 Code
  - return 하거나, 안 하거나



참고)

int, char -> primitive type

String, Phone -> reference type

Array -> 위 type의 Array...

```java
public int getRealDebt() {
    return 10000;
}
```

```java
public void setColor(char color) {
    this.color = color;
}
```





#### 주제 #12 methods - 호출

```java
Phone phone = new Phone();

phone.setName("Galaxy Note");
phone.setColor('B');
phone.setPrice(10000);

int realDebt = phone.getRealDebt();
System.out.println( realDebt );
```



##### methods는 다음과 같이 호출한다.

##### object + . 

-> heap 공간에 object 만들어진다. 만들어진 그 객체를 가리킨다.



다른 언어의 address는 Virtual Machine이 없음 -> real 머신에서의 address [ex) C언어] -> 실제 물리적인 언어

Java -> 실제 물리적인 Machine에서 동작하지 않음 -> JVM 위에서 동작 -> VM에 메모리 구조가 있다.

Real Machine 위에 가상의 기계 JVM이 있다.



프로그램은 Real Machine 위에서 동작한다. JVM의 코드에 의해서

우리의 관심 -> VM 위의 소프트웨어적으로 구현된 메모리 공간



##### object + . + method name + ( parameters )

파라미터 조심!



##### variable = object + . + method name + ( parameters )

int realDebt = phone.getRealDebt();



메소드 호출 시 `.`을 사용하여 레퍼런싱 후 기술되어 있는 메소드 호출



만약 

`Phone phone = new Phone()`에서 뒤의 new 이하 코드 작성하지 않음

-> Phone phone 객체가 만들어지지 않은 상태

-> 실제론 존재하지 않는 변수만 선언된 null 형태

-> .으로 가리킬 시 nullPointException이 발생할 수도.





#### 주제 #12 method 추가

Phone Class에 getSalePrice() method를 추가해 보자.

만약, color == 'A'인 경우에는 price 값을, 그렇지 않은 경우는 price + 1000을 return 하도록 해보자.

```java
public class Phone {
    private String name = "Iphone 12 Pro";
    private char color;
    private int price;
    
    public int getRealDebt() { return 1000; }
    
    public int getSalePrice() {
        if( this.color == 'A' ) {
            return this.price;
        }
        else {
            return this.price + 1000;
        }
    }
}
```

```java
Phone phone = new Phone();

phone.setName("Galaxy Note");
phone.setColor('B');
phone.setPrice(10000);

System.out.println( phone.getSalePrice() );
```





DTO(Data Transfer Object)

VO(Value Object)

멤버 변수, setters, getters 가지는 형태로 많이 사용한다.



굉장히 다양한 클래스가 있다.





#### 보충 #01 Array of Object

`int [] intArray = new int[5]`

위의 Primitive Type처럼 객체(Reference Type)도 배열(Array)로 만들 수 있다.

```java
phone [] phoneArray = new Phone[5];

for( int i = 0; i < phoneArray.length; i++) {
    phoneArray[i].setPrice(i * 2000);
}

for( Phone phone : phoneArray ) {
    System.out.println( phone.getPrice() );
}
```

-> java.lang.NullPointerException 발생



`phone [] phoneArray = new Phone[5];`

아직 오른쪽 객체를 만들지 않았다.

객체를 가리킬 수 있는 변수들만 만들었다.

ㅁ -> ㅁ(X)

ㅁ -> ㅁ(X)

ㅁ -> ㅁ(X)

ㅁ -> ㅁ(X)

ㅁ -> ㅁ(X)



`phoneArray[i].setPrice(i * 2000);`

객체를 가리키지 않으니 null -> 객체에 접근하려 해서 오류 발생



```java

Phone [] phoneArray = new Phone[5];

for( int i = 0; i < phoneArray.length; i++) {
    phoneArray[i] = new Phone();
    phoneArray[i].setPrice(i * 2000);
}

for( Phone phone : phoneArray ) {
    System.out.println( phone.getPrice() );
}
```



객체를 만들어준 다음에 setPrice를 하자!



아.. null pointer exception 발생 -> 어떻게 대응할 것인가

에러 발생 라인 번호 가서 .부분(referencing)을 찾아야 한다.

그 녀석이 null인지 아닌지 확인





#### 보충 #02 JVM Memory Overview

Java는 High-Level Language로 Memory Management로부터 자유롭다. [장단점 존재]

- 다른 언어 -> Memory allocation, deallocation을 직접 한다. [JVM 고려하지 않은 C언어와 같은 컴파일러 언어]
  - Real Machine의 Memory Management를 실제 코드가 직접 한다.
  - Deallocation도 직접 해야 한다.
  - 굉장히 어려운 일
  - 메모리 관리를 잘못 함 -> 윈도우로 치면 블루스크린과 같은 예기치 않은 문제 발생할수도



- Java는 new하고 나면 만들어짐
  - garbage collector -> 자동으로 Memory Management 해준다. 정리 해준다.
  - 특정 Object가 사용하던 공간. 사용하던 Object의 reference가 사라짐 -> garbage collector가 알아서 정리
  - 모았다가 진행하는 등 다양한 방식
  - 빠르게 메모리를 확보하진 못해서 순간순간 늦어질 수 있는 단점



그래도 알아두어야 할 몇 가지 내용들을 살펴보자.



JVM은 주요하게 3개의 메모리 영역을 가지고 있으며, 그 용도는 아래와 같다.



- Class Area(Method Area)
  - for Class, Static, Method



- Heap
  - for Objects

new 의 오른쪽에 있는 애들은 전부 힙에 만들어진다고 생각하면 됨



- Stack
  - for Call

method call 하게되면, 스택에 method call이 되면 해당 method를 위한 스택 공간이 따로 마련된다.

다른 메소드 호출 -> 스택 안에 방금 호출된 메소드의 공간 안에서 변수 등 작업

마지막으로 호출 된 메소드 종료 -> 해당 스택 클리어 -> 바로 위에 호출했던 스택에 가서 수행

종료하면 또 사라지고 위의 스택 실행..



Q) 재귀 호출

탈출 조건 제대로 안쓰면 어디 메모리에 문제가 생길까?



A) 스택

스택에 메소드가 호출되자너

메소드 호출 부분 -> 스택에 만들어짐

특정 시점에 멈춰야되는데 그게 안 됨 -> 무한반복 -> VM 공간 내주다가 거덜남 -> stack overflow





#### Code 중심으로 Memory 파악하기

```java
public static void main(String[] args) {
    int i = 10;
    String s1 = "Hello";
    String s2 = new String("World");
    Phone phone = new Phone("S20");
    
    System.out.println(i);
    System.out.println(s1);
    System.out.println(s2);
    System.out.println(phone);
}
```



##### Class Area, Heap, Stack



1. Class Area -> MemoryTest
2. Stack -> i = 10
3. Class Area -> String, Stack -> s1
4. Heap -> 1000, "Hello"
5. Stack -> 1000 [힙 가리킴]
6. Stack -> s2가 만들어진다.
7. Heap -> 2000, "World"
8. Stack -> 2000 [힙 가리킴]
9. Class Area-> phone
10. Stack -> phone
11. Heap -> 3000, "S20"
12. Stack -> 3000



primitive type i는 만들어지면 stack 안에 자기 자신의 값을 가지지만,
s1, s2, phone은 위치 정보를 갖는 형태로 만들어진다.





#### 보충 #03 Garbage Collection

C, C++ 해봤으면 Memory Management 얼마나 힘든지 알쥬?



Java -> new 연산자를 통해서 Memory Allocation을 수행하지만, Deallocation은 JVM이 알아서 처리한다.

JVM은 Heap에 만들어진 객체 중 더 이상 참조되지 않은 것들을 대상으로 적절한 시점에 Garbage Collection 작업을 수행한다.

3가지를 기억하자.

1. 우리는 Garbage Collection에 직접 관여할 수 없다.
2. 자동으로 처리된다는 점은 Coding 관점에서는 장점이지만, 운영 관점에서는 단점이 된다.
   - Software Engineer 말고 System Engineer 입장에서 보면.. 메모리 튀는 경우가 있다.
3. 불필요한 객체 생성을 지양한다.





#### 보충 #04 String Class

숫자나 문자 한 글자는 Primitive Type으로 선언과 동시에 값의 범위가 정해진다.

하지만, 우리가 가장 많이 사용하는 문자열은 본질적으로 가변적이기 때문에 Primitive Type으로 표현하기 어렵다.



Java에서 문자열은 Phone Class처럼 Class로 정의하고 기본으로 제공된다.

(java.lang package)



Primitive Type처럼 new 없이 바로 문자열을 값으로 줄 수도 있고, Reference Type처럼 new 연산자를 이용하여 값을 줄 수도 있다.

`String s = "Hello";`

`String s = new String("Hello");`

둘 다 Reference Type



```java
public static void main(String[] args) {
    int i1 = 10;
    int i2 = 10;
    
    String s1 = "Hello";
    String s2 = "Hello";
    String s3 = new String("Hello");
    String s4 = new String("Hello");
    
    if( i1 == i2 ) { System.out.println("i1 i2 same");}
    if( s1 == s2 ) { System.out.println("s1 s2 same");}
    if( s3 == s4 ) { System.out.println("s3 s4 same");}
}
```

```
i1 i2 same
s1 s2 same
```



##### 왜 s3과 s4는 같지 않을까

==는 두 변수의 memory 값을 비교한다.

i1과 i2는 local 변수이므로 Stack에 만들어지고, Primitive Type이므로 그 변수에 값이 저장됨.

s3과 s4는 각각 new에 의해 Heap에 서로 다른 객체를 생성하고 그 주소값을 저장

"Hello" <- 객체 상수(일종의 리터럴)로서 String Constant Pool에 관리(Heap에 만들어짐)되고, 재사용됨.

s1, s2가 같은 곳을 가리키게 된다.



new를 쓰면 heap에 무조건 allocation 따로 한다. 각자 만들어진다.

s3, s4 각각 다른 공간에 referencing -> ==로 비교시 다른 값이 나온다.





#### 문자열의 내용이 같은지 확인하려면?

String 객체의 equals() 를 이용

```java
public static void main(String[] args) {
    int i1 = 10;
    int i2 = 10;
    
    String s1 = "Hello";
    String s2 = "Hello";
    String s3 = new String("Hello");
    String s4 = new String("Hello");
    
    if( i1 == i2 ) { System.out.println("i1 i2 same");}
    if( s1 == s2 ) { System.out.println("s1 s2 same");}
    if( s3 == s4 ) { System.out.println("s3 s4 same");}
    if( s3.equals(s4) ) { System.out.println("s3 s4 Same");}
}
```

```
i1 i2 same
s1 s2 same
s3 s4 Same // [4번째 내용]
```



equals 메소드는 String class에 있다. 미리 만들어져 있음.

s1.equals(s2), s1.equals(s3)도 가능!



##### 우리는 자주 복수개의 String을 이어서 새로운 String을 만들게 된다.

`+` operator를 사용하는 방법과 StringBuilder를 사용하는 방법을 알아보자.

`+` operator를 이용하면 그만큼 String 객체가 새로 만들어진다. 불필요한 객체가 많이 만들어져서 성능에 영향을 미칠 수 있다.

간단한 +의 나열은 compiler가 내부적으로  StringBuilder를 사용해 처리한다. 하지만, Loop 등의 코드 안에선 그렇지 않다.



```java
public static void main(String[] args) {
    String s1 = "Hello";
    String s2 = "World";
    String s3 = s1 + ", " + s2;
    
    System.out.println(s3);
    
    StringBuilder sb = new StringBuilder("");
    sb.append(s1).append(", ").append(s2);
    System.out.println(sb.toString());
    
    String[] strArray = {"Hello", ", ", "World" };
    String str = "";
    for( String s : strArray ){
        str += s;
    }
    System.out.println(str);
    
    sb.setLength(0); // 현재 가지고 있는 메모리 공간 재활용
    for( String s : strArray ){
        sb.append(s);
    }
    System.out.println(sb);
}
```



StringBuilder 객체 만들고

append 해 가면서 새로운 문자열 만들기

array 쭉 채우다가 공간이 다 차면 새로운 array를 만든다.

객체(array)를 만드는 데 부담이 훨씬 줄어든다.

그냥 `+` 사용 -> 계속 만들어진다.

StringBuilder는 객체를 만드는 overhead 줄어든다.

성능 면 -> StringBuilder를 쓰는 게 좋다.



간단한 코드에서 + 사용은 ㄱㅊ

Loop같은 곳에서는 StringBuilder를 사용하는 것이 좋다.



##### sb.setLength(0); 

// 현재 가지고 있는 메모리 공간 재활용



Q) StringBuilder를 그냥 출력하는 것과 toString()으로 출력하는 것엔 어떤 차이가 있나요?

A) StringBuilder는 toString 메소드를 기본적으로 호출

toString -> append된 모든 문자열을 toString이 리턴해준다. String으로 받아서 println에 넣어줌.

println해서 그냥 sb를 전달해도 된다. [println에서 내부적으로 알아서 toString 메소드를 알아서 호출해서 결과를 출력]





#### 보충 #05 toString()

어떤 객체의 상태를 표현하는 가장 간단한 방법은 toString()이라는 method를 만드는 것.

toString() method는 객체를 만들면 자동으로 만들어지는데(사실은 **Object Class로부터 상속**) default로 객체의 주소 정보를 String type으로 return한다.

​	toString() -> 주소의 referencing 정보를 출력하는 녀석.

​	object 클래스를 상속받아서 아무것도 안 하면 그냥 똑같은 기능을 사용하는 것(재정의)

System.out.println(객체)로 객체를 전달하면, 객체의 현재 상태로 member variables의 값을 출력하려면 toString() method를 **재정의**하면 된다.

상속(Inheritance)을 학습하면서 재정의 부분을 다시 알아보자.







##### Phone Class에 toString() 추가하기 전, 후

```java
Phone phone = new Phone();

phone.setName("Galaxy Note");
phone.setColor('B');
phone.setPrice(10000);

System.out.println(phone);
```

`result: com.minki.Phone@6d06d69c`



```java
public String toString() {
    return this.name + " " + this.color + " " + this.price;
}
```

toString 호출하면 문자열이 리턴되도록 만듦

`result: Galaxy Note B 10000`





#### 보충 Pass By Value

Java에서 생성자 또는 method를 호출할 때, 전달되는 parameter의 값이 어떤 방식으로 전달되는지 생각해보자.



```java
package com.minki;

public class PassByValueTest {
	public static void main(String[] args) {
		int i = 10;
		setVal(i);
		System.out.println(i);
		
		Pass p = new Pass();
		p.val = 10;
		setVal(p);
		System.out.println(p.val);
	}
	
	public static void setVal(int x) { x = 5; } // x값만 변경, i에 영향 없음
	
	public static void setVal(Pass p) { p.val = 5; } // reference라 실제 값 변경
}

class Pass{
	public int val = 3;
}
```



result

```
10
5
```

1) i와 setVal 안의 x는 다른 값

2) p의 주소를 찾아가서 변경하기 때문에 바뀜



primitive type, reference type에 따라 이런 부분 고민해봐야

pass by value, pass by reference

자바는 기본적으로 value 개념

reference하는 애들 참조해서 갈 수 있다.





#### 학습 #01 package

한 개의 Java 파일에 모든 코드를 다 담을 순 없쥬? Module별로 나누어서 관리하는 게 일반적.

파일을 계층적(hierarchical) 구조로 관리하기 위해 폴더를 사용하듯, Java의 Class도 package라는 구조를 통해 계층적으로 관리한다.



보통 www를 제외한 도메인의 역순 구조를 많이 사용한다.

www.minki.com이 도메인이면, com.minki가 기본 package가 된다. 그 하위 package는 업무 구분 등으로 구성한다.



www.minki.com base -> com.minki

ERP -> com.minki.erp

ERP - 인사 -> com.minki.erp.hr

Data Warehouse -> com.minki.dw



package이름을 도메인 거꾸로 쓰는 방식으로 사용해서 클래스 이름의 중복을 피한다.

패키지 이름은 사실상 클래스 이름의 일부



Java Source(~.java) 맨 위에 package keyword를 사용하여 표현하며, 구분자는 dot(.)을 사용한다.

IDE에 따라 다르지만, eclipse 경우 src폴더 안에 해당 package 구분자에 맞게 폴더를 구성하여 관리한다.

compile된 ~.class 파일도 package 구분자에 맞게 폴더를 구성하여 생성된다.



어떤 프로젝트를 만들 때 자바의 클래스를 모듈화해야 한다 

-> 패키지부터 고민해야. 패키지 이름





#### 학습 #02 import

패키지 쪼개서 쓰면 관리하기 용이하다

갖다 쓸 땐 요 녀석의 패키지를 갖다쓰겠다는 키워드를 사용하게 됨 -> import



다른 package에 정의된 Java Module을 사용하고자 할 때는 import keyword를 사용한다.

import 다음에 package 명을 쓰면 된다.

만약 import를 사용하지 않으려면?

Java Module 앞에 package명을 붙여서 사용하면 된다.



com.minki.sub package를 만들고 SubClass.java를 만들어보자.



```java
package com.minki.sub;

import com.minki.Phone; // 패키지 import로 갖다쓴다.

public class SubClass {
    Phone phone; // Phone을 쓰기 위해 다른 패키지를 import 해줘야 함
}

package com.minki.sub;

public class SubClass {
    com.minki.Phone phone; // import 안하고 쓰기. Package명과 클래스 이름을 다 써주면 된다.
}
```



```java
package com.minki.sub;

import com.minki.*; // 여러 개 import도 가능

public class SubClass {
	Phone p = new Phone();
	com.minki.Phone p1 = new com.minki.Phone();
}
```



Class를 만들 때 Package에 입력하면 Package도 같이 만들어진다.





#### 학습 #02 java.lang.package

System.out.println의 System Class는 내가 만든 게 아닌데?

String Class도 아닌데?



Java에서 기본적으로 제공해서 따로 import하지 않아도 되는 package가 있다.

##### java.lang.package



이 package에 있는 Java Module은 import하지 않아도 된다.





#### 학습 #03 Access Modifier

저번에 member variables에 public 대신 private를 붙여서 Encapsulation을 구현해보았다.

public, private처럼 member variables 또는 methods 앞에 위치해서 외부의 Access를 제어하는 Keyword를 Access Modifier라고 하는 거고, 권한이 다 다르군

|   구분    | Same Class | Same Package | Sub Class | Universe |
| :-------: | :--------: | :----------: | :-------: | :------: |
|  private  |     O      |      X       |     X     |    X     |
| (default) |     O      |      O       |     X     |    X     |
| protected |     O      |      O       |     O     |    X     |
|  public   |     O      |      O       |     O     |    O     |



같은 클래스 안에선 다 access 가능

private는 같은 package여도 안 돼

SubClass -> 상속 -> 다음 주. 하위 클래스:상위 클래스의 protected, public만 접근 가능.

public은 어디에서나 접근 가능



헷갈리는 default, protected -> 상속 배우면서 자세히



