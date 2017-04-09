# 연산자(Operator)

### 부호 연산자(+,-)의 산출 타입은 int

```java
short a = 100;
short b = -a; //Compile Error
int c = -a
```

 \- boolean, char 타입에는 부호 연산자를 사용할 수 없다.



### i++ / i=i+1 ?

- 일반적으로 `i++`가 `i=i+1`보다 연산 속도가 빠르다고 알려져 있지만, 실제로 컴파일 하면 동일한 바이트 코드가 생성되기 때문에, 둘의 연산 속도는 같다.



### 비트 반전 연산자(~)

- 정수 타입(byte, short, int long)의 피연산자를 이진수로 표현했을 때 비트값을 반전시킨다.

- 비트 반전 연산자의 산출값에 1을 더하면 부호가 반대인 정수를 얻을 수 있다.

- `Integer.toBinaryString()` 메소드를 통해 이진수 확인 가능

  ```java
  public static void main(String[] args) {
    int a = 10;
    int b = ~a;
    int c = ~a + 1;
    System.out.println(toBinaryString(a) + " (십진수: " + a + ")");
    System.out.println(toBinaryString(b) + " (십진수: " + b + ")");
    System.out.println(toBinaryString(c) + " (십진수: " + c + ")");
  }

  public static String toBinaryString(int value) {
    String bin = Integer.toBinaryString(value);
    //앞의 비트가 0이면 생략되기 때문에 0을 붙여줌
    while(bin.length() < 32) {
      bin = "0" + bin;
    }
    return bin;
  }
  ```

  ​

### 산술 연산자(+, -, *, /, %) 연산 규칙

1. 피연산자들이 모두 정수 타입이고, int 타입보다 크기가 작은 타입일 경우 모두 int 타입으로 변환 후 연산을 수행한다. 따라서 연산의 산출 타입은 `int`이다.
2. 피연산자들이 모두 정수 타입이고, long 타입이 있을 경우 모두 long 타입으로 변환 후 연산을 수행한다. 따라서 연산의 산출 타입은 `long`이다.
3. 피연산자 중 실수 타입이 있을 경우 크기가 큰 실수 타입으로 변환 후 연산을 수행한다. 따라서 연산의 산출 타입은 실수 타입니다.

  **cf> 리터럴 간의 연산은 타입 변환 없이 해당 타입으로 계산한다. **

```java
char c1 = 'A' + 1; //리터럴 'A'에 1을 더한 것이므로 66이 되어 저장됨.
char c2 = 'A';
//char c3 = c2 + 1; // c2가 int 차입으로 변환되어 연산되기 때문에 산출 타입이 int가 됨.
int c3 = c2 + 1;

byte b1 = 10 + 20;
byte b2 = 10;
//byte b3 = b2 + 1; //산출 타입 int가 됨.
int b3 = b2 + 1;
```



### 산술 연산 전에 오버플로우를 탐지할 것

```java
public static void main(String[] args) {
  try {
    int result = safeAdd(2000000000, 2000000000);
    System.out.println(result);
  } catch (ArithmeticException e) {
    System.out.println("Overflow. Cannot calculate exactly.")
  }
  
  public static int safeAdd(int left, int right) {
    if ( right>0 ) {
      if ( left>(Integer.MAX_VALUE - right) ) {
        throw new ArithmeticException("Overflow occured.");
      }
    } else {
      if ( left<(Integer.MIN_VALUE - right) ) {
        throw new ArithmeticException("Overflow occured.");
      }
    }
    return left+right;
  }
}
```



### 정확한 계산은 부동소수점 타입을 사용하지 말 것

- 부동소수점 타입은 0.1을 정확히 표현할 수 없어 근사치로 처리함. => **정확한 계산은 정수 연산으로!**

  ```java
  int a = 1;
  double b = 0.1;
  int c = 7;

  double result = a - b*c; //0.3이 나오지 않음

  //정수로 변경해서 사용
  int intVal = a*10;
  int temp = intVal - c;

  double rightResult = temp/10.0; //0.3이 나옴
  ```

  ​

### NaN과 Infinity

- `/` 또는 `%` 연산 시 좌측 피연산자가 정수 타입인 경우, 우측 피연산자가 0일 경우 ArithmeticException이 발생한다.

- 좌측 피연산자가 실수 혹은 우측 피연산자가 0.0(또는 0.0F)인 경우에는 `/` 연산 시 Infinity 값을 가지며, `%` 연산 시 NaN(Not a Number) 값을 가진다.

- Infinity와 NaN의 경우 산술 연산을 해도 결과가 그대로이기 때문에 값을 미리 확인해야 한다.

  ```java
  int x = 5;
  double y = 0.0;
  double z = x/y;

  System.out.println(Double.isinfinite(z)); //true
  System.out.println(Double.isNaN(z)); //false

  if ( Double.isInfinite(z) || Double.isNaN(z) ) {
    System.out.println("값 산출 불가");
  } else {
    System.out.println(z+3);
  }

  //입력값으로 NaN을 받는 경우가 있으므로 부동소수점을 입력받을 때는 반드시 NaN Check를 해야함.
  String userInput = "NaN";
  double bal = Double.valueOf(userInput);

  double currentBalance = 1000.0;

  //NaN은 != 연산자를 제외한 모든 비교 연산자를 사용할 경우 false를 리턴 -> 반드시 isNaN 사용!
  if(Double.isNaN(bal)) {
    System.out.println("NaN");
    bal = 0.0;
  }
  currentBalance += bal;
  System.out.println(currentBalance);
  ```



### 문자열 연결 연산자(+)

- 문자열과 숫자가 혼합되었을 경우 왼쪽에서 오른쪽으로 연산이 진행되기 때문에 먼저 연산되는 것에 따라 다른 결과가 나온다.

  ```java
  String str1 = "JDK" + 3 + 3.0; // "JDK33.0"
  String str2 = 3 + 3.0 + "JDK" // "6.0JDK"
  ```

  ​

### 0.1 == 0.1F ?

- 부동소수점 타입은 0.1을 정확히 표현할 수 없기 때문에 0.1F는 0.1의 근사값으로 변환되어 0.1보다 큰 값이 된다. 따라서 False. 피연산자를 모두 Float 타입으로 Casting하거나 정수로 변환해서 비교할 것.



### 문자열 비교는 `equals()`를 사용하자

- 문자열 리터럴이 동일하면 동일한 String 객체를 참조하기 때문에 ==를 써도 원하는 결과를 얻을 수 있지만, 문자열 변수가 다른 객체를 참조하고 있다면 equals() 메소드를 사용해야 한다. 그냥 항상 equals() 쓰자.

  ```java
  String str1 = "Juhan";
  String str2 = "Juhan";
  String str3 = new String("Juhan");

  System.out.println(str1 == str2); //true
  System.out.println(str1 == str3); //false
  System.out.println(str1.equals(str3)); //true
  ```

  ​

### `&&`와 `&` , `||`와 `|`

- 산출 결과는 같음. 하지만 `&&`는 앞의 피연산자가 false라면 뒤의 피연산자를 평가하지 않고 바로 false를 산출하지만 `&`는 두 피연산자 모두 평가함. `||` 역시 앞의 피연산자가 true라면 바로 true를 산출하는 반면, `|`는 두 피연산자를 모두 평가함. 두 개짜리가 더 빠르다.



### 삼항 연산자( ? : )

```java
int score = 85;
char grade = (score>90)? 'A' : ((score>80)? 'B' : 'C');
System.out.println(grade); //'B'
```

