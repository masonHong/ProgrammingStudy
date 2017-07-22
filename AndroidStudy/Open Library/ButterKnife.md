# 버터나이프(ButterKnife)
[공식사이트](http://jakewharton.github.io/butterknife/)

## 설정
- app수준 gradle 추가
```gradle
compile 'com.jakewharton:butterknife:8.7.0'
annotationProcessor 'com.jakewharton:butterknife-compiler:8.7.0'
```

## 기본적인 사용 방법
```android
@BindView(R.id.textTitle) TextView textTitle; // 뷰 바인드

@Override
protected void onCreate(Bundle savedInstanceState) {
	...
	ButterKnife.bind(this);
	...
}

@OnClick({R.id.button1, R.id.button2}) // 클릭 리스너 할당
public void onButtonClick(View view) {
	switch(view.getId()) {
	}
}
```