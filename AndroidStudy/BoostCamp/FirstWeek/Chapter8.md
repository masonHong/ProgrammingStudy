# 위젯의 이벤트 처리하기 #

## 1. 버튼 클릭 처리하기
1. 익명 클래스 사용
```xml
<Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Button"/>
```
```java
findViewById(R.id.button).setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        Toast.makeText(MainActivity.this, "Click!", Toast.LENGTH_SHORT).show();
    }
});
```
2. 액티비티에 리스너 implements
```xml
<Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Button"/>
```
```java
public class MainActivity extends AppCompatActivity implements View.OnClickListener{
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        findViewById(R.id.button).setOnClickListener(this);
    }

    @Override
    public void onClick(View v) {
        Toast.makeText(this, "Click!", Toast.LENGTH_SHORT).show();
    }
}
```
3. onClick 속성 사용
```xml
<Button
    android:id="@+id/button"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Button"
    android:onClick="onButtonClick"/>
```
```java
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    public void onButtonClick(View v) {
        Toast.makeText(this, "Click!", Toast.LENGTH_SHORT).show();
    }
}
```

## 2. 위젯 터치 이벤트 처리하기 ##
* **onTouch()의 리턴 값**은 이후 리스너도 실행할 것인가에 대한 정보이다.
* **OnTouchListener**를 설정하는 방법과 **OnTouchEvent**를 오버라이드 하는 방법이 있다.

```java
@Override
public boolean onTouch(View v, MotionEvent event) {
    if(event.getAction() == MotionEvent.ACTION_DOWN) {
        Log.i("TAG", "onTouch. ACTION_DOWN");
    } else if (event.getAction() == MotionEvent.ACTION_MOVE) {
        Log.i("TAG", "onTouch, ACTION_MOVE");
    }

    float x = event.getX();
    float y = event.getY();
    Log.i("TAG", "onTouch. x:"+x+", y:"+ y);
    return true;
}
```

## 3. 그 밖의 다양한 이벤트 종류 살펴보기 ##
```java
imageView.setOnDragListener();			// 뷰 드래그
imageView.setOnFocusChangeListener();	// 뷰 포커스 변경
imageView.setOnLongClickListener();		// 뷰 롱 클릭
checkBox.setOnCheckedChangeListener();	// 체크 상태 변화
seekBar.setOnSeekBarChangeListener();	// 시크바 위치 변화
listView.setOnItemClickListener();		// 아이템 클릭
listView.setOnItemLongClickListener();	// 아이템 롱 클릭
listView.setOnItemSelectedListener();	// 아이템 선택
```