# Configuration API reference

## Configure with the Experience Platform Launch App ID

Experience Platform Launch generates a unique environment ID that the SDK uses to retrieve your configuration. This ID is generated when an app configuration is created and published to a given environment. The app is first launched and then the SDK retrieves and uses this Adobe-hosted configuration.

{% hint style="success" %}
We strongly recommend that you configure the SDK with the Experience Platform Launch environment ID.
{% endhint %}

After the configuration is retrieved when the app is initially launched, the configuration is stored in local cache. Subsequent requests for configuration causes the continued use of the cached configuration, unless configuration changes. If a network error occurs while downloading the configuration file, the local cache is used.

No configuration changes are made when the following conditions are met:

* No change from cached configuration.
* Configuration retrieval fails due to network, or other, considerations.
* A file-read or parsing errors occurs.

The unique environment ID provided by Experience Platform Launch can be configured with the SDK using the following:

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

{% tab title="React Native" %}
#### JavaScript

### configureWithAppID

Configure the SDK by downloading the remote configuration file hosted on Adobe servers specified by the given application ID. The configuration file is cached once downloaded and used in subsequent calls to this API. If the remote file is updated after the first download, the updated file is downloaded and replaces the cached file.

The appid is preserved, and on application restarts, the remote configuration file specified by appid is downloaded and applied to the SDK.

On failure to download the remote configuration file, the SDK is configured using the cached file if it exists, or if no cache file exists then the existing configuration remains unchanged.

Calls to this API will replace any existing SDK configuration except those set using `ACPCore.updateConfiguration` or `ACPCore.setPrivacyStatus`. Configuration updates made using `ACPCore.updateConfiguration` and `ACPCore.setPrivacyStatus` bare always applied on top of configuration changes made using this API.

`@param {String?} appId` a unique identifier assigned to the app instance by the Adobe Mobile Services. It is automatically added to the ADBMobile JSON file when downloaded from the Adobe Mobile Services UI and can be found in Manage App Settings. A value of `nil` has no effect.

```jsx
import {ACPCore} from '@adobe/react-native-acpcore';

initSDK() { 
    ACPCore.configureWithAppId("yourAppId");
    ACPCore.start();
}
```
{% endtab %}
{% endtabs %}

## Programmatic updates to configuration

You can also update the configuration programmatically by passing configuration keys and values to override existing configuration.

{% hint style="info" %}
Keys that are not found on the current configuration are added when this method is followed. Null values are allowed and replace existing configuration values.
{% endhint %}

{% hint style="warning" %}
Do not use this API to update build.environment or any key with environment prefix, because it can lead to unexpected behaviors. For more information, read [Environment-aware configuration properties](../configuration#environment-aware-configuration-properties).
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

{% tab title="React Native" %}
#### JavaScript

### updateConfiguration

```jsx
ACPCore.updateConfiguration({"yourConfigKey": "yourConfigValue"});
```
{% endtab %}
{% endtabs %}

## Using a bundled file configuration

You can include a bundled JSON configuration file in your app package to replace or complement the configuration that was downloaded by using the [Configure with Launch App ID](./#configure-with-launch-app-id) approach.

To download the JSON configuration file, use the following URL:

`https://assets.adobedtm.com/PASTE-LAUNCH-ENVIRONMENT-ID.json`

* In iOS, the `ADBMobileConfig.json` file can be placed anywhere that it is accessible in your bundle.
* In Android, the `ADBMobileConfig.json` file must be placed in the assets folder.

You can also load a different `ADBMobileConfig.json` file by using the `ConfigureWithFileInPath` method. The Adobe Experience Platform SDKs will attempt to load the file from the given path and parse its JSON contents. Previous programmatic configuration changes that were set by using the `UpdateConfiguration` method are applied on the bundled file's configuration before setting the new configuration to the Adobe Experience Platform SDKs. If a file-read error or JSON parsing error occurs, no configuration changes are made.

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

{% tab title="React Native" %}
#### JavaScript

### configureWithFileInPath

```jsx
 configureWithFileInPath(filepath?: String) {
   ACPCore.configureWithFileInPath(filepath);
  },
```
{% endtab %}
{% endtabs %}

