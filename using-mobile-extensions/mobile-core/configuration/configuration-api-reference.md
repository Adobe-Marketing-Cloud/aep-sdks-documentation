# Configuration API reference

## Configure with the Launch App ID

Launch generates a unique environment ID that the SDK uses to retrieve your configuration. This ID is generated when an app configuration is created and published to a given environment. The app is first launched and then the SDK retrieves and uses this Adobe-hosted configuration.

{% hint style="success" %}
We strongly recommend that you configure the SDK with the Launch environment ID.
{% endhint %}

After the configuration is retrieved when the app is initially launched, the configuration is stored in local cache. Subsequent requests for configuration causes the continued use of the cached configuration, unless configuration changes. If a network error occurs while downloading the configuration file, the local cache is used.

No configuration changes are made when the following conditions are met:

* No change from cached configuration.
* Configuration retrieval fails due to network, or other, considerations.
* A file-read or parsing errors occurs.

The unique environment ID provided by Launch can be configured with the SDK using the following:

{% tabs %}
{% tab title="Android" %}
### configureWithAppID

Causes the SDK to download the configuration for the provided app ID and apply the configuration to the current session.

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
### configureWithAppID

Causes the SDK to download the configuration for the provided App ID and apply it to the current session.

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

{% hint style="info" %}
Alternatively, you may also place the Launch environment ID in your iOS project's _Info.plist_ with the `ADBMobileAppID` key. When the SDK is initialized, the environment ID is automatically read from the _Info.plist_ file, and associated configuration
{% endhint %}
{% endtab %}
{% endtabs %}

## Programmatic updates to configuration

You can also update the configuration programmatically by passing configuration keys and values to override existing configuration.

{% hint style="info" %}
Keys that are not found on the current configuration are added when this method is followed. Null values are allowed and replace existing configuration values.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### updateConfiguration

#### Syntax

```java
public static void updateConfiguration(final Map configMap);
```

#### Example

```java
HashMap<String, Object> data = new HashMap<String, Object>();
data.put("global.ssl", true);
MobileCore.updateConfiguration(data);
```
{% endtab %}

{% tab title="iOS" %}
### updateConfiguration

{% hint style="success" %}
Starting in ACPCore 2.0.3 for iOS, any key provided via **updateConfiguration** should not have a prefix. The configuration extension might modify the key provided to be correct for the corresponding `build.environment` in which the app is running. For more information, see [Environment-aware Configuration Properties](./#environment-aware-configuration-properties).
{% endhint %}

#### Syntax

```objectivec
+ (void) updateConfiguration: (NSDictionary* __nullable) config;
```

#### Example

**Objective-C**

```objectivec
NSDictionary *updatedConfig = @{@"global.ssl":@YES};
[ACPCore updateConfiguration:updatedConfig];
```

**Swift**

```swift
let updatedConfig = ["global.ssl":true]
ACPCore.updateConfiguration(updatedConfig)
```
{% endtab %}
{% endtabs %}

## Using a bundled file configuration

You can include a bundled JSON configuration file in your app package to replace or complement the configuration that was downloaded by using the [Configure with Launch App ID](./#configure-with-launch-app-id) approach.

To download the JSON configuration file, use the following URL:

`https://assets.adobedtm.com/PASTE-LAUNCH-ENVIRONMENT-ID.json`

* In iOS, the `ADBMobileConfig.json` file can be placed anywhere that it is accessible in your bundle.
* In Android, the `ADBMobileConfig.json` file must be placed in the assets folder.

You can also load a different `ADBMobileConfig.json` file by using the `ConfigureWithFileInPath` method. The Adobe Experience Platform SDKs will attempt to load the file from the given path and parse its JSON contents. Previous programmatic configuration changes that were set by using the `UpdateConfiguration` method are applied on the bundled file's configuration before setting the new configuration to the Adobe Cloud Platform SDKs. If a file-read error or JSON parsing error occurs, no configuration changes are made.

To pass in a bundled path and file name:

{% tabs %}
{% tab title="Android" %}
### configureWithFileInPath

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
### configureWithFileInPath

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

