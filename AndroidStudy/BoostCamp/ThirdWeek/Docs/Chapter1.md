# 서비스 살펴보기

## 서비스의 이해

### 특징

- 서비스는 **백그라운드**에서 오래 실행되는 작업을 수행할 때 사용한다.
- 다른 어플리케이션 구성요소가 서비스를 시작할 수 있고 계속해서 실행이 된다.
- 구성 요소를 서비스에 바인드하여 서비스와 상호작용할 수 있다.

## 서비스 생명주기 메소드

![Service Life Cycle](https://developer.android.com/images/service_lifecycle.png?hl=ko)

## 서비스 실행 및 중지

### startService()
- 서비스를 '시작'상태로 실행시킨다. 무기한으로 실행될 수 있다.
- onStartCommand()이 호출된다.
- 종료하려면 stopSelf() 또는 stopService()를 호출한다.

### bindService()
- 서비스를 '바인드'상태로 실행시킨다.
- 클라이언트-서버 인터페이스를 제공하여 상호작용할 수 있도록 해준다.
- 여러 개의 구성 요소가 서비스에 바인드될 수 있지만, 모두 해제되면 서비스는 소멸된다.
- onBind()가 호출된다.
- 상호작용을 위해서는 IBinder를 반환해야하며 허용하지 않으려면 null을 반환해야 한다.

### Service vs IntentService

- Service
	- 모든 서비스의 기본 클래스.
	- 이 클래스를 상속 받아서 사용할 경우에는 새 스레드를 만드는 것이 중요하다. 서비스가 기본적으로 애플리케이션의 기본 스레드를 사용하기 때문. 모든 액티비티의 성능이 느려질 수 있다.
	- UI와 관련되지 않은 작업에 사용되며 수행시간이 길어선 안된다. 긴 작업이 필요하다면 스레드를 가지고 사용해야한다.
	- startService()또는 bindService()로 시작한다.
	- onStartCommand()또는 onBind()가 호출된다.

- IntentService
	- 보통 긴 작업에 사용되며 메인 스레드와 상호작용하지 않는다. 상호작용이 필요하다면 Handler혹은 Broadcast Intent를 사용하면 된다.
	- Callback이 요구되는 상황에서도 사용된다. (특정 작업 intent)
	- Intent를 사용하여 시작한다.
	- onHandleIntent()가 호출된다.

```java
public class HelloIntentService extends IntentService {

  /**
   * A constructor is required, and must call the super IntentService(String)
   * constructor with a name for the worker thread.
   */
  public HelloIntentService() {
      super("HelloIntentService");
  }

  /**
   * The IntentService calls this method from the default worker thread with
   * the intent that started the service. When this method returns, IntentService
   * stops the service, as appropriate.
   */
  @Override
  protected void onHandleIntent(Intent intent) {
      // Normally we would do some work here, like download a file.
      // For our sample, we just sleep for 5 seconds.
      try {
          Thread.sleep(5000);
      } catch (InterruptedException e) {
          // Restore interrupt status.
          Thread.currentThread().interrupt();
      }
  }
  @Override
  public int onStartCommand(Intent intent, int flags, int startId) {
      Toast.makeText(this, "service starting", Toast.LENGTH_SHORT).show();
      return super.onStartCommand(intent,flags,startId);
  }
}
```

```java
public class HelloService extends Service {
  private Looper mServiceLooper;
  private ServiceHandler mServiceHandler;

  // Handler that receives messages from the thread
  private final class ServiceHandler extends Handler {
      public ServiceHandler(Looper looper) {
          super(looper);
      }
      @Override
      public void handleMessage(Message msg) {
          // Normally we would do some work here, like download a file.
          // For our sample, we just sleep for 5 seconds.
          try {
              Thread.sleep(5000);
          } catch (InterruptedException e) {
              // Restore interrupt status.
              Thread.currentThread().interrupt();
          }
          // Stop the service using the startId, so that we don't stop
          // the service in the middle of handling another job
          stopSelf(msg.arg1);
      }
  }

  @Override
  public void onCreate() {
    // Start up the thread running the service.  Note that we create a
    // separate thread because the service normally runs in the process's
    // main thread, which we don't want to block.  We also make it
    // background priority so CPU-intensive work will not disrupt our UI.
    HandlerThread thread = new HandlerThread("ServiceStartArguments",
            Process.THREAD_PRIORITY_BACKGROUND);
    thread.start();

    // Get the HandlerThread's Looper and use it for our Handler
    mServiceLooper = thread.getLooper();
    mServiceHandler = new ServiceHandler(mServiceLooper);
  }

  @Override
  public int onStartCommand(Intent intent, int flags, int startId) {
      Toast.makeText(this, "service starting", Toast.LENGTH_SHORT).show();

      // For each start request, send a message to start a job and deliver the
      // start ID so we know which request we're stopping when we finish the job
      Message msg = mServiceHandler.obtainMessage();
      msg.arg1 = startId;
      mServiceHandler.sendMessage(msg);

      // If we get killed, after returning from here, restart
      return START_STICKY;
  }

  @Override
  public IBinder onBind(Intent intent) {
      // We don't provide binding, so return null
      return null;
  }

  @Override
  public void onDestroy() {
    Toast.makeText(this, "service done", Toast.LENGTH_SHORT).show();
  }
}
```