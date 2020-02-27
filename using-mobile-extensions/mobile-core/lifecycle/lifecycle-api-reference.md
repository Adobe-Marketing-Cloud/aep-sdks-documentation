# Lifecycle API reference

## Lifecycle Start

You can use this API to start a new lifecycle session or resume a previously paused lifecycle session. If a previously paused session timed out, then a new session is created. If a current session is running, then calling this method does nothing.

### lifecycleStart <a id="lifecycleStart"></a>

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public static void lifecycleStart(final Map<String, String> additionalContextData);
```
**Example**

```java
Identity.syncIdentifier("idType", 
                        "idValue", 
                        VisitorID.AuthenticationState.AUTHENTICATED);
```
{% endtab %}

{% hint style="warning" %}
This method should be called from the Activity onResume method.
{% endhint %}


### Collect additional data with Lifecycle

Additional context data may be passed when calling this method. Lifecycle data and any additional data are sent as context data parameters to Analytics, to Target as mbox parameters, and for Audience Manager they are sent as customer variables. Any additional data is also used by the Rules Engine when processing rules.

{% hint style="warning" %}
If you want to track additional context data, you need to add this code in your main activity and any other activity from which your app can be launched.
{% endhint %}

```java
@Override
public void onResume() {
    HashMap<String, Object> additionalContextData = new HashMap<String, Object>();
    contextData.put("myapp.category", "Game");
    MobileCore.lifecycleStart(additionalContextData);
}
```

{% endtab %}

{% tab title="iOS" %}

#### Objective-C

```objectivec
// Objective-C
- (void) applicationWillEnterForeground:(UIApplication *)application {      
    [ACPCore lifecycleStart:@{@"state": @"appResume"}];      
}
```

#### Swift

```swift
// Swift
func applicationWillEnterForeground(_ application: UIApplication) {      
    ACPCore.lifecycleStart(["state": "appResume"])
}
```

{% endtab %}

{% tab title="React Native" %}

#### JavaScript

```jsx
ACPCore.lifecycleStart({"lifecycleStart": "myData"});
```

{% endtab %}
{% endtabs %}









{% tabs %}
{% tab title="Android" %}
Import the Lifecycle framework:

```java
import com.adobe.marketing.mobile.*;
```

Register the framework with Mobile Core:

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

With the `onResume` function, start Lifecycle data collection:

```java
@Override  
   public void onResume() {  
      MobileCore.setApplication(getApplication());
      MobileCore.lifecycleStart(null);
   }
```

{% hint style="info" %}
Setting the application is only necessary on activities that are entry points for your application. However, setting the application on each Activity has no negative impact and ensures that the SDK always has the necessary reference to your application. In each of your activities, call`setApplication`.
{% endhint %}

To pause the lifecycle data collection, use the `onPause` function.

{% hint style="info" %}
To ensure accurate session and crash reporting, this call must be added to every activity.
{% endhint %}

```java
@Override
   public void onPause() {
      MobileCore.lifecyclePause();
   }
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C & Swift <a id="objective-c-and-swift"></a>

The `lifecycleStart:` method tells the SDK that the user is launching the app. It should be called from both entry points in your `AppDelegate`:

* `application:didFinishLaunchingWithOptions:`  
* `applicationWillEnterForeground:`

{% endtab %}

{% tab title="React Native" %}
### JavaScript

> Tip: Implementing Lifecycle via Javascript may lead to inaccurate Lifecycle metrics. As a result, we recommend that you implement Lifecycle in native [Android and iOS code](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle). However, if you need to implement Lifecycle in Javascript, you can use [`AppState`](https://facebook.github.io/react-native/docs/appstate) to receive notifications about when your app enters foreground/background. Based on the `AppState` you can make the corresponding calls to `lifecycleStart` and `lifecyclePause`.

Import the Lifecycle extension

```jsx
import {ACPLifecycle} from '@adobe/react-native-acpcore';
```

Get the extension version

```jsx
ACPLifecycle.extensionVersion().then(version => console.log("AdobeExperienceSDK: ACPLifecycle version: " + version));
```

Registering the extension with Core

```jsx
ACPLifecycle.registerExtension();
```

Starting a lifecycle event

```jsx
ACPCore.lifecycleStart({"lifecycleStart": "myData"});
```

Pausing a lifecycle event

```jsx
ACPCore.lifecyclePause();
```
{% endtab %}
{% endtabs %}

## Collect additional data with Lifecycle

When you call [Lifecycle start](lifecycle-api-reference.md#lifecycle-start-and-pause) you can, optionally, pass a dictionary of additional data that will be attached to the lifecycle event.

{% hint style="info" %}
You can pass additional data to lifecycle on app launch, app resume, both, or neither.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

{% hint style="warning" %}
You need to add this code in your main activity and any other activity from which your app can be launched.
{% endhint %}

```java
@Override
public void onResume() {
    HashMap<String, Object> additionalContextData = new HashMap<String, Object>();
    contextData.put("myapp.category", "Game");
    MobileCore.lifecycleStart(additionalContextData);
}
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

```objectivec
// Objective-C
- (void) applicationWillEnterForeground:(UIApplication *)application {      
    [ACPCore lifecycleStart:@{@"state": @"appResume"}];      
}
```

#### Swift

```swift
// Swift
func applicationWillEnterForeground(_ application: UIApplication) {      
    ACPCore.lifecycleStart(["state": "appResume"])
}
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

```jsx
ACPCore.lifecycleStart({"lifecycleStart": "myData"});
```
{% endtab %}
{% endtabs %}