#  안드로이드스튜디오 템플릿을 활용한 프로젝트 생성하기

## 네비게이션 드로어 프로젝트 생성 및 코드 분석

![NavigationDrawerExample](./Imgs/NavigationDrawerExample.JPG)

### MainActivity.java

```java
public class MainActivity extends AppCompatActivity
        implements NavigationView.OnNavigationItemSelectedListener {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        // 툴바를 상단의 앱바로 설정한다
        Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);

        // Fab의 클릭 리스너를 설정한다
        FloatingActionButton fab = (FloatingActionButton) findViewById(R.id.fab);
        fab.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                // 스낵바가 생성된다
                Snackbar.make(view, "Replace with your own action", Snackbar.LENGTH_LONG)
                        .setAction("Action", null).show();
            }
        });

        // 드로우어를 토글 버튼과 연동시킨다
        DrawerLayout drawer = (DrawerLayout) findViewById(R.id.drawer_layout);
        ActionBarDrawerToggle toggle = new ActionBarDrawerToggle(
                this, drawer, toolbar, R.string.navigation_drawer_open, R.string.navigation_drawer_close);
        drawer.setDrawerListener(toggle);
        toggle.syncState();

        // 네비게이션 뷰의 아이템 클릭 리스너를 설정한다
        NavigationView navigationView = (NavigationView) findViewById(R.id.nav_view);
        navigationView.setNavigationItemSelectedListener(this);
    }

    @Override
    public void onBackPressed() {
        // 백버튼을 눌렀을 때 드로우어가 열려있으면 닫아주고 아니면 기본 작업을 한다
        DrawerLayout drawer = (DrawerLayout) findViewById(R.id.drawer_layout);
        if (drawer.isDrawerOpen(GravityCompat.START)) {
            drawer.closeDrawer(GravityCompat.START);
        } else {
            super.onBackPressed();
        }
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        // 메뉴를 팽창시킨다
        getMenuInflater().inflate(R.menu.main, menu);
        return true;
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        // 메뉴 아이템의 선택 이벤트를 설정해준다
        int id = item.getItemId();

        // 세팅 메뉴를 선택하였을 때
        if (id == R.id.action_settings) {
            return true;
        }

        return super.onOptionsItemSelected(item);
    }

    @SuppressWarnings("StatementWithEmptyBody")
    @Override
    public boolean onNavigationItemSelected(MenuItem item) {
        // 네비게이션의 아이템 선택 이벤트를 설정해준다
        int id = item.getItemId();

        if (id == R.id.nav_camera) {
            // Handle the camera action
        } else if (id == R.id.nav_gallery) {

        } else if (id == R.id.nav_slideshow) {

        } else if (id == R.id.nav_manage) {

        } else if (id == R.id.nav_share) {

        } else if (id == R.id.nav_send) {

        }

        // 모든 처리가 끝난 후에 드로우어를 닫아준다
        DrawerLayout drawer = (DrawerLayout) findViewById(R.id.drawer_layout);
        drawer.closeDrawer(GravityCompat.START);
        return true;
    }
}
```

### activity_main.xml

```java
<?xml version="1.0" encoding="utf-8"?>
<android.support.v4.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fitsSystemWindows="true"
    tools:openDrawer="start">
    <!-- 액티비티의 앱 바 와 컨텐츠 -->
    <include
        layout="@layout/app_bar_main"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
    <!-- 액티비티의 네비게이션 뷰 -->
    <android.support.design.widget.NavigationView
        android:id="@+id/nav_view"
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        android:fitsSystemWindows="true"
        app:headerLayout="@layout/nav_header_main"
        app:menu="@menu/activity_main_drawer" />
</android.support.v4.widget.DrawerLayout>
```

### app_bar_main

```java
<?xml version="1.0" encoding="utf-8"?>
<android.support.design.widget.CoordinatorLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.project.boostcamp.navigationdrawerexample.MainActivity">
    <!-- 앱 바 -->
    <android.support.design.widget.AppBarLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:theme="@style/AppTheme.AppBarOverlay">
        <!-- 툴 바 -->
        <android.support.v7.widget.Toolbar
            android:id="@+id/toolbar"
            android:layout_width="match_parent"
            android:layout_height="?attr/actionBarSize"
            android:background="?attr/colorPrimary"
            app:popupTheme="@style/AppTheme.PopupOverlay" />
    </android.support.design.widget.AppBarLayout>
    <!-- 컨텐츠 -->
    <include layout="@layout/content_main" />
    <!-- FAB -->
    <android.support.design.widget.FloatingActionButton
        android:id="@+id/fab"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="bottom|end"
        android:layout_margin="@dimen/fab_margin"
        app:srcCompat="@android:drawable/ic_dialog_email" />
</android.support.design.widget.CoordinatorLayout>
```

