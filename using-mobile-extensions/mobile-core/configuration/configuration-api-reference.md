# Configuration API reference

## configureWithAppID

This API causes the SDK to download the configuration for the provided app ID and apply the configuration to the current session.

{% tabs %}
{% tab title="Android" %}
This API causes the SDK to download the configuration for the provided app ID and apply the configuration to the current session.

#### Syntax

```java
public static void configureWithAppID(final String appId);
```

#### Example

```java
MobileCore.ConfigureWithAppId("1423ae38-8385-8963-8693-28375403491d");
```
{% endtab %}

{% tab title="iOS" %}
#### Syntax

```objectivec
+ (void) configureWithAppId: (NSString* __nullable) appid;
```

#### Example

**Objective-C**

```objectivec
[ACPCore configureWithAppId:@"1423ae38-8385-8963-8693-28375403491d"];
```

**Swift**

```swift
ACPCore.configure(withAppId: "1423ae38-8385-8963-8693-28375403491d")
```
{% endtab %}
{% endtabs %}

## updateConfiguration

You can also update the configuration programmatically by passing configuration keys and values to override the existing configuration.

{% hint style="info" %}
Keys that are not found on the current configuration are added when this method is followed. Null values are allowed and replace existing configuration values.
{% endhint %}

{% hint style="warning" %}
Do not use this API to update the build.environment or any key with an environment prefix, because it can lead to unexpected behaviors. For more information, read [Environment-aware configuration properties](./#environment-aware-configuration-properties).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

### updateConfiguration <a id="updateConfiguration"></a>

#### Syntax

```java
public static void updateConfiguration(final Map configMap);
```

#### Example

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

**Objective-C**

```objectivec
NSDictionary *updatedConfig = @{@"global.privacy":@"optedout"};
[ACPCore updateConfiguration:updatedConfig];
```

**Swift**

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
{% endtabs %}
