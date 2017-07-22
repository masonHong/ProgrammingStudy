# Immutable

Immutable이란 생성후 변경 불가능한 객체를 말합니다. 그래서 Immutable에는 Set 메소드를 지원하지 않습니다. 멤버 변수를 변경할 수 없다는 의미입니다. 여기서 변경할 수 없다는 의미는 Heap 영역에서만 국한됩니다. 즉 재할당은 가능합니다. String a = "a";를 실행한 후에 a = "b"; 가 가능하다는 의미입니다. 참조가 변하는 것이지 실제 값이 바뀌는 것이 아닙니다.

Immutable을 사용하면 멀티 쓰레드 환경에서 더 신뢰할 수 있는 코드를 만들어 내기가 쉽습니다. 멤버 변수를 변경시키지 않기 때문에 스레드가 비정상적인 작동을 할 위험이 없기 때문입니다.

대표적인 Immutable 클래스로는 String, Boolean, Integer, Float, Long 등이 있습니다.

Immutable은 보통 final 클래스로 정의하며 모든 멤버 변수를 final로 지정합니다.

```java
public final class WrongImmutable {
    private final Date date;
    public WrongImmutable(Date date) {
        this.date = date;
    }
}
```

위의 코드는 잘못된 Immutable의 예시입니다. 다음 코드를 보면 date가 내부적으로 값이 변경될 수 있습니다.

```java
public class WornImmutableTest {
    public static void main(String[] args) {
        Date testDate = new Date();
        WrongImmutable wrongImmutable = new WrongImmutable(testDate);
        testDate.setTime(testDate.getTime() + 100000000);
    }
}
```

main에서 testDate의 시간을 변경하면 WrongImmutable안에 date의 시간도 변경된다는 것을 확인할 수 있습니다. 따라서 멤버 변수를 전달 받을 때에는 어떤 식으로든 복사를 해야합니다. 예를 들면 this.date = new Date(date.getTime()); 와 같은 방식입니다.

자바에는 reflection을 이용하면 Immutable은 사실 존재할 수 없습니다. reflection을 사용함으로 써 결국 모든 멤버 변수에 접근이 가능합니다.