# 위치 및 구글 맵 살펴보기

## 기본으로 제공하는 프로젝트

- gradle

```gradle
dependencies {
    ...
    compile 'com.google.android.gms:play-services-maps:11.0.2'
    ...
}
```

- google_maps_api.xml

```xml
<string name="google_maps_key" templateMergeStrategy="preserve" translatable="false">YOUR_KEY_HERE</string>
```

- AndroidManifest.xml

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.project.boostcamp.googlemapsexample">
    ...
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <application
        ...
		>
        ...
        <meta-data
            android:name="com.google.android.geo.API_KEY"
            android:value="@string/google_maps_key" />
        ...
    </application>
</manifest>
```

- activity_maps.xml
```xml
<fragment xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:map="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/map"
    android:name="com.google.android.gms.maps.SupportMapFragment"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.project.boostcamp.googlemapsexample.MapsActivity" />
```

- MapsActivity.java

```java
public class MapsActivity extends FragmentActivity implements OnMapReadyCallback {
    private GoogleMap mMap;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_maps);
        ...
        SupportMapFragment mapFragment = (SupportMapFragment) getSupportFragmentManager()
                .findFragmentById(R.id.map);
        mapFragment.getMapAsync(this);
        ...
    }
    ...
    @Override
    public void onMapReady(GoogleMap googleMap) {
        mMap = googleMap;
        LatLng sydney = new LatLng(-34, 151);
        mMap.addMarker(new MarkerOptions().position(sydney).title("Marker in Sydney"));
        mMap.moveCamera(CameraUpdateFactory.newLatLng(sydney));
    }
}
```

## 마커 등록 및 삭제

### 마커를 등록할 때 필요한 것.
- GoogleMap 객체
- LatLng 객체
- MarkerOptions 객체

### 등록 과정
- LatLng 생성
- MarkerOptions 생성하여 기본 속성 설정
- GoogleMap의 객체에서 addMarker() 메소드 호출

### 마커 이벤트 처리
- OnMarkerClickListener // 클릭 이벤트
- OnMarkerDragListener // 드래그 이벤트
- OnInfoWindowClickListener // 정보창 이벤트

## 커스텀 마커 등록

### 마커의 속성
- 위치: 마커 위치
- 앵커: 마커 이미지의 중심
- 알파: 투명도
- 제목: 눌렀을 때 정보창에 표시되는 문자열
- 스니펫: 제목 아래에 표시되는 추가 텍스트
- 아이콘: 마커 대신 표시되는 이미지
- 드래그 가능
- 가시성
- 평면 또는 빌보드 방향
- 회전
- zIndex: 다른 마커와의 순서(타일 계층)

## 현재 위치 파악

### 구글의 LocationServices 활용

- gradle

```gradle
dependencies {
    ...
    compile 'com.google.android.gms:play-services:11.0.2'
}
```

- 버튼 보이기

```java
mMap.setMyLocationEnabled(true); // 권한 허용 필요
mMap.setOnMyLocationButtonClickListener(); // 리스너 등록
```

- 현재 위치 가져오기

```java
public class MapsActivity extends FragmentActivity implements OnMapReadyCallback, GoogleMap.OnMarkerClickListener, GoogleMap.OnMyLocationButtonClickListener {
    private FusedLocationProviderClient mFusedLocationClient;
    ...
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        ...
        mFusedLocationClient = LocationServices.getFusedLocationProviderClient(this);
    }
	@Override
	public boolean onMyLocationButtonClick() {
	    mFusedLocationClient.getLastLocation()
	            .addOnSuccessListener(this, new OnSuccessListener<Location>() {
	                @Override
	                public void onSuccess(Location location) {
	                    if (location != null) {
	                        double latitude = location.getLatitude();
	                        double longitude = location.getLongitude();
	                        LatLng latLng = new LatLng(latitude, longitude);
	                        mMap.moveCamera(CameraUpdateFactory.newLatLng(latLng));
	                    }
	                }
	            });
	    return false;
	}
}
```

## 근접 경보 설정

## 사용자 이동 위치 실시간 표시