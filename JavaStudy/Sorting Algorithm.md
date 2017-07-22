# 정렬 알고리즘

정렬 알고리즘에는 대표적으로 선택, 삽입, 버블, 병합, 퀵 정렬이 있다. 일반 적인 성능은 선택 < 삽입 < 버블 < 병합 < 퀵 순서로 퀵이 평균적으로 가장 빠르다.

## 선택정렬

```java
void selectionSort(Vector<int> v) {
    for(int i=0; i<v.size()-1; i++) {
        for(int j=i+1; j<v.size(); j++) {
            if(v[i] >= v[j]) {
                swap(v[i], v[j]);
            }
        }
    }
}
```

## 삽입정렬

```java

```