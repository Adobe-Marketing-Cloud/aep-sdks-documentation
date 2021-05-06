# Configuration API reference

## configureWithAppID

This API causes the SDK to download the configuration for the provided app ID and apply the configuration to the current session.

{% tabs %}
{% tab title="Android" %}
#### Syntax

```java
public static void configureWithAppID(final String appId);
```

#### Example

#### Java

```java
MobileCore.configureWithAppId("1423ae38-8385-8963-8693-28375403491d");
```
{% endtab %}

{% tab title="iOS" %}
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
{% tab title="Android" %}
### updateConfiguration <a id="updateConfiguration"></a>

#### Syntax

```java
public static void updateConfiguration(final Map configMap);
```

#### Example

#### Java

```java
HashMap<String, Object> data = new HashMap<String, Object>();
data.put("global.privacy", "optedout");
MobileCore.updateConfiguration(data);
```
{% endtab %}

{% tab title="iOS" %}
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
{% tab title="Android" %}
#### Syntax

```java
public static void configureWithFileInPath(final String filePath);
```

#### Example

#### Java

```java
MobileCore.configureWithFileInPath("absolute/path/to/exampleJSONfile.json");
```
{% endtab %}

{% tab title="iOS" %}
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

## configureWithFileInAssets \(Android Only\)

You can bundle a JSON configuration file in the app's Assets folder to replace or complement the configuration that was downloaded by using the [Configure with Launch App ID](./#configure-with-launch-app-id) approach.

{% hint style="info" %}
Method `configureWithFileInAssets` was added in Android Core version 1.7.0.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Syntax

```java
public static void configureWithFileInAssets(final String fileName);
```

#### Example

#### Java

```java
MobileCore.configureWithFileInAssets("exampleJSONfile.json");
```
{% endtab %}
{% endtabs %}

