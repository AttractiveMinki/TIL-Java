## Java 기본 문법 응용 Array



오늘 - Java의 Array(배열) 문제 풀이



#### Array를 사용하지 않고 주사위 5번 던진 결과 출력하기

```java
	public static void main(String[] args) {
     int N = 6;
        
     int result1 = (int)(Math.random() * N) + 1;
     int result2 = (int)(Math.random() * N) + 1;
     int result3 = (int)(Math.random() * N) + 1;
     int result4 = (int)(Math.random() * N) + 1;
     int result5 = (int)(Math.random() * N) + 1;
        
     System.out.println(result1);
     System.out.println(result2);
     System.out.println(result3);
     System.out.println(result4);
     System.out.println(result5);
    }
```

좀 비효율적인듯..



#### 동일한 type의 변수를 여러 개 사용

- 변수의 수 증가

- 코드의 길이 증가



- 반복문 적용 불가

- 변수의 수가 동적으로 결정될 경우, 사용 불가



#### Array로 동일 Type 변수 대신하기

- 변수의 수 감소

- 코드의 길이 감소



- 반복문 적용 가능

- 변수의 수가 동적으로 결정될 경우, 사용 가능





#### Array 만들기 #1

- 선언 - 대괄호 사용
  - int [] intArray; - 일반적으로 사용. 아직 한 개의 변수만 선언.
  - int intArray [];
- 생성 - new라는 연산자 사용(자바에서 객체를 만들 때 사용하는 대표적 키워드 - new) [배열도 객체다]
  - intArray = new int[5]; - int 변수 다섯 개. 인덱스는 0 ~ 4 [Zero Based]
  - intArray = new int[10];
- 개별 요소 값 할당
  - intArray[0] = 3;
  - intArray[2] = 7;



변수 선언하는 방법은 두 가지

세 단계를 거친다.

선언, 생성, 할당



#### Array 사용, 반복문 없이 주사위 5번 던지고 출력하기

```java
int [] resultArray = new int[5];

resultArray[0] = (int)(Math.random() * N) + 1;
resultArray[1] = (int)(Math.random() * N) + 1;
resultArray[2] = (int)(Math.random() * N) + 1;
resultArray[3] = (int)(Math.random() * N) + 1;
resultArray[4] = (int)(Math.random() * N) + 1;

System.out.println(resultArray[0]);
System.out.println(resultArray[1]);
System.out.println(resultArray[2]);
System.out.println(resultArray[3]);
System.out.println(resultArray[4]);
```



#### Array 사용, 반복문 쓰고 주사위 5번 던지고 출력하기

```java
int N = 6;

int [] resultArray = new int[5];

for (int i=0; i<5; i++ ){
    resultArray[i] = (int)(Math.random() * N) + 1;
}

for (int i=0; i<5; i++ ){
	System.out.println(resultArray[i]);    
}
```



배열은 반복문과 굉장히 밀접한 연관되어 사용될 수밖에 없다.



문자열을 저장할 수 있는 String 클래스도 내부적으론 char의 배열을 쓴다.





#### String "MINKI"를 이용하여 char 배열 minkiArray를 만들고, 출력하는 코드를 작성하라

```java
String minkiStr = "MINKI";

char[] minkiArray = new char[minkiStr.length()]; // length는 속성(attribute)이 아니고 메소이기 때문에 ()가 붙는다. 함수에 해당하기 때문에 호출해야 함

for (int i = 0; i < minkiArray.length; i++) {
    minkiArray[i] = minkiStr.charAt(i); // 문자열에서 한 글자씩 index 옮겨가며 가져오는 String class의 메소드 -> charAt
}

for (int i = 0; i < minkiArray.length; i++) {
    System.out.print(minkiArray[i]);
}


```

char[] minkiArray = new char[minkiStr.length()];



##### charAt()

문자열에서 한 글자씩 index 옮겨가며 가져오는 String class의 메소드

문자열 인덱싱이 안되다니.. 충격



