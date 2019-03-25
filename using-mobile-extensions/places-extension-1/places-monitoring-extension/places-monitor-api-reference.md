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

This API tracks the device's location and monitors the POIs that are near by. You can use this method to start monitoring the user's GPS location. Location monitoring can be done in one of the following ways:

* **Continuous**

  The monitoring extension receives and processes locations more frequently. This monitoring strategy consumes a lot of power but provides higher accuracy. You can enable continuous monitoring by passing `YES` to the `continuousMonitoring` parameter. For more information, see [Apple documentation on continuous monitoring](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423750-startupdatinglocation).

* **Significant**

  The monitoring extension only receives and processes location updates after the device has moved a significant distance from the previously processed location. This monitoring strategy consumes less power than the continuous monitoring strategy. You can enable significant monitoring by passing `NO` to the `continuousMonitoring` parameter. For more information, see [Apple documentation on significant monitoring](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423531-startmonitoringsignificantlocati)

{% tabs %}
{% tab title="iOS" %}
### StartWithContinuousMonitoring

#### Syntax

```text
+(void) startWithContinuousMonitoring:(BOOL)continuousMonitoring;
```

#### Example

```text
[ACPPlacesMonitor startWithContinuousMonitoring:YES];
```
{% endtab %}
{% endtabs %}

**Tip**: If the authorization for the location service has not been provided for the application, the first call to the `StartWithContinuousMonitoring` API requests the authorization to use the location service as configured for the application.

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

