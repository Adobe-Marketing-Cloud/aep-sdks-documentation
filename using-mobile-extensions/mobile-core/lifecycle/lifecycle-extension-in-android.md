# Lifecycle extension in Android

You can track lifecycle to learn how frequently and how long your app is being used.

**Tip:** The code snippets in this section are only examples. Your final implementation will probably contain additional code that is specific to your app.

**Important**: The Lifecycle extension supports the `MobileCore.lifecycleStart()` and `MobileCore.lifecyclePause()` APIs to track application lifecycle for the Adobe SDK.

## Implementing Lifecycle Metrics in Android <a id="implementing-lifecycle-metrics-in-android"></a>

Tracking lifecycle requires that the Adobe Experience Cloud Platform SDKs have a valid configuration. For more information, see [Configuration Methods in Android](https://launch.gitbook.io/marketing-mobile-sdk-v5-by-adobe-documentation/sdk-core/configuration-methods-in-android).

To implement lifecycle metrics, complete the following steps in each Activity of your application:

1. Import the library:

   ```java
      import com.adobe.marketing.mobile.*;
   ```

2. Register the Lifecycle extension:

   ```java
   public class TargetApp extends Application {​ 
   @Override 
   public void onCreate() {     
       super.onCreate();
       MobileCore.setApplication(this);​     
       try {
           Lifecycle.registerExtension();     
           } catch (Exception e) {         
               //Log the exception     
           } 
    }
   }
   ```

   For more information about registering an extension and setting up the SDK, see .

3. In the `onResume` function, start the lifecycle data collection:

   ```java
      @Override
      public void onResume() {
         MobileCore.setApplication(getApplication());      
         MobileCore.lifecycleStart(null);   
      }
   ```

   **Important:** Setting the Application is only necessary on Activities that are entry points for your application. However, setting the Application on each Activity has no negative impact and also guarantees that the SDK will always have the necessary reference to your Application. As a result, we recommend calling the `setApplication` method in each of your Activities.

4. In the `onPause` function, pause the lifecycle data collection:

   ```java
      @Override   
      public void onPause() {      
         MobileCore.lifecyclePause();   
      }
   ```

**Important:** To ensure accurate session and crash reporting, you must add these calls to every activity.

## Tracking App Crashes in Android <a id="tracking-app-crashes-in-android"></a>

This information helps you understand how crashes are tracked and the best practices to handle false crashes.

**Important**: App crashes are tracked as part of lifecycle metrics. Before you can track crashes, add the library to your project. For more information about implementing lifecycle, see [Implementing Lifecycle Metrics in Android](https://launch.gitbook.io/marketing-mobile-sdk-v5-by-adobe-documentation/lifecycle/lifecycle-extension-in-android#implementing-lifecycle-metrics-in-android).

When lifecycle metrics are implemented, a call is made to `MobileCore.lifecycleStart(additionalContextData)` in the `OnResume` method of each activity. In the `onPause` method, a call is made to `MobileCore.lifecyclePause()`. In the `MobileCore.lifecyclePause()` method, a flag is set to indicate a graceful exit. When the app is launched again or resumed, `MobileCore.lifecycleStart(additionalContextData)` checks this flag. If the app did not exit successfully as determined by the flag status, an `a.CrashEvent` context data is sent with the next call, and a crash event is reported.

**Important**: To ensure accurate crash reporting, you must call `lifecyclePause()` in the `onPause` method of each activity.

To understand why this is essential, here is an illustration of the Android activity lifecycle:![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LEjacBAdplK5nbOMI2b%2F-LHtfLJQuwJ-BOkMS_Vd%2F-LHtgvIovrrVwScLXkyL%2Fandroid-crash.png?alt=media&token=1a7bd350-67b0-405f-aa44-ea012549a525)

For more information about the Android activity lifecycle, see [Activities](https://developer.android.com/guide/components/activities/).

This Android lifecycle illustration was created and shared by the [Android Open Source Project](https://source.android.com/) and used according to terms in the [Creative Commons 2.5 Attribution License](https://creativecommons.org/licenses/by/2.5/).

**What can cause a false crash to be reported?**

* If you are debugging by using an IDE, such as Android Studio, and launching the app again from the IDE while the app is in the foreground causes a crash.

  **Tip**: You can avoid this crash by backgrounding the app before launching again from the IDE.

* If the previous foreground Activity of your app is moved to the background and does not call `MobileCore.lifecyclePause()`in `onPause`, and your app is manually closed or killed by the operating system, the next launch results in a crash.

**How should Fragments be handled?**

Fragments have application lifecycle events that are similar to Activities. However, a Fragment cannot be active without being attached to an Activity.

## Implementing Global Lifecycle Callbacks <a id="implementing-global-lifecycle-callbacks"></a>

Starting with API Level 14, Android allows global lifecycle callbacks for activities. For more information, see the [_Android Developers Guide_](https://developer.android.com/reference/android/app/Application#registerActivityLifecycleCallbacks%28android.app.Application.ActivityLifecycleCallbacks).

You can use these callbacks to ensure that all of your `Activities` correctly call `AdobeMobileMarketing.lifecycleStart()`, and do not need to implement the code for each of the Activity.

```java
import com.adobe.marketing.mobile.*;

public class MainActivity extends Activity {    

@Override    
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);        
    setContentView(R.layout.activity_main);        
    
    getApplication().registerActivityLifecycleCallbacks(new Application.ActivityLifecycleCallbacks() {        
    @Override        
    public void onActivityResumed(Activity activity) {
        MobileCore.setApplication(getApplication());
        MobileCore.lifecycleStart(null);        
        }        
        @Override        
        public void onActivityPaused(Activity activity) { 
            MobileCore.lifecyclePause();        
        }        
        // the following methods aren't needed for our lifecycle purposes, but are        
        // required to be implemented by the ActivityLifecycleCallbacks object        
        @Override        
        public void onActivityCreated(Activity activity, Bundle savedInstanceState) {}        
        @Override        
        public void onActivityStarted(Activity activity) {}        
        @Override        
        public void onActivityStopped(Activity activity) {}        
        @Override        
        public void onActivitySaveInstanceState(Activity activity, Bundle outState) {}        
        @Override        
        public void onActivityDestroyed(Activity activity) {}        
        });    
    }
 ...
}
```

To include additional data with lifecycle metric calls, pass an additional parameter to `lifecycleStart` that contains context data:

```java
@Overridepublic 
void onResume() {    
  HashMap<String, Object> additionalContextData = new HashMap<String, Object>();    
  contextData.put("myapp.category", "Game");    
  MobileCore.lifecycleStart(additionalContextData);}
```

**Important:** You need to add this code only in your main Activity and any other Activity in which your app may be launched.[  
](https://launch.gitbook.io/marketing-mobile-sdk-v5-by-adobe-documentation/lifecycle)

