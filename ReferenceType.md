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