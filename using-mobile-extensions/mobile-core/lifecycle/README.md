# Lifecycle

Sessions contain information about the current lifecycle such as device information, application install or upgrade information, session start and pause times, number of application launches, plus any additional context data provided by the developer through the `LifecycleStart` API. Session data is persisted, so it is available across application launches.

The Lifecycle framework provides valuable information about your user's current app lifecycle such as  device information, application install or upgrade information, session start and pause times, number of application launches.

## Add Lifecycle to your App

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
 #import <ACPLifecycle_iOS/ACPLifecycle_iOS.h> 
 #import <ACPCore_iOS/ACPCore_iOS.h>
```
{% endtab %}
{% endtabs %}

## Register Lifecycle with Mobile Core

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

   For more information about registering an extension and setting up the SDK, see .

2. In the `onResume` function, start the lifecycle data collection:

   ```java
      @Override  
      public void onResume() {  
         MobileCore.setApplication(getApplication());
         MobileCore.lifecycleStart(null);
      }
   ```

   **Important:** Setting the Application is only necessary on Activities that are entry points for your application. However, setting the Application on each Activity has no negative impact and also guarantees that the SDK will always have the necessary reference to your Application. As a result, we recommend calling the `setApplication` method in each of your Activities.

3. In the `onPause` function, pause the lifecycle data collection:

   ```java
      @Override
      public void onPause() {
         MobileCore.lifecyclePause();
      }
   ```

**Important:** To ensure accurate session and crash reporting, you must add these calls to every activity.
{% endtab %}

{% tab title="iOS" %}
1. Register the Lifecycle extension: In your app's `didFinishLaunchingWithOptions` function register the Lifecycle extensions

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPLifecycle registerExtension];
​
  // Override point for customization after application launch.
  return YES;
}
```
{% endtab %}
{% endtabs %}

## Lifecycle metrics

The following is a complete list of all of the metrics provided on your user's app lifecycle.

### Install

| **Metric** | **Key** | **DescriptIon** |
| :--- | :--- | :--- |
| First Launches | a.InstallEvent | Triggered at the first run after installation or re-installation. |
| Install Date | a.InstallDate | Date of first launch after installation. The format is `M/d/yyyy`, and an example is `5/3/2017`. |

### Upgrade

| **Metric** | **Key** | **Description** |
| :--- | :--- | :--- |
| Upgrades | a.UpgradeEvent | Triggered at the first run after upgrade or anytime the version number changes. |
| Days since last upgrade | a.DaysSinceLastUpgrade | Number of days since the application version number has changed. |
| Launches since last upgrade | a.LaunchesSinceUpgrade | Number of launches since the application version number has changed. |

### Launch

| **Metric** | **Key** | **Description** |
| :--- | :--- | :--- |
| Daily Engaged Users | a.DailyEngUserEvent | Triggered when the application is used on a particular day.    **Important**: This metric is not automatically stored in an Analytics metric. You must create a processing rule that sets a custom event to capture this metric. |
| Monthly Engaged Users | a.MonthlyEngUserEvent | Triggered when the application is used during a particular month.    **Important**: This metric is not automatically stored in an Analytics metric. You must create a processing rule that sets a custom event to capture this metric. |
| Launches | a.LaunchEvent | Triggered on every run, including crashes and installs. Also triggered when the app is resumed from the background after the lifecycle session timeout is exceeded. |
| Previous Session Length | a.PrevSessionLength | Reports the number of seconds that a previous application session lasted based on how long the application was open and in the foreground |
| Ignored Session Length | a.ignoredSessionLength | If the last session is set to last longer than `lifecycle.sessionTimeout`, that session length is ignored and recorded here. |
| Launch Number | a.Launches | Number of times the application was launched or brought out of the background. |
| Days since first use | a.DaysSinceFirstUse | Number of days since first run. |
| Days since last use | a.DaysSinceLastUse | Number of days since last use. |
| Hour of Day | a.HourOfDay | Measures the hour the app was launched and uses the 24-hour numerical format. Used for time parting to determine peak usage times. |
| Day of Week | a.DayOfWeek | Measures the day of the week the app was launched. |

### Crash

| **Metric** | **Key** | **Description** |
| :--- | :--- | :--- |
| Crashes | a.CrashEvent | Triggered when the application crashed before closing. The event is sent when the application is started again after the crash. |

### Device Information

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Metric</b>
      </th>
      <th style="text-align:left"><b>Key</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">App ID</td>
      <td style="text-align:left">a.AppID</td>
      <td style="text-align:left">Stores the application name and version in the following format: <code>AppName BundleVersion (app version code)</code> .
        An example of this format is MyAppName 1.1(1)</td>
    </tr>
    <tr>
      <td style="text-align:left">Device Name</td>
      <td style="text-align:left">a.DeviceName</td>
      <td style="text-align:left">Stores the device name.</td>
    </tr>
    <tr>
      <td style="text-align:left">Operating System Version</td>
      <td style="text-align:left">a.OSVersion</td>
      <td style="text-align:left">Operating system name and version.</td>
    </tr>
    <tr>
      <td style="text-align:left">Carrier Name</td>
      <td style="text-align:left">a.CarrierName</td>
      <td style="text-align:left">
        <p>Stores the name of the mobile service provider as provided by the device.
          <br
          />
        </p>
        <p><b>Important</b>: This metric is not automatically stored in an Analytics
          variable. You must create a processing rule to copy this value to an Analytics
          variable for reporting.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Resolution</td>
      <td style="text-align:left">a.Resolution</td>
      <td style="text-align:left">Width x Height in pixels.</td>
    </tr>
    <tr>
      <td style="text-align:left">Locale</td>
      <td style="text-align:left">a.locale</td>
      <td style="text-align:left">Locale set for this device, for example, <em>en-US</em>.</td>
    </tr>
    <tr>
      <td style="text-align:left">Run mode</td>
      <td style="text-align:left">a.RunMode</td>
      <td style="text-align:left">The SDK running mode, for example, <code>Application / Extension</code>.</td>
    </tr>
  </tbody>
</table>## Configuration Keys

If you need to update SDK configuration, programmatically, please use the following information to change your Lifecycle configuration values. For more information, please see [Configuration Methods Reference](../configuration-reference.md).

{% hint style="warning" %}
The time that your app spends in the background is not included in the session length.
{% endhint %}

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">lifecycle.sessionTimeout</td>
      <td style="text-align:left">
        <p>Time, in seconds, that must elapse between the time the app is launched
          and before the launch is considered to be a new session. This timeout also
          applies when your application is sent to the background and reactivated.</p>
        <p></p>
        <p>Default value is 300 seconds (5 minutes).</p>
      </td>
    </tr>
  </tbody>
</table>## 

