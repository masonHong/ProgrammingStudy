#6 List, Set, Map

## List

List에는 ArrayList, LinkedList, Stack, Vector가 존재한다. 순서가 있는 데이터의 집합이며 데이터의 중복을 허용한다.

- ArrayList: 순차적인 접근에 강하다.
- LinkedList: 삽입과 삭제에 강하다.
- Vector: 모든 메소드가 동기화 되어있다.

## Set

Set에는 HashSet, TreeSet이 있다. 순서를 유지하지 않는 데이터의 집합이며 데이터의 중복을 허용하지 않는다.

- HashSet: 가장 빠른 접근 속도. 순서를 예측할 수 없음.
- LinkedHashSet: 가장 최근에 접근한 순서대로 접근 가능.
- TreeSet: 정렬된 순서로 보관하며 정렬 방법을 지정 가능.

## Map

Map에는 HashMap, TreeMap, HashTable, Properties가 있다. Key와 Value의 쌍으로 이루어진 데이터의 집합이며 순서는 유지하지 않고 키는 중복을 허용하지 않지만 값의 중복을 허용한다.

- HashMap: 해시 테이블을 사용한다. 중복을 허용하지 않으며 순서를 보장하지 않음. 키와 값으로 null을 허용한다.
- Hashtable: HashMap보다는 느리지만 동기화를 지원한다. 키와 값으로 null을 허용하지 않는다.
- TreeMap: 이진검색트리의 형태이다. 정렬된 순서로 저장하므로 빠른 검색이 가능하다. 저장시간이 오래걸린다.