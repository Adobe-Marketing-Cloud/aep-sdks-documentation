# Configuration API reference

## clearUpdatedConfiguration

{% hint style="info" %}
This API is only available in Android and iOS (AEP 3.x).
{% endhint %}

You can clear any programmatic updates made to the configuration via the `clearUpdatedConfiguration` API. This will clear programmatic updates to configuration made via the `updateConfiguration(configMap)`(Android)/ `updateConfigurationWith(configDict:)`(iOS) API. It will also clear any updates to the `MobilePrivacyStatus`(Android)/ `PrivacyStatus`(iOS)  made via `setPrivacyStatus(privacyStatus)`(Android)/ `setPrivacyStatus(_ status:)`(iOS).

 Here are some examples of scenarios:

* `configureWithAppId(appId)`(Android)/`configureWith(appId:)`(iOS) -> `updateConfiguration(configMap)`(Android)/ `updateConfigurationWith(configDict:)`(iOS) -> `clearUpdatedConfiguration()`: In this example, you end up with the initial configuration set via `configureWithAppId(appId)`(Android)/ `configureWith(appId:)`(iOS)

* `configureWithFileInPath(filePath)`(Android)/ `configureWith(filePath:)`(iOS) -> `updateConfiguration(configMap)`(Android)/ `updateConfigurationWith(configDict)`(iOS) -> `clearUpdatedConfiguration()`: In this example, you end up with the initial configuration set via `configureWithFileInPath(filePath)`(Android)/ `configureWith(filePath:)`(iOS)

* `configureWithFileInAssets(fileName)`(Android) -> `updateConfiguration(configMap)`(Android) -> `clearUpdatedConfiguration()`: In this example, you end up with the initial configuration set via `configureWithFileInAssets(fileName)`(Android)

* `configureWithAppId(appId)`(Android)/`configureWith(appId:)`(iOS) or `configureWithFileInPath(filePath)`(Android)/ `configureWith(filePath:)`(iOS) or `configureWithFileInAssets(fileName)`(Android) -> `updateConfiguration(configMap)`(Android)/ `updateConfigurationWith(configDict)`(iOS) -> `clearUpdatedConfiguration()` -> `updateConfiguration(configMap)`(Android)/ `updateConfigurationWith(configDict)`(iOS): In this example, the configuration will be the most recently updated configuration and will not have any keys from the first update unless they are included in the most recent update.

* `configureWithAppId(appId)`(Android)/`configureWith(appId:)`(iOS) or `configureWithFileInPath(filePath)`(Android)/ `configureWith(filePath:)`(iOS) or `configureWithFileInAssets(fileName)`(Android) -> `setPrivacyStatus(privacyStatus)`(Android)/ `setPrivacyStatus(_ status:)`(iOS) -> `clearUpdatedConfiguration()`: In this example, the configuration will have the initial `MobilePrivacyStatus`(Android)/ `PrivacyStatus`(iOS) set via `configureWithAppId(appId)`(Android)/`configureWith(appId:)`(iOS) or `configureWithFileInPath(filePath)`(Android)/ `configureWith(filePath:)`(iOS) or `configureWithFileInAssets(fileName)`(Android).

{% tabs %}
{% tab title="Android" %}

### Java

**Syntax**

```java
public static void clearUpdatedConfiguration();
```

**Example**

```java
MobileCore.clearUpdatedConfiguration();
```

