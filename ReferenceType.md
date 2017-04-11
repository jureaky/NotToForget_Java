# 참조 타입(Reference Type)

### 참조 타입이란 객체의 번지를 참조하는 타입을 말한다.

#### 배열 타입, 열거 타입, 클래스 타입, 인터페이스 타입이 있다.



- 기본 타입으로 선언된 변수는 스택에 실제 값을 변수 안에 저장하지만, 참조 타입으로 선언된 변수는 스택에 생성되긴 하지만 객체는 힙에 생성되고, 이때 생성된 객체의 번지를 변수의 값으로 저장한다.
- `new` 연산자는 객체 생성 연산자로, 힙 영역에 새로운 객체를 만들 때 사용한다.



### 배열(Array)

- 배열(Array): 같은 타입의 데이터를 연속된 공간에 나열시키고, 각 데이터에 인덱스(index)를 부여해 놓은 자료구조

- {}를 사용한 배열 객체 생성은 배열 변수의 선언과 동시에 이루어져야 한다. 배열 변수의 선언 후 나중에 초기화를 시켜주려면 `new`연산자를 사용한다. 메소드의 매개값으로 배열을 생성함과 동시에 사용하고자 할 때에도 반드시 `new`연산자를 이용해야 한다.

  ```java
  int[] scores;
  //scores = {36, 20, 45, 50, 15} //Compile Error

  String[] names = null;
  names = new String[] {"David", "Mark", "Baker"};

  //int sum = sum({90, 80, 70}); //Compile Error
  int sum = sum(new int[] {90, 80, 70});
  ```



- 다차원 배열은 수학의 행렬과는 다르다. 일차원 배열이 서로 연결된 구조로 다차원 배열이 구현된다. 첫 번째 차원의 배열의 인덱스마다 그 다음 차원의 배열을 참조하는 방식으로 생성된다. 따라서 계단식 구조를 갖는 것이 가능하다.

  ```java
  int[] scores = new int[2][];
  scores[0] = new int[2];
  sores[1] = new int[3];

  scores.length; //2
  scores[0].length; //2
  scores[1].length; //3
  ```

  ​

- 배열의 복사는 for문으로 할 수도 있지만 `System.arraycopy()`메소드를 이용할 수 있다.

  `System.arraycopy(Object src, int srcPos, Object dest, int destPos, int length)`

  (원본 배열, 복사 시작점 인덱스, 새 배열, 붙여넣기 시작점 인덱스, 복사 개수)

  ```java
  System.arraycopy(originArray, 0, newArray, 0, originArray.length);
  ```

  ​

### 열거 타입(Enumeration Type)

- 한정된 값만을 갖는 데이터 타입. 몇 개의 열거 상수 중에서 하나의 상수를 저장하는 데이터 타입.

```java
public enum TypeName { CONSTANT_1, CONSTANT_2, CONSTANT_3 }
```

- 열거 타입 변수에 열거 상수를 저장할 때는 상수 단독으로 사용할 수 없고 `열거타입.열거상수`의 형식으로 사용해야 한다.
- 열거 상수 역시 열거 객체이다. 메소드 영역에 생성된 열거 상수가 힙 영역에 생성된 각자의 열거 상수 객체를 참조한다.



- 열거 타입은 컴파일시 java.lang.Enum 클래스를 상속한다. 따라서 여기에 선언된 메소드들을 사용할 수 있다.

  1. **name()**

     열거 객체가 가지고 있는 문자열(=열거 상수의 이름)을 리턴한다.

     ```java
     Week today = Week.SUNDAY;
     String name = today.name(); //"SUNDAY
     ```

  2. **ordinal()**

     열거 객체의 인덱스를 리턴한다. 0번부터 시작.

  3. **compareTo()**

     매개값으로 주어진 열거 객체를 기준(0)으로 인덱스를 비교한다. 순번이 빠르면 음수, 늦으면 양수가 리턴된다.

  4. **valueOf(String name)**

     매개값으로 주어진 문자열과 동일한 문자열을 가지는 열거 객체를 리턴한다. 외부로부터 문자열을 입력받아 열거 객체로 변환할 때 유용하게 사용한다.

  5. **values()**

     모든 열거 객체들을 배열로 만들어 리턴한다. 배열의 인덱스==열거 객체의 순번

