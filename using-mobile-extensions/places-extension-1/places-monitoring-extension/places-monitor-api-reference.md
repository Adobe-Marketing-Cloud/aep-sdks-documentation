# Places Monitor API reference

## Register Places Monitor Extension

Registers the Places Monitor extension with the Core Event Hub.

{% tabs %}
{% tab title="Android" %}
### RegisterExtension

#### Syntax

```java
public static void registerExtension();
```

#### Example

Call this method in the `onCreate` method where you initialize the rest of the Experience Platform SDK.

```java
public class MobileApp extends Application {
  @Override
  public void onCreate(){
     super.onCreate();
     MobileCore.setApplication(this);
     try {
        PlacesMonitor.registerExtension();
     } catch (Exception e) {
       //Log the exception
       }
    }
 }
```
{% endtab %}

{% tab title="iOS" %}
### RegisterExtension

#### Syntax

```objectivec
+ (void) registerExtension;
```

#### Example

This method should be called in the `didFinishLaunchingWithOptions` delegate method of the `AppDelegate`.

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    [ACPCore configureWithAppId:@"launch-appID"];    
    [ACPPlaces registerExtension];    
    [ACPPlacesMonitor registerExtension];

    [ACPCore start:^{
        // do other initialization of the SDK
    }];

    return YES;
}
```
{% endtab %}
{% endtabs %}

## Extension version

Returns the current version of the Places Monitor extension

{% tabs %}
{% tab title="Android" %}
### ExtensionVersion

#### Syntax

```java
public static String extensionVersion();
```

#### Example

```java
String placesMonitorVersion = PlacesMonitor.extensionVersion();
```
{% endtab %}

{% tab title="iOS" %}
### ExtensionVersion

#### Syntax

```objectivec
+ (nonnull NSString*) extensionVersion;
```

#### Example

```objectivec
NSString *placesMonitorVersion = [ACPPlacesMonitor extensionVersion];
```
{% endtab %}
{% endtabs %}

## Start device monitoring

Begin tracking the device's location and monitoring nearby Places.

{% tabs %}
{% tab title="Android" %}
### Start

If authorization to use device location has not been granted by the user, the first call to the `start` API will prompt the user for permission.

#### Syntax

```java
public static void start();
```

#### Example

```java
PlacesMonitor.start();
```
{% endtab %}

{% tab title="iOS" %}
### Start

**Important**: To begin monitoring, the location service must have the necessary authorization.

* If the authorization for the location service has not been provided to the application, the first call to the `start` API requests the authorization to use the location service as configured for the application.
* Depending on your device's capabilities, if the authorization has been provided, the Places Monitor tracks the user's location based on the currently set `ACPPlacesMonitorMode`.

  By default, the monitor uses `ACPPlacesMonitorModeSignificantChanges`.

#### Syntax

```objectivec
+ (void) start;
```

#### Example

```objectivec
[ACPPlacesMonitor start];
```
{% endtab %}
{% endtabs %}

## Stop device monitoring

Stops tracking the device's location.

{% tabs %}
{% tab title="Android" %}
### Stop

#### Syntax

```java
public static void stop();
```

#### Example

```java
PlacesMonitor.stop();
```
{% endtab %}

{% tab title="iOS" %}
### Stop

#### Syntax

```objectivec
+ (void) stop;
```

#### Example

```objectivec
[ACPPlacesMonitor stop];
```
{% endtab %}
{% endtabs %}

## Update Location

Use this API for an immediate update on the device's location. When you call this API, the device attempts to determine the location with the level of accuracy that you specified. This process also refreshes the nearby POIs that are monitored by the extension.

{% tabs %}
{% tab title="Android" %}
### UpdateLocation

#### Syntax

```java
public static void updateLocation();
```

#### Example

```java
PlacesMonitor.updateLocation();
```
{% endtab %}

{% tab title="iOS" %}
### UpdateLocationNow

#### Syntax

```objectivec
+ (void) updateLocationNow;
```

#### Example

```objectivec
[ACPPlacesMonitor updateLocationNow];
```
{% endtab %}
{% endtabs %}

## Monitoring Mode \(iOS only\)

Monitoring can be set to one of the following values:

* `ACPPlacesMonitorModeContinuous`

  The monitoring extension receives and processes locations more frequently. This monitoring strategy consumes a lot of power but provides higher accuracy. For more information, see [Apple documentation on continuous monitoring](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423750-startupdatinglocation).

* `ACPPlacesMonitorModeSignificantChanges`

  The monitoring extension only receives and processes location updates after the device has moved a significant distance from the previously processed location. This monitoring strategy consumes less power than the continuous monitoring strategy. For more information, see [Apple documentation on significant monitoring](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423531-startmonitoringsignificantlocati)

{% tabs %}
{% tab title="iOS" %}
### SetPlacesMonitorMode

#### Syntax

```text
+ (void) setPlacesMonitorMode: (ACPPlacesMonitorMode) monitorMode;
```

#### Example

```text
[ACPPlacesMonitor setPlacesMonitorMode:ACPPlacesMonitorModeSignificantChanges];
```
{% endtab %}
{% endtabs %}