사용예시

```java
String minkiStr = "MINKI";

for (int i = 0; i < minkiArray.length; i++) {
    minkiArray[i] = minkiStr.charAt(i);
}
```



##### str.substring(시작위치, 끝위치)

문자열 슬라이싱

파이썬 [:] 역할인듯






#### Array 출력 우아하게

Arrays.toString() 

// https://docs.oracle.com/javase/8/docs/api/ -> java.util -> Arrays -> toString 메소드



#### Array 만들기 #2

int [] intArray = {0, 1, 3, 4};

int intArray [] = {-3, -1, 1, 3, 5}

- new가 없고, []도 없다.
- 한 번 할당된 값을 변경할 수 없다. (Array Constant, 어래이 상수)
- 선언과 동시에 값을 줘야 한다.



#### 배열 length, default value

- Array 객체의 length Attribute로 길이를 표현
  - int [] intArray = {-3, -1, 1, 3, 5}
  - System.out.println(intArray.length);

- Array 요소 중 값을 할당받지 않은 요소는 default value 값을 가진다.
  - int intArray [] = new int[3];
  - System.out.println(intArray[0])
  - local -> default 값 없음
  - Array엔 default value, 0에 준하는 값이 들어간다.
    - 0, 공백문자, false





#### Local Variables vs Array in Memory

stack

- 호출 시 하나씩 만들어진다.

- int i = 3;



heap

- array같은 건 창고(heap)에 저장. [주소는 stack에]
- array도 객체 -> 얼마나 만들어질지 모름 -> 문자열처럼 다른 공간 힙에 객체 만듦

- int[] intArr = new int[3];



어제 했던 것

primitive type -> 자기 자신이 들어감

reference type -> heap에 원하는 구성 만들어놓고 주소값 가져오는 형태





#### for-each with Array 

인덱스 대신 요소 복사해서 사용

- Java 5.0부터 지원
- 가독성이 개선된 반복문으로, 배열 및 Collections에서 사용
- index 대신 직접 요소(elements)에 접근하는 변수를 제공
- naturally ready only(copied value) -> 원본 변경 어렵 [파이썬도 동일. 복사해서 쓴다]

```java
int intArray[] = {1, 3, 5, 7, 9};

for( int x : intArray ){
    System.out.println( x );
}
```





#### 주사위 5번 던지기 for-each

```java
int N = 6;

int [] resultArray = new int[5];

for (int i=0; i<resultArray.length; i++ ){
    resultArray[i] = (int)(Math.random() * N) + 1;
}

for (int x : resultArray ){
	System.out.println(x);    
}
```



#### 참고 [length]

- length: 배열의 길이

- length(): 문자열의 길이

- size(): 컬랙션 프레임워크 타입의 길이

https://mine-it-record.tistory.com/126





#### 학생 이름 저장 후 출력하기

```java
string [] students = { "이민기", "남궁민", "개미남", "홍길동" };

for( String student : students ) {
    System.out.println(student);
}
```





#### swap

```java
String temp = students[1];
students[1] = students[2];
students[2] = temp;
```





#### 학생에 박보검 추가하기

```java
string [] students = { "이민기", "남궁민", "개미남", "홍길동" };

students = { "이민기", "남궁민", "개미남", "홍길동", "박보검" }; // 에러!

String [] students2 = { "이민기", "남궁민", "개미남", "홍길동", "박보검"};

String [] students3 = new String[5];
System.out.arraycopy(students, 0, students3, 0, 4);
students3[4] = "신자바";
```



#### Array is Immutable

- 최초 Memory Allocation 이후, 변경할 수 없음. (크기 변경 불가)
- 개별 요소는 다른 값으로 변경이 가능하나, 삭제할 수는 없음.
- 크기를 늘리거나 줄일 수 없음.
- 변경이 필요한 경우, 새로 작성하는 것이 일반적으로 유리함.





#### System.arraycopy

System.arraycopy(src, srcPos, dest, destPos, length)

