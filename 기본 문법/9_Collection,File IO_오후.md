## 9_Collection/File IO`_오후`



상속, 다형성, 인터페이스, method overwrite 쉽지 않을 듯..



 collection부터 하자.



오늘의 포인트

- Collection / Exception / File IO





#### Order #3 - package 생성

#### Order #4 - package 별 Class 생성

#### Order #5 - Organization Class





#### 많은 Class들... 관계들..

이후의 과정은 플젝 개념으로 진행 -> Class와 interface의 수도 많고, 또 Reference하는 관계도 많아진다.





#### <> Generic

객체를 여러 개 저장해야 할 경우가 많다.

우선 Array를 생각할 수 있는데, 속도는 빠르지만, index 제어 등 불편한 부분이 많다.



Collections API를 이용하면, 조금 더 편한 방법으로 객체의 집합을 관리할 수 있다.



이러한 Collection을 포함하여, Java에서는 무언가를 담는 Container를 만들 때, 담을 객체의 Type을 Dynamic하게 지정할 수 있는 방법을 제공한다.



Java 1.5부터는 Generic( <> )을 도입해서, Class Code 작성 시점에 임의의 (가령 `<T>` ) 타입을 사용하도록 하고, 그 Class를 사용하는 Code에서 <T> 대신 실제 사용하는 Type(가령 `<String>`)을 사용할 수 있도록 하였다.



환자 객체 여러 개를 저장할 수 있는 자료구조가 필요

지금까지 Array(객체) 많이 사용했다.

배열 -> role. i 같은 인덱스를 꼭 사용해야!

객체 add(), remove()

배열 찾아가서 조정하는 과정 많았을 듯.

배열 -> **low level한 자료구조.** (어느 언어에서나 대부분 지원) [인간의 사고와는 조금 떨어짐. machine의 구조]

직접 index를 가지고 memory reference를 찾아가면서.. 하고,

직접 assign하고, 제거

좀 불편하고 어려움



Collection 종류 굉장히 많다.

배열에 비해 high level

인간의 사고와 조금 더 가까움

객체 하나만 얻으면, 이 객체를 저장하고 관리할 수 있는 다양한 형태의 자료구조를 선택

선택 후 add, remove 하는 메소드 호출하면서 전달만 하면 됨

나머지는 컬렉션에 맡긴다.

컬렉션이 알아서 자기 성격에 맞는 자료구조에 따라서 내부적으로 구현이 되어 있다.

쉽게 배열 대신 쓸 수 있는게 컬렉션 -> 앞으로 컬렉션 많이 사용.



컬렉션 사용 시 Java 1.5부터 Generic이란 개념 도입

자료구조에 담으려고 하는게 어떨 땐 ★, ○, △이 될 수도 있다.

자료구조를 만드는 시점에 ★, ○, △ 다 담으려 하면..

자료구조안에 Type으로 ★, ○, △이 있어야 담기 가능.

★타입 배열, 변수가 있어야 ★을 담을 수 있다.



클래스 내 임의로 만듦 -> 각자 다 이상한 형태의 객체를 만듦

어떻게 다 자료구조에 담을 수 있을까

예전에 최상위 클래스 Object를 이용하는 방법이 있었다. -> 좀 불편

모든 Specific한 Type들을 코드(.java)파일을 만드는 시점에 다 받아들일 수 있는 일반화된 타입 정의 -> Generic



```java
<T>
```

<T>를 사용하는 시점에 <String>이라고 써주면, T가 String으로 바뀐다.



StringContainer - 제네릭 비사용시 알고 있는 일반적인 내용

```java
public class StringContainer {
	private String obj; // String type obj 선언
	
    public StringContainer(){}

    public String getObj() { return obj; } // Getter return String

    public void setObj(String t) { obj = t; } // Setter 받는거 String
}
```



StringContainer와 다르게 <T>가 있다.

```java
public class GenericContainer<T> { // 꺽쇠 표시 추가됨
    private T obj; // 구체적인 타입이었던 String이 T로 바뀌었다.
    // T가 Type을 의미하는 군
    public GenericContainer(){}

    public T getObj() { return obj; } // return type으로도 T가 쓰이고

    public void setObj(T t) { obj = t; } // parameter type으로도 T가 쓰인다.
} // 1.5 이전에는 불가
```



```java
public static void main(String[] args) {
    StringContainer sc1 = new StringContainer(); // String이란 Type 명시
    sc1.setObj("String"); // set에는 String밖에 못온다.
    sc1.setObj(new Integer(0)); // Integer타입의 객체같은 또 다른 타입의 객체를 StringContainer에 담을 수 있는 방법이 없다.

    GenericContainer<Integer> gc1 = new GenericContainer<>(); // 없었던 <Integer> 추가
    // 뒤의 <>는 써도 되고 안써도 된다. <Integer> 사용 시점에 <T>가 <Integer>로 바뀐다.
    gc1.setObj(3);

    GenericContainer<String> gc2 = new GenericContainer<>(); // 똑같은 코드를 가지고 String type을 표현하고 싶다.
    gc2.setObj("Generic");
}
```



StringContainer -> 타입이 고정되어 있다.

GenericContainer -> Generic Type. Runtime시에, 실제 코드가 사용되는 시점에 T를 대체할 수 있는 구조.

위에 꺼보다 GenericContainer  사용하는 것이 더 유리하겠쥬?

Generic도 알아야 겠지만, Generic을 이용해서 Collection이 다 만들어져 있다.

Generic으로 되어 있는 Collection이용 시 -> 꺽쇠 후 product, 꺽쇠 후 myClass 이런 식으로 하면 거기에 있는 클래스의 객체로 대체된다.



Generic의 T에 대체되는 것 -> 우리가 만드는 임의의 클래스들은 다 가능.



1.5 이상부터는 내가 임의로 Class를 만든 뒤 Collection을 이용해 저장하는 것이 가능하다.

Generic 사용하면 편안



웹 애플리케이션 하면 사실 Data의 대부분은 DB쪽에 만들어놓고, 자바는 Backend쪽에..

다양한 형태로 구성되어 있는 DB에 있는 것들을 표현하기 위해 DTO, VO란 형태의 자바 파일 클래스를 만듦 -> 여러 개를 담아서 화면에 출력해야 된다든지 할 때 Generic 형태의 Collection들을 적극적으로 활용하면 된다.



Wrapper

예전에 primitive type(객체처럼 쓸 수 있음) 구분되어 있었음

버전 올라가면서 하나인 것처럼 쓸 수 있음





#### Order #4 - 의료기관 about() 추가







