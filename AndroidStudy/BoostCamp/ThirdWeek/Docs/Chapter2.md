# 브로드캐스트리시버 살펴보기

## 브로드캐스트리시버의 이해
- BroadcastReceiver는 시스템으로부터 방송 메시지를 듣는다.
- 예를들면 부팅, 문자, 전화 등
- 메시지를 수신 받으면 onReceive()가 호출된다.

## 브로드캐스트리시버 등록 및 제거

### 등록 방법1
- 매니페스트 파일에 receiver를 추가합니다. receiver는 BroadcastReceiver를 상속받아야 한다.
- receiver안에 intent-filter를 추가합니다. intent-filter속성은 수신 받을 메시지입니다. ex) BOOT_COMPLETED
- 등록을 해지할 수 없음.

```xml
<receiver android:name=".MyBroadcastReceiver"  android:exported="true">
    <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="android.intent.action.INPUT_METHOD_CHANGED" />
    </intent-filter>
</receiver>
```

### 등록 방법2
- IntentFilter 객체를 생성한다.
- BroadcastReceiver 객체를 생성한다.
- registerReceiver()를 사용하여 리시버를 등록한다.
- unregisterReceiver()로 등록을 해지할 수 있다.

```java
BroadcastReceiver br = new MyBroadcastReceiver();
IntentFilter filter = new IntentFilter(ConnectivityManager.CONNECTIVITY_ACTION);
intentFilter.addAction(Intent.ACTION_AIRPLANE_MODE_CHANGED);
this.registerReceiver(br, filter);
```

## 브로드캐스트리시버를 활용한 SMS 수신

## 추가 내용
- If you don't need to send broadcasts to components outside of your app, then send and receive local broadcasts with the LocalBroadcastManager which is available in the Support Library. 
- Because a receiver's onReceive(Context, Intent) method runs on the main thread, it should execute and return quickly.
- When you register a receiver, any app can send potentially malicious broadcasts to your app's receiver.