src: 복사하고자 하는 소스(Array)

srcPos: 어느 부분부터 읽어올 것인지

dest: 복사할 소스

destPos: 어느 부분부터 쓸 지

length:  원본에서 복사본까지 얼마만큼 읽어올 것인지

주의) length -> array 범위 벗어나면 안 됨 [arrayindexoutofboundsexception]





#### 최댓값 최솟값 출력하기

```java
int[] intArray = { 3, 27, 13, 8, 235, 7, 22, 9, 435, 31, 54};

int min = 999;
int max = 0;

for (int i = 0; i < intArray.length; i++){
    if( intArray[i] < min){
        min = intArray[i];
    }
    if( intArray[i] > max){
        max = intArray[i]
    }
}

System.out.println("Min : " + min + " Max : " + max);
```





#### 위의 문제 Integer, Math Class로 refactoring

```java
int[] intArray = { 3, 27, 13, 8, 235, 7, 22, 9, 435, 31, 54};

int min = Integer.MAX_VALUE;
int max = Integer.MIN_VALUE;

for (int i = 0; i < intArray.length; i++){
	min = Math.min(min, intArray[i]);
    max = Math.max(max, intArray[i]);
}

System.out.println("Min : " + min + " Max : " + max);
```





#### 0~9 사용횟수 출력

```java
int[] intArray = {3, 7, 2, 5, 7, 7, 9, 2, 8, 1, 1, 5, 3};
int[] used = new int[10];

for (int i = 0; i < intArray.length; i++){
    used[intArray[i]]++;
}

System.out.println(Arrays.toString(used));
```





##### Arrays.toString(used);

지정된 배열 및 그 요소를 나타내는 문자열을 반환

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/toString





#### 1~20 중 사용하지 않은 숫자 출력

```java
int[] intArray = {1, 3, 4, 7, 8, 10, 12, 15, 16, 17, 18};
int[] used = new int[21]; // 0: dummy

for (int i = 0; i < intArray.length; i++){
    used[intArray[i]]++;
}

for (int i = 0; i < used.length; i++){
    if( used[i] == 0) {
        System.out.print(i + " ");
    }
}
```





#### 다차원 배열(Multi-Dimensional Array)

```java
char[][] grid = new char[4][3];

grid[0][0] = 'C'; grid[0][1] = 'A'; grid[0][2] = 'A';
grid[1][0] = 'C'; grid[1][1] = 'C'; grid[1][2] = 'B';
grid[2][0] = 'B'; grid[2][1] = 'A'; grid[2][2] = 'C';
grid[3][0] = 'C'; grid[3][1] = 'C'; grid[3][2] = 'C';

for (int i = 0; i < grid.length; i++){
    for ( int j = 0; j < grid[i].length; j++){
        System.out.print(grid[i][j]);
    }
    System.out.println();
}
```





#### 2차원 Array 만들기 #1

- 선언 - 대괄호 사용

  - int `[][] ` intArray; - 일반적으로 사용. 아직 한 개의 변수만 선언.
  - int [] intArray [];
  - int intArray [][];

  

- 생성

  - intArray = new int`[4][3]`; - int 변수 다섯 개. 인덱스는 0 ~ 4 [Zero Based]

  

- 개별 요소 값 할당

  - intArray`[0][2] `= 3;

    

#### 2차원 Array 만들기 #2

- int Type 기준으로 4x3 배열(Array)과 값을 동시에 만들기
  - int `[][]` intArray = { {0, 1, 2}, {0, 1, 2}, {0, 1, 2}, {0, 1, 2}}



#### 2차원 Array 만들기 #3

- int Type 기준으로 4x? 배열(Array)과 값을 동시에 만들기
  - int `[][]` intArray = new int[4][];
- 1차 Array만 생성 후, 필요에 따라 2차 배열을 생성함
  - intArray[1] = new int[2];
  - intArray[0] = new int[4];
  - intArray[2] = {1, 2, 3}; -> 에러





#### java.util.Scanner