{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### Swift

**Syntax**

```swift
static func clearUpdatedConfiguration()
```

**Example**

```swift
MobileCore.clearUpdatedConfiguration()
```

### Objective-C

**Syntax**

```objectivec
+ (void) clearUpdatedConfiguration(); 
```

**Example**

```objectivec
[AEPMobileCore clearUpdatedConfiguration];
```

{% endtab %}
{% endtabs %}

## configureWithAppID

This API causes the SDK to download the configuration for the provided app ID and apply the configuration to the current session.

{% tabs %}
{% tab title="Android" %}
### Java

**Syntax**

```java
public static void configureWithAppID(final String appId);
```

**Example**

```java
MobileCore.configureWithAppId("1423ae38-8385-8963-8693-28375403491d");
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}

### Swift

**Syntax**

```swift
 static func configureWith(appId: String)
```

**Example**

```swift
 MobileCore.configureWith(appId: "1423ae38-8385-8963-8693-28375403491d")
```

### Objective-C

**Syntax**

```objectivec
+ (void) configureWithAppId: (NSString* appId);
```

**Example**

```objectivec
 [AEPMobileCore configureWithAppId: @"1423ae38-8385-8963-8693-28375403491d"];
```

{% endtab %}

{% tab title="iOS \(ACP 2.x\)" %}

### Swift

**Syntax**

```swift
static func configure(withAppId: String)
```

**Example**

```swift
ACPCore.configure(withAppId: "1423ae38-8385-8963-8693-28375403491d")
```

### Objective-C

**Syntax**

```objectivec
+ (void) configureWithAppId: (NSString* __nullable) appid;
```

**Example**

```objectivec
[ACPCore configureWithAppId:@"1423ae38-8385-8963-8693-28375403491d"];
```

{% endtab %}

{% tab title="Unity" %}

### C\#

**Syntax**

```csharp
public static void ConfigureWithAppID(string appId)
```

**Example**

```csharp
ACPCore.ConfigureWithAppID("1423ae38-8385-8963-8693-28375403491d");
```
{% endtab %}

{% tab title="Xamarin" %}

### C\#

**Android Syntax**

```csharp
public unsafe static void ConfigureWithAppID (string appId);
```

**iOS Syntax**

```csharp
public static void ConfigureWithAppID (string appid);
```

**Example**

```text
ACPCore.ConfigureWithAppID("1423ae38-8385-8963-8693-28375403491d");
```
{% endtab %}
{% endtabs %}

## configureWithFileInAssets

{% hint style="info" %}
This API is only available in Android and was added in Android was added in Android Core version 1.7.0.
{% endhint %}

You can bundle a JSON configuration file in the app's Assets folder to replace or complement the configuration that was downloaded by using the [Configure with App ID per environment](./#configure-with-app-id-per-environment) approach.


{% tabs %}
{% tab title="Android" %}
### Java

**Syntax**

```java
public static void configureWithFileInAssets(final String fileName);
```

**Example**

```java
MobileCore.configureWithFileInAssets("exampleJSONfile.json");
```
{% endtab %}
{% endtabs %}

## configureWithFileInPath

You can include a bundled JSON configuration file in your app package to replace or complement the configuration that was downloaded by using the [Configure with App ID per environment](./#configure-with-app-id-per-environment) approach.

To pass in a bundled path and file name:

{% tabs %}
{% tab title="Android" %}

### Java

**Syntax**

```java
public static void configureWithFileInPath(final String filePath);
```

**Example**

```java
MobileCore.configureWithFileInPath("absolute/path/to/exampleJSONfile.json");
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}

### Swift

**Syntax**

```swift
 static func configureWith(filePath: String)
```

**Example**

```swift
 let filePath = Bundle.main.path(forResource: "ExampleJSONFile", ofType: "json")
 MobileCore.configureWith(filePath: filePath)
```

### Objective-C

**Syntax**

```objectivec
+ (void) configureWithFileInPath: (NSString* __nullable) filepath;
```

**Example**

```objectivec
 NSString *filePath = [[NSBundle mainBundle] pathForResource:@"ExampleJSONFile" ofType:@"json"];
 [AEPMobileCore configureWithFilePath:filePath];
```

{% endtab %}

{% tab title="iOS \(ACP 2.x\)" %}

### Swift

**Syntax**

```swift
static func configureWithFile(inPath: String)
```

**Example**

```swift
let filePath = Bundle.main.path(forResource: "ExampleJSONFile", ofType: "json")
ACPCore.configureWithFile(inPath: filePath)
```

### Objective-C

**Syntax**

```objectivec
+ (void) configureWithFileInPath: (NSString* __nullable) filepath;
```

**Example**

```objectivec
NSString *filePath = [[NSBundle mainBundle] pathForResource:@"ExampleJSONFile"ofType:@"json"];
[ACPCore configureWithFileInPath:filePath];
```

{% endtab %}

{% tab title="Xamarin" %}

### C\#

**Android Syntax** 

```csharp
public unsafe static void ConfigureWithFileInPath (string filepath);
```

**iOS Syntax**

```csharp
public static void ConfigureWithFileInPath (string filepath);
```

**Example**

```csharp
ACPCore.ConfigureWithFileInPath("absolute/path/to/exampleJSONfile.json");
```
{% endtab %}
{% endtabs %}

## extensionVersion

The `extensionVersion()` API returns the version of the Configuration extension.

To get the version of the Configuration extension, use the following code sample:

{% tabs %}
{% tab title="Android" %}
#### Java

