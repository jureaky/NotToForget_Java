# 형 변환시 주의사항

### 값의 손실이 없이 안전하게 변환될 수 있는 지 검사하기

- byte 타입으로 변환 예제

  ```Java
  int intValue = 128;

  if( (i<Byte.MIN_VALUE) || (i>Byte.MAX_VALUE) ) {
    System.out.println("Cannot cast to Byte Type. Check the value again.");
  } else {
    byte byteValue = (byte) intValue;
    System.out.println(byteValue);
  }

  ```



### 정수에서 실수로 변환 시 정밀도 손상이 일어날 수 있음

\> float 타입은 가수에 23bit를 할당한다. int는 32비트이므로 int -> float 변환 시 23비트로 완전히 표현되지
   않는 값은 근사치로 변환된다. 따라서 float 값을 다시 int로 변환하면 원래의 int 값을 얻지 못한다.
   -->> ***int는 항상 double로 변환해야 안전하다. double 타입은 가수에 52bit를 할당하기 때문이다.***

```java
int num1 = 123456780;
int num2 = 123456780;

float num3 = num2;
num2 =(int) num3;

int result = num1 - num2; //0이 되어야 하나, -4가 나옴

double num4 = num2;
num2 = (int) num4;
int result = num1 = num2; //0이 나옴.
```

