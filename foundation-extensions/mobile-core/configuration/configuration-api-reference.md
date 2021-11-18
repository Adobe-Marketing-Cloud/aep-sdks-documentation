# Configuration API reference

## Version of the Configuration extension

The `extensionVersion()` API returns the version of the Configuration extension.

To get the version of the Configuration extension, use the following code sample:

{% tabs %}

{% tab title="iOS \(ACP 2.x\)" %}
**Objective C**

```objectivec
NSString *coreExtensionVersion = [ACPCore extensionVersion];
```

**Swift**

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

## configureWithAppID

This API causes the SDK to download the configuration for the provided app ID and apply the configuration to the current session.

{% tabs %}

{% tab title="iOS \(ACP 2.x\)" %}
#### Syntax

```objectivec
+ (void) configureWithAppId: (NSString* __nullable) appid;
```

#### Example

#### Objective-C

```objectivec
[ACPCore configureWithAppId:@"1423ae38-8385-8963-8693-28375403491d"];
```

#### Swift

```swift
ACPCore.configure(withAppId: "1423ae38-8385-8963-8693-28375403491d")
```
{% endtab %}

{% tab title="Unity" %}
#### Syntax

```csharp
public static void ConfigureWithAppID(string appId)
```

#### Example

#### C\#

```csharp
ACPCore.ConfigureWithAppID("1423ae38-8385-8963-8693-28375403491d");
```
{% endtab %}

{% tab title="Xamarin" %}
#### Android Syntax

```csharp
public unsafe static void ConfigureWithAppID (string appId);
```

#### iOS Syntax

```csharp
public static void ConfigureWithAppID (string appid);
```

#### Example

#### C\#

```text
ACPCore.ConfigureWithAppID("1423ae38-8385-8963-8693-28375403491d");
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
{% tab title="iOS \(ACP 2.x\)" %}

### updateConfiguration

#### Syntax

```objectivec
+ (void) updateConfiguration: (NSDictionary* __nullable) config;
```

#### Example

#### Objective-C

```objectivec
NSDictionary *updatedConfig = @{@"global.privacy":@"optedout"};
[ACPCore updateConfiguration:updatedConfig];
```

#### Swift

```swift
let updatedConfig = ["global.privacy":"optedout"]
ACPCore.updateConfiguration(updatedConfig)
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### updateConfiguration

```jsx
ACPCore.updateConfiguration({"global.privacy":"optedout"});
```
{% endtab %}

{% tab title="Flutter" %}
#### Dart

### updateConfiguration

```dart
FlutterACPCore.updateConfiguration({"global.privacy":"optedout"});
```
{% endtab %}

{% tab title="Cordova" %}
## Javascript

Update SDK configuration

```javascript
ACPCore.updateConfiguration({"newConfigKey":"newConfigValue"}, successCallback, errorCallback);
```
{% endtab %}

{% tab title="Unity" %}
## C\#

Update SDK configuration

```csharp
var dict = new Dictionary<string, object>();
dict.Add("newConfigKey", "newConfigValue");
ACPCore.UpdateConfiguration(dict);
```
{% endtab %}

{% tab title="Xamarin" %}
## C\#

Update SDK configuration

**iOS**

```csharp
 var config = new NSMutableDictionary<NSString, NSObject>
 {
   ["newConfigKey"] = new NSString("newConfigValue")
 };
ACPCore.UpdateConfiguration(config);
```

**Android**

```csharp
var config = new Dictionary<string, Java.Lang.Object>();
config.Add("newConfigKey", "newConfigValue");
ACPCore.UpdateConfiguration(config);
```
{% endtab %}
{% endtabs %}

## configureWithFileInPath

You can include a bundled JSON configuration file in your app package to replace or complement the configuration that was downloaded by using the [Configure with Launch App ID](./#configure-with-launch-app-id) approach.

To pass in a bundled path and file name:

{% tabs %}

{% tab title="iOS \(ACP 2.x\)" %}
#### Syntax

```objectivec
+ (void) configureWithFileInPath: (NSString* __nullable) filepath;
```

#### Example

**Objective-C**

```objectivec
NSString *filePath = [[NSBundle mainBundle] pathForResource:@"ExampleJSONFile"ofType:@"json"];
[ACPCore configureWithFileInPath:filePath];
```

**Swift**

```swift
let filePath = Bundle.main.path(forResource: "ExampleJSONFile", ofType: "json")
ACPCore.configureWithFile(inPath: filePath)
```
{% endtab %}

{% tab title="Xamarin" %}
#### Android Syntax

```csharp
public unsafe static void ConfigureWithFileInPath (string filepath);
```

#### iOS Syntax

```csharp
public static void ConfigureWithFileInPath (string filepath);
```

#### Example

#### C\#

```csharp
ACPCore.ConfigureWithFileInPath("absolute/path/to/exampleJSONfile.json");
```
{% endtab %}
{% endtabs %}

