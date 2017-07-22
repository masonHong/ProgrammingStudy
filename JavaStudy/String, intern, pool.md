# String의 저장 방식

String을 메모리에 저장하는 방법에는 3가지 정도가 있다.

```java
String a = "java";
String b = new String("java");
String c = new String("java").intern();
```

모두 같은 의미의 문자열 "java"를 저장하고 있지만 주소를 보면 몇몇이 다른 위치에 저장되어있다.

메모리에는 여러 영역이 있지만 String은 Heap 영역에 저장이 된다. Heap영역에는 Permanent라는 영역이 또 존재하는데 이 곳에서는 String Pool이라는 저장소가 있다.

```java
String a = "java";
String b = "java";
String c = "java";
```

위의 코드에서 a,b,c는 Permanent 영역에 저장된다. Permanent 영역에 있는 데이터는 재사용을 위해서 저장되어있다. 변수 a가 생성되고 나서 b를 생성할 때 이미 만들어져있는 "java"를 재사용한다는 의미이다. 그래서 String 변수 a,b,c 모두 같은 주소를 가르킨다. 결국 == 동등연산자와 equals모두 true를 반환한다.

```java
String a = "java";
String b = new String("java");
String c = new String("java");
```

위의 코드에서는 a,b,c 모두 다른 주소를 가리킨다. a는 Permanent 영역에 저장이 되며 b와 c는 일반 Heap 영역에 저장이 된다. Heap의 일반 영역에서는 각각 다른 주소에 저장된다. 이 경우에는 == 동등연산자는 모두 false를 반환하지만 equals는 모두 true를 반환한다.

```java
String a = "java";
String b = new String("java").intern();
```

위의 코드에서는 b가 intern()이라는 메소드를 호출하고 있다. intern() 메소드는 Heap의 일반 영역에 생성된 데이터를 사용하지 않고 Permanent에 저장하거나 저장되어있는 데이터를 사용하겠다는 의미이다. 따라서 a에서 생성된 "java" 문자열을 재사용하게 된다. 결국 a == b 와 a.equals(b) 모두 true를 반환한다.

System.identityHashCode()라는 함수가 있는데 이 함수는 해당 Object의 실제 메모리의 위치와 관련된 값을 반환한다.