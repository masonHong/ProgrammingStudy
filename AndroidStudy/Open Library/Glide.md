# Glide Library

## Gradle

```gradle
dependencies {
    ...
    compile 'com.github.bumptech.glide:glide:4.0.0-RC1'
    compile 'com.android.support:support-v4:26.+'
    annotationProcessor 'com.github.bumptech.glide:compiler:4.0.0-RC1'
	...
}
```

## AppGlideModule
- GlideApp 클래스를 사용하기 위해서 필요하다
- 빌드를 한번 하고 나면 GlideApp 클래스가 생성된다

```java
@GlideModule
public final class MyAppGlideModule extends AppGlideModule {
}
```

## 사용 방법

```java
GlideApp.with(context)
        .load(shop.getImageUrl())
        .fitCenter()
        .placeholder(R.drawable.place_holder)
        .into(imageView);
```