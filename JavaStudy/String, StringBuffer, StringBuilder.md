# String, StringBuffer, StringBuilder

String은 문자열을 대표하는 클래스입니다. 문자열을 조작하는 경우 유용하게 사용됩니다.

StringBuffer와 StringBuilder는 String을 붙여쓰기와 같은 조작을 할 때에 사용됩니다. String의 일반적인 사용방법을 이용해도 되지만 성능상의 이점을 StringBuffer와 StringBuilder가 가지고 있습니다. 본래 JDK 1.5 이전 버전에서는 String + String의 성능이 StringBuilder를 사용하는 것보다 느렸습니다. 하지만 이후부터는 컴파일러가 String + String을 StringBuilder로 변환하는 과정이 추가되었기 때문에 성능상의 문제가 없습니다.

StringBuffer와 StringBuilder의 차이는 동기화의 지원 여부입니다. StringBuffer는 멀티 스레드에서 동시 접근을 해도 syncronized 키워드를 사용하기 때문에 동기화 문제가 해결이 됩니다. 하지만 StringBuilder는 지원하지 않기 때문에 심각한 문제를 초래할 수 있습니다.