# Places Monitor API reference

## Register Places Monitor Extension

Registers the `ACPPlacesMonitor` extension with the Core Event Hub.

{% tabs %}
{% tab title="iOS" %}
### RegisterExtension

#### Syntax

```text
+ (void) registerExtension
```

#### Example

This method should be called in the  `didFinishLaunchingWithOptions` delegate method of the `AppDelegate`.

```text
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

Returns the current version of the `ACPPlacesMonitor` extension.

{% tabs %}
{% tab title="iOS" %}
### ExtensionVersion

#### Syntax

```text
+(nonnull NSString*) extensionVersion;
```

#### Example

```text
[ACPPlacesMonitor extensionVersion];
```
{% endtab %}
{% endtabs %}

## Start monitoring

This API starts tracking the device's location and monitors their nearby Places.

**Important**: To begin monitoring, the location service must have the necessary authorization.

- If the authorization for the location service has not been provided to the application, the first call to the `start` API requests the authorization to use the location service as configured for the application.

- Depending on your device's capabilities, if the authorization has been provided, the Places Monitor tracks the user's location based on the currently set `ACPPlacesMonitorMode`.

  By default, the monitor uses `ACPPlacesMonitorModeSignificantChanges`.

{% tabs %}
{% tab title="iOS" %}

### Start

#### Syntax

```text
+ (void) start;
```

#### Example

```text
[ACPPlacesMonitor start];
```

{% endtab %}
{% endtabs %}

## Monitoring Mode

Monitoring can be set to one of the following values:

* **ACPPlacesMonitorModeContinuous**

  The monitoring extension receives and processes locations more frequently. This monitoring strategy consumes a lot of power but provides higher accuracy. For more information, see [Apple documentation on continuous monitoring](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423750-startupdatinglocation).

* **ACPPlacesMonitorModeSignificantChanges**

  The monitoring extension only receives and processes location updates after the device has moved a significant distance from the previously processed location. This monitoring strategy consumes less power than the continuous monitoring strategy. For more information, see [Apple documentation on significant monitoring](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423531-startmonitoringsignificantlocati)

{% tabs %}
{% tab title="iOS" %}
### SetPlacesMonitorMode

#### Syntax

```objective-c
+ (void) setPlacesMonitorMode: (ACPPlacesMonitorMode) monitorMode;
```

#### Example

```objective-c
[ACPPlacesMonitor setPlacesMonitorMode:ACPPlacesMonitorModeSignificantChanges];
```
{% endtab %}
{% endtabs %}

## Stop Monitoring

Stops tracking the significant, or continuous, monitoring of the device's location. When you call this method, geofence and beacon monitoring is also stopped. To start location and geofence monitoring again, call the `startWithContinuousMonitoring` method.

{% tabs %}
{% tab title="iOS" %}
### Stop

#### Syntax

```text
+(void) stop;
```

#### Example

```text
[ACPPlacesMonitor stop];
```
{% endtab %}
{% endtabs %}

## Update Location

Use this API for an immediate update on the device's location. When you call this API, the device attempts to determine the location with the level of accuracy that you specified. This process also refreshes the nearby POIs that are monitored by the extension.

{% tabs %}
{% tab title="iOS" %}
### UpdateLocationNow

#### Syntax

```text
+(void) updateLocationNow;
```

#### Example

```text
[ACPPlacesMonitor updateLocationNow];
```
{% endtab %}
{% endtabs %}

