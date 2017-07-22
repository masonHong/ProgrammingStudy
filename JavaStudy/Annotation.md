# 어노테이션

어노테이션은 메타데이터로 볼 수 있다. 메타데이터란 애플리케이션 처리해야 할 데이터가 아니라, 컴파일 과정과 실행 과정에서 코드를 어떻게 컴파일하고 처리할 것인지를 알려주는 정보이다.

```java
@AnnotationName
```

## 어노테이션의 용도

- 컴파일러에게 코드 문법 에러를 체크하도록 정보를 제공
- 소프트웨어 개발 툴이 빌드나 배치 시 코드를 자동으로 생성할 수 있도록 정보를 제공
- 실행 시(런타임 시) 특정 기능을 실행하도록 정보를 제공

코드 문법 에러를 체크하는 대표적인 예는 @Override 어노테이션이다. @Override는 메소드 선언 시 사용하는데, 메소드가 오버라이드(재정의)된 것임을 컴파일러에게 알려주어 컴파일러가 오버라이드 검사를 하도록 해준다. 정확히 오버라이드가 되지 않았다면 컴파일러는 에러를 발생시킨다.

## 어노테이션 타입 정의와 적용

```java
public @interface AnnotationName {
    String elementName1();
    int elementName2() default 5;
}

@AnnotationName(elementName1 = "hello");
@AnnotationName(elementName1 = "hello", elementName2 = 10);

public @interface Annotation1 {
    String value(); // 기본 엘리먼트
}

@Annotation1("hello");

@Target({ElementType.TYPE, ElementType.FIELD, ElementType.METHOD});
public @interface Annotation2 {
}

@Annotation2
public class ClassName {
    @Annotation2
    private String field;

    // @Annotation2 --- @Target에 CONSTRUCT가 없음
    public ClassName() {}

    @Annotation2
    public void methodName() {}
}
```