```java
String coreExtensionVersion = MobileCore.extensionVersion();
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
#### Swift

```swift
let version = MobileCore.extensionVersion
```

#### Objective C

```objectivec
NSString *version = [AEPMobileCore extensionVersion];
```
{% endtab %}

{% tab title="iOS \(ACP 2.x\)" %}
#### Objective C

```objectivec
NSString *coreExtensionVersion = [ACPCore extensionVersion];
```

#### Swift

```swift
let coreExtensionVersion  = ACPCore.extensionVersion()
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

```jsx
ACPCore.extensionVersion().then(coreExtensionVersion => console.log("AdobeExperienceSDK: ACPCore version: " + coreExtensionVersion));
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

```dart
String coreExtensionVersion = await FlutterACPCore.extensionVersion;
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

```jsx
ACPCore.extensionVersion(function(version) {  
   console.log("ACPCore version: " + version);
}, function(error) {  
   console.log(error);  
});
```
{% endtab %}

{% tab title="Unity" %}
### C\#

```csharp
string coreExtensionVersion = ACPCore.ExtensionVersion();
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

```csharp
string coreExtensionVersion = ACPCore.ExtensionVersion();
```
{% endtab %}
{% endtabs %}

## updateConfiguration

You can also update the configuration programmatically by passing configuration keys and values to override the existing configuration.

{% hint style="info" %}
Keys that are not found on the current configuration are added when this method is followed. Null values are allowed and replace existing configuration values.
{% endhint %}

{% hint style="warning" %}
Do not use this API to update the `build.environment` key or any key with an environment prefix, because it can lead to unexpected behaviors. For more information, read [Environment-aware configuration properties](./#environment-aware-configuration-properties).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### Java

**Syntax**

```java
public static void updateConfiguration(final Map configMap);
```

**Example**

```java
HashMap<String, Object> data = new HashMap<String, Object>();
data.put("global.privacy", "optedout");
MobileCore.updateConfiguration(data);
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}

### Swift

**Syntax**

```swift
@objc(updateConfiguration:)
static func updateConfigurationWith(configDict: [String: Any])
```

**Example**

```swift
 let updatedConfig = ["global.privacy":"optedout"]
 MobileCore.updateConfigurationWith(configDict: updatedConfig)
```

### Objective-C

**Syntax**

```objectivec
 + (void) updateConfiguration: (NSDictionary* __nullable) config;
```

**Example**

```objectivec
 NSDictionary *updatedConfig = @{@"global.privacy":@"optedout"};
 [AEPMobileCore updateConfiguration:updatedConfig];
```
{% endtab %}

{% tab title="iOS \(ACP 2.x\)" %}

### Swift

**Syntax**

```swift
static func updateConfiguration(_: [String: Any])
```

**Example**

```swift
let updatedConfig = ["global.privacy":"optedout"]
ACPCore.updateConfiguration(updatedConfig)
```

### Objective-C

**Syntax**

```objectivec
+ (void) updateConfiguration: (NSDictionary* __nullable) config;
```

**Example**

```objectivec
NSDictionary *updatedConfig = @{@"global.privacy":@"optedout"};
[ACPCore updateConfiguration:updatedConfig];
```

{% endtab %}

{% tab title="React Native" %}
### JavaScript

**Syntax**

```javascript
updateConfiguration(configMap?: { string: any })
```

**Example**

```jsx
ACPCore.updateConfiguration({"global.privacy":"optedout"});
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

**Syntax**

```dart
static Future<void> updateConfiguration(Map<String, Object> configMap);
```

**Example**

```dart
FlutterACPCore.updateConfiguration({"global.privacy":"optedout"});
```
{% endtab %}

{% tab title="Cordova" %}
### Javascript

```javascript
ACPCore.updateConfiguration({"newConfigKey":"newConfigValue"}, successCallback, errorCallback);
```
{% endtab %}

{% tab title="Unity" %}
### C\#

**Syntax**

```csharp
public static void UpdateConfiguration(Dictionary<string, object> config);
```

**Example**

```csharp
var dict = new Dictionary<string, object>();
dict.Add("newConfigKey", "newConfigValue");
ACPCore.UpdateConfiguration(dict);
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

**Syntax**

```csharp
void UpdateConfiguration([NullAllowed] NSDictionary config);
```

**iOS Example**

```csharp
 var config = new NSMutableDictionary<NSString, NSObject>
 {
   ["newConfigKey"] = new NSString("newConfigValue")
 };
ACPCore.UpdateConfiguration(config);
```

**Android Example**

```csharp
var config = new Dictionary<string, Java.Lang.Object>();
config.Add("newConfigKey", "newConfigValue");
ACPCore.UpdateConfiguration(config);
```
{% endtab %}
{% endtabs %}