사용자의 입력을 다양한 방법으로 처리해준다.

- .hasNext() -> 있는지 없는지, true false
- .next() -> 문자열 String 리턴
- .nextXXX() -> 해당 type으로
- .nextLine() -> 줄 전체, 개행 문자를 만날 때까지
- .nextChar() 이건 없음 -> .next().charAt(0) [next로 스트링 입력받은 뒤 charAt으로 한 글자를 입력받음]





#### 2차원 배열 입력받고 출력하기

```java
// import java.util.Scanner;

Scanner sc = new Scanner(System.in);
char[][] grid = new char[4][4];

for(int i = 0; i < 4; i++)
    for(int j = 0; j < 4; j++)
        grid[i][j] = sc.next().charAt(0);

for(int i = 0; i < 4; i++){
    for(int j = 0; j < 4; j++){
        System.out.print(grid[i][j]);
    }
    System.out.println();
}
sc.close();
```

```
2 3 1 4
1 X 3 2
3 4 X X
X 4 1 5

2314
1X32
34XX
X415
```



#### Array 순회 / 탐색

- 전체 중 X를 만나면
- X가 움직이면서
- X 주변 탐색
  - 좌/우
  - 상/하
- X 주변 탐색(4방)
- X 주변 탐색(8방)





#### X로 표시된 항목의 좌우 숫자의 합을 구하는 코드를 작성하시오.

```java
// import java.util.Scanner;

Scanner sc = new Scanner(System.in);
char[][] grid = new char[4][4];

int sum = 0;

for(int i = 0; i < 4; i++)
    for(int j = 0; j < 4; j++)
        grid[i][j] = sc.next().charAt(0);

for(int i = 0; i < 4; i++){
    for(int j = 0; j < 4; j++){
        if (grid[i][j] == 'X'){
            if(j - 1 >= 0 && grid[i][j - 1] != 'X') sum += grid[i][j - 1] - '0';
            if(j + 1 <  4 && grid[i][j + 1] != 'X') sum += grid[i][j + 1] - '0';
        }
    }
}
System.out.println(sum);
sc.close();
```

```
2 3 1 4
1 X 3 2
3 4 X X
X 4 1 5

12
```



X가 3행 1열에 있으면 4를 두 번 더할 수 있는 문제가 있다.



이미 사용된 숫자 다시 사용하지 않아야



#### 사방 탐색, 이미 사용한 숫자 사용하지 마십쇼

```java
Scanner sc = new Scanner(System.in);
char[][] grid = new char[4][4];
boolean[][] used = new boolean[4][4];

int sum = 0;

for(int i = 0; i < 4; i++)
    for(int j = 0; j < 4; j++)
        grid[i][j] = sc.next().charAt(0);

for(int i = 0; i < 4; i++){
    for(int j = 0; j < 4; j++){
        if (grid[i][j] == 'X'){
            if(i - 1 >= 0 && grid[i - 1][j] != 'X' && !used[i - 1][j]) 
            {
                sum += grid[i - 1][j] - '0';
                used[i - 1][j] = true;
            }
            if(i + 1 < 4 && grid[i + 1][j] != 'X' && !used[i + 1][j]) 
            {
                sum += grid[i + 1][j] - '0';
                used[i + 1][j] = true;
            }
            if(j - 1 >= 0 && grid[i][j - 1] != 'X' && !used[i][j - 1]) 
            {
                sum += grid[i][j - 1] - '0';
                used[i][j - 1] = true;
            }
            if(j + 1 < 4 && grid[i][j + 1] != 'X' && !used[i][j + 1]) 
            {
                sum += grid[i][j + 1] - '0';
                used[i][j + 1] = true;
            }
        }
    }
}
System.out.println(sum);
sc.close();
```

```
2 3 1 4
1 X 3 2
3 4 X X
X 4 1 5

26
```



8방 더 길어지자너

델타 배우면 간단해짐



index 벗어나면 java.lang.ArrayIndexOutOfBoundsException