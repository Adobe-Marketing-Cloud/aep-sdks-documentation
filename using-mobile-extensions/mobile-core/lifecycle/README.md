# Lifecycle

{% hint style="warning" %}
In version 4 of the iOS SDK, this implementation was completed automatically.

The Experience Platform SDK will not automatically collect Lifecycle metrics. To continue collecting Lifecycle metrics, you must add code to your app. For more information, see [Manual Lifecycle Implementation](https://aep-sdks.gitbook.io/docs/resources/upgrading-to-aep/manual-lifecycle-implementation).
{% endhint %}

Sessions contain information about the app's current lifecycle, such as the device information, the application install or upgrade information, the session start and pause times, the number of application launches, and additional context data that is provided by the developer through the `LifecycleStart` API. Session data is persisted, so it is available across application launches.

## Add Lifecycle to your app

{% tabs %}
{% tab title="Android" %}
1. Import the library:

```java
   import com.adobe.marketing.mobile.*;
```
{% endtab %}

{% tab title="iOS" %}
1. Import the library:

```objectivec
 #import "ACPLifecycle.h"
 #import "ACPCore.h"
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

Import the Lifecycle extension

```jsx
import {ACPLifecycle} from '@adobe/react-native-acpcore';
```

Get the extension version

```jsx
ACPLifecycle.extensionVersion().then(version => console.log("AdobeExperienceSDK: ACPLifecycle version: " + version));
```
{% endtab %}
{% endtabs %}

## Register Lifecycle with Mobile Core and add appropriate Start/Pause calls

{% tabs %}
{% tab title="Android" %}
1. Register the Lifecycle extension:

   ```java
   public class TargetApp extends Application {
   ​
    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
   ​
        try {
            Lifecycle.registerExtension();
        } catch (Exception e) {
            //Log the exception
        }
    }
   }
   ```

2. In the `onResume` function, start the lifecycle data collection:

   ```java
      @Override  
      public void onResume() {  
         MobileCore.setApplication(getApplication());
         MobileCore.lifecycleStart(null);
      }
   ```

   **Important:** Setting the application is only necessary on Activities that are entry points for your application. However, setting the application on each Activity has no negative impact and also guarantees that the SDK always has the necessary reference to your application. As a result, we recommend calling the `setApplication` method in each of your Activities.

3. In the `onPause` function, pause the lifecycle data collection:

   ```java
      @Override
      public void onPause() {
         MobileCore.lifecyclePause();
      }
   ```

**Important:** To ensure accurate session and crash reporting, add these calls to every activity.
{% endtab %}

{% tab title="iOS" %}
1. Register the Lifecycle extension: In your app's `didFinishLaunchingWithOptions` function register the Lifecycle extensions

   ```objectivec
   - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
     [ACPLifecycle registerExtension];

     // Override point for customization after application launch.
     return YES;
   }
   ```

2. Start Lifecycle data collection by calling `lifecycleStart:` from the callback of the `ACPCore::start:` method in your app's `application:didFinishLaunchingWithOptions:` delegate method. 



   ```objectivec
   - (BOOL) application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           // register the lifecycle extension
           [ACPLifecycle registerExtension];

           const UIApplicationState appState = application.applicationState;
           [ACPCore start:^{
               // only start lifecycle if the application is not in the background
               if (appState != UIApplicationStateBackground) {
                   [ACPCore lifecycleStart:nil];
               }
           }];
       }
   ```

3. When your app is launched, if it is resuming from a backgrounded state, iOS might call your `applicationWillEnterForeground:` delegate method. You also need to call `lifecycleStart:`, but this time you do not need all of the supporting code that you used in `application:didFinishLaunchingWithOptions:`:

   ```objectivec
   - (void) applicationWillEnterForeground:(UIApplication *)application {
       [ACPCore lifecycleStart:nil];
   }
   ```

4. When the app enters the background, pause Lifecycle data collection from your app's `applicationDidEnterBackground:` delegate method:

   ```objectivec
    - (void) applicationDidEnterBackground:(UIApplication *)application {
       [ACPCore lifecyclePause];
    }
   ```
{% endtab %}

{% tab title="React Native" %}
**Registering the extension with Core:**

```jsx
ACPLifecycle.registerExtension();
```

**Starting a lifecycle event:**

```jsx
ACPCore.lifecycleStart({"lifecycleStart": "myData"});
```

**Pausing a lifecycle event:**

```jsx
ACPCore.lifecyclePause();
```
{% endtab %}
{% endtabs %}

## Lifecycle metrics

The following is a complete list of all of the metrics provided on your user's app lifecycle.

### Install

| **Metric** | **Key** | **DescriptIon** |
| :--- | :--- | :--- |
| First Launches | `a.InstallEvent` | Triggered at the first run after installation or re-installation. |
| Install Date | `a.InstallDate` | Date of first launch after installation. The format is `M/d/yyyy`, and an example is `5/3/2017`. |

### Upgrade

| **Metric** | **Key** | **Description** |
| :--- | :--- | :--- |
| Upgrades | `a.UpgradeEvent` | Triggered at the first run after upgrade or when the version number changes. |
| Days since last upgrade | `a.DaysSinceLastUpgrade` | Number of days since the application version number  changed. |
| Launches since last upgrade | `a.LaunchesSinceUpgrade` | Number of launches since the application version number changed. |

### Launch

| **Metric** | **Key** | **Description** |
| :--- | :--- | :--- |
| Daily Engaged Users | `a.DailyEngUserEvent` | Triggered when the application is used on a particular day.     **Important**: This metric is not automatically stored in an Analytics metric. You must create a processing rule that sets a custom event to capture this metric. |
| Monthly Engaged Users | `a.MonthlyEngUserEvent` | Triggered when the application is used during a particular month. **Important**: This metric is not automatically stored in an Analytics metric. You must create a processing rule that sets a custom event to capture this metric. |
| Launches | `a.LaunchEvent` | Triggered on every run, including crashes and installs. Also triggered when the app is resumed from the background after the lifecycle session timeout is exceeded. |
| Previous Session Length | `a.PrevSessionLength` | Reports the number of seconds that a previous application session lasted based on how long the application was open and in the foreground. |
| Ignored Session Length | `a.ignoredSessionLength` | If the last session is set to last longer than `lifecycle.sessionTimeout`, that session length is ignored and recorded here. |
| Launch Number | `a.Launches` | Number of times the application was launched or brought out of the background. |
| Days since first use | `a.DaysSinceFirstUse` | Number of days since first run. |
| Days since last use | `a.DaysSinceLastUse` | Number of days since last use. |
| Hour of Day | `a.HourOfDay` | Measures the hour the app was launched and uses the 24-hour numerical format. Used for time parting to determine peak usage times. |
| Day of Week | `a.DayOfWeek` | Measures the day of the week the app was launched. |

### Crash

| **Metric** | **Key** | **Description** |
| :--- | :--- | :--- |
| Crashes | `a.CrashEvent` | Triggered when the application crashed before closing. The event is sent when the application is started again after the crash. |

### Device Information

<table>
  <thead>
    <tr>
      <th style="text-align:left">Metric</th>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">AppID</td>
      <td style="text-align:left"><code>a.AppID</code>
      </td>
      <td style="text-align:left">Stores the application name and version in the <code>AppName BundleVersion (app version code)</code> format.
        An example of this format is <code>MyAppName 1.1(1)</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left">Device name</td>
      <td style="text-align:left"><code>a.DeviceName</code>
      </td>
      <td style="text-align:left">Stores the device name.</td>
    </tr>
    <tr>
      <td style="text-align:left">Operating system version</td>
      <td style="text-align:left"><code>a.OSVersion</code>
      </td>
      <td style="text-align:left">Operating system name and version.</td>
    </tr>
    <tr>
      <td style="text-align:left">Carrier name</td>
      <td style="text-align:left"><code>a.CarrierName</code>
      </td>
      <td style="text-align:left">
        <p>Stores the name of the mobile service provider as provided by the devices.</p>
        <p>Important: This metric is not automatically stored in an Analytics variable.
          For reporting, you must create a processing rule to copy this value to
          an Analytics variable.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Resolution</td>
      <td style="text-align:left"><code>a.Resolution</code>
      </td>
      <td style="text-align:left">Width x height, in pixels.</td>
    </tr>
    <tr>
      <td style="text-align:left">Locale</td>
      <td style="text-align:left"><code>a.Locale</code>
      </td>
      <td style="text-align:left">Locale set for this device, for example, <em>en-US</em>.</td>
    </tr>
    <tr>
      <td style="text-align:left">Run mode</td>
      <td style="text-align:left"><code>a.RunMode</code>
      </td>
      <td style="text-align:left">The SDK running mode, for example, <code>Application/Extension</code>.</td>
    </tr>
  </tbody>
</table>If you need to programmatically update your SDK configuration, use the following information to change your Lifecycle configuration values: {% hint style="warning" %} The time that your app spends in the background is not included in the session length. {% endhint %}.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>lifecycle.sessionTimeout</code>
      </td>
      <td style="text-align:left">
        <p>Time, in seconds, that must elapse between the time the app is launched
          and before the launch is considered to be a new session. This timeout also
          applies when your application is sent to the background and reactivated.</p>
        <p>Default value is 300 seconds (5 minutes).</p>
      </td>
    </tr>
  </tbody>
</table>