## 하단 네비게이션 프로젝트 생성 및 코드 분석

![BottomNavigationExample](./Imgs/BottomNavigationExample.JPG)

### MainActivity.java

```java
public class MainActivity extends AppCompatActivity {
    private TextView mTextMessage; // 화면에 표시될 텍스트
    // 하단 네비게이션 아이템 선택 리스너
    private BottomNavigationView.OnNavigationItemSelectedListener mOnNavigationItemSelectedListener
            = new BottomNavigationView.OnNavigationItemSelectedListener() {

        @Override
        public boolean onNavigationItemSelected(@NonNull MenuItem item) {
            switch (item.getItemId()) {
                case R.id.navigation_home:
                    mTextMessage.setText(R.string.title_home);
                    return true;
                case R.id.navigation_dashboard:
                    mTextMessage.setText(R.string.title_dashboard);
                    return true;
                case R.id.navigation_notifications:
                    mTextMessage.setText(R.string.title_notifications);
                    return true;
            }
            return false;
        }

    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        // 텍스트 뷰 바인딩
        mTextMessage = (TextView) findViewById(R.id.message);
        // 하단 네비게이션 뷰 바인딩
        BottomNavigationView navigation = (BottomNavigationView) findViewById(R.id.navigation);
        // 하단 네비게이션 뷰 아이템 선택 리스너 설정
        navigation.setOnNavigationItemSelectedListener(mOnNavigationItemSelectedListener);
    }
}
```

### BottomNavigationView

```xml
<android.support.design.widget.BottomNavigationView
        android:id="@+id/navigation"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_gravity="bottom"
        android:background="?android:attr/windowBackground"
        app:menu="@menu/navigation" />
```

### menu/navigation

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@+id/navigation_home"
        android:icon="@drawable/ic_home_black_24dp"
        android:title="@string/title_home" />
    <item
        android:id="@+id/navigation_dashboard"
        android:icon="@drawable/ic_dashboard_black_24dp"
        android:title="@string/title_dashboard" />
    <item
        android:id="@+id/navigation_notifications"
        android:icon="@drawable/ic_notifications_black_24dp"
        android:title="@string/title_notifications" />
</menu>
```

## 구글 맵 프로젝트 생성 및 코드 분석

![GoogleMapsExample](./Imgs/GoogleMapsExample.JPG)

### MainActivity.java

```java
public class MapsActivity extends FragmentActivity implements OnMapReadyCallback {
    private GoogleMap mMap; // 구글 맵

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_maps);
        // 맵 프래그먼트를 바인딩 한 후 맵이 준비가 되면 알림을 받을 수 있도록 한다.
		// R.id.map 은 단순한 프래그먼트
        SupportMapFragment mapFragment = (SupportMapFragment) getSupportFragmentManager()
                .findFragmentById(R.id.map);
        mapFragment.getMapAsync(this);
    }
    // 맵이 준비가 되었을 때 발생하는 이벤트
    @Override
    public void onMapReady(GoogleMap googleMap) {
        mMap = googleMap;
        // 시드니에 마커를 추가하는 부분
        LatLng sydney = new LatLng(-34, 151);
        mMap.addMarker(new MarkerOptions().position(sydney).title("Marker in Sydney"));
        mMap.moveCamera(CameraUpdateFactory.newLatLng(sydney));
    }
}
```

### activity_maps.xml

```xml
<fragment xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:map="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/map"
    android:name="com.google.android.gms.maps.SupportMapFragment"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.project.boostcamp.googlemapexample.MapsActivity" />
```

### google_maps_api.xml

구글 맵스를 사용하기 전에 구글 API 콘솔 사이트로 이동하여 API키를 발급 받아야한다.

[구글 API 콘솔](https://developers.google.com/maps/documentation/android/start#get-key)

그리고 API키의 제한을 걸기 위해서 패키지 이름과 SHA-1 인증키가 필요하다. 이는 예제 프로젝트를 생성하였을 때에는 바로 알려준

```xml
<resources>
    <string name="google_maps_key" templateMergeStrategy="preserve" translatable="false">AIzaSyAvK-E2GGSG-EvAdiBo8jRxWJpNwThwcLc</string>
</resources>
```