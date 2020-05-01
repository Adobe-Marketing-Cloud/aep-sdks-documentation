# Configuration

The Configuration extension is built into the Mobile Core extension. It provides several different APIs for you to setup the configuration either remotely on Experience Platform Launch or locally.

## Configure with the Experience Platform Launch App ID

Experience Platform Launch generates a unique environment ID that the SDK uses to retrieve your configuration. This ID is generated when an app configuration is created and published to a given environment. The app is first launched and then the SDK retrieves and uses this Adobe-hosted configuration.

{% hint style="success" %}
We strongly recommend that you configure the SDK with the Experience Platform Launch environment ID. Follow the steps in [Set up a mobile property](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/50f1aec2d1ab7760583a7ba8dcd97f3c265309f6/getting-started/create-a-mobile-property/README.md) if you need to create a new Experience Platform Launch App.
{% endhint %}

After the configuration is retrieved when the app is initially launched, the configuration is stored in local cache. The SDK tries to refresh the configuration every cold launch or when a new session is detected. If there is no change or a network request error occurs while downloading the configuration file, the cached configuration will be used.

The unique environment ID provided by Experience Platform Launch can be configured with the SDK using the following:

{% tabs %}
{% tab title="Android" %}
#### Java

```java
MobileCore.ConfigureWithAppId("1423ae38-8385-8963-8693-28375403491d");
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

```objectivec
[ACPCore configureWithAppId:@"1423ae38-8385-8963-8693-28375403491d"];
```

#### Swift

```swift
ACPCore.configure(withAppId: "1423ae38-8385-8963-8693-28375403491d")
```

{% hint style="info" %}
Alternatively, you can also place the Launch environment ID in your iOS project's _Info.plist_ with the `ADBMobileAppID` key. When the SDK is initialized, the environment ID is automatically read from the _Info.plist_ file and the associated configuration.
{% endhint %}
{% endtab %}

{% tab title="Cordova" %}
#### Cordova

When using Cordova, the `configureWithAppId` method call must be done in native code which is shown under the Android and iOS tabs.
{% endtab %}
{% endtabs %}

## Programmatic updates to configuration

You can also update the configuration programmatically by passing configuration keys and values to override the existing configuration.

{% hint style="info" %}
Keys that are not found on the current configuration are added when this method is followed. Null values are allowed and replace existing configuration values.
{% endhint %}

{% hint style="warning" %}
Do not use this API to update the build.environment or any key with an environment prefix, because it can lead to unexpected behavior. For more information, read [Environment-aware configuration properties](./#environment-aware-configuration-properties).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

```java
HashMap<String, Object> data = new HashMap<String, Object>();
data.put("global.privacy", "optedout");
MobileCore.updateConfiguration(data);
```
{% endtab %}

{% tab title="iOS" %}
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

```jsx
ACPCore.updateConfiguration({"global.privacy":"optedout"});
```
{% endtab %}

{% tab title="Flutter" %}
#### Dart

```dart
FlutterACPCore.updateConfiguration({"global.privacy":"optedout"});
```
{% endtab %}

{% tab title="Cordova" %}
#### Cordova

```jsx
ACPCore.updateConfiguration({"global.privacy":"optedout"}, function(handleCallback) {
  console.log("AdobeExperenceSDK: Update configuration successful: " + handleCallback);
}, function(handleError) {
  console.log("AdobeExperenceSDK: Failed to update configuration : " + handleError);
});
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
#### Java

```java
// Case 1: to use ADBMobileConfig.json in the assets folder
// No code is needed

// Case 2: to use a config json from a different path:
MobileCore.configureWithFileInPath("absolute/path/to/exampleJSONfile.json");
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

```objectivec
NSString *filePath = [[NSBundle mainBundle] pathForResource:@"ExampleJSONFile"ofType:@"json"];
[ACPCore configureWithFileInPath:filePath];
```

#### Swift

```swift
let filePath = Bundle.main.path(forResource: "ExampleJSONFile", ofType: "json")
ACPCore.configureWithFile(inPath: filePath)
```
{% endtab %}
{% endtabs %}

## Environment-aware configuration properties

{% hint style="info" %}
This feature is only available in iOS ACPCore version 2.0.3 or later.
{% endhint %}

Some extension developers might use different configuration values based on their environment, and the generated configuration might have several entries for the same property. For example, the Adobe Campaign Standard extension has different endpoints for development, staging, and production servers. Here is an example of a raw configuration that supports multiple build environments:

#### JavaScript

```javascript
{
  "myExtension.server": "mydomain.com",
  "__dev__myExtension.server": "mydomain.dev.com",
  "__stage__myExtension.server": "mydomain.stage.com"
}
```

{% hint style="success" %}
Each time a remote configuration is generated by Experience Platform Launch, a `build.environment` value is set. This value is based on the environment that you are publishing. When the remote configuration is downloaded, the Configuration extension considers the value in `build.environment` and provides **only** the non-prefixed version for the current environment in the shared state.
{% endhint %}

Here is a modification of the previous example, which now includes `build.environment`:

```javascript
{
  "build.environment": "dev",
  "myExtension.server": "mydomain.com",
  "__dev__myExtension.server": "mydomain.dev.com",
  "__stage__myExtension.server": "mydomain.stage.com"
}
```

Here is the resulting shared state from the Configuration extension:

```javascript
{
  "build.environment": "dev",
  "myExtension.server": "mydomain.dev.com"  
}
```

### Sample configuration

Here's a sample JSON file for the SDK:

```javascript
{
    "experienceCloud.org": "3CE342C75100435B0A490D4C@AdobeOrg",  
    "target.clientCode": "yourclientcode",  
    "target.timeout": 5,  
    "audience.server": "omniture.demdex.net",  
    "audience.timeout": 5,  
    "analytics.rsids": "mobilersidsample",  
    "analytics.server": "obumobile1.sc.omtrdc.net",  
    "analytics.aamForwardingEnabled": false,  
    "analytics.offlineEnabled": true,  
    "analytics.batchLimit": 0,  
    "analytics.backdatePreviousSessionInfo": false,
    "global.privacy": "optedin",  
    "lifecycle.sessionTimeout": 300,  
    "rules.url": "https://link.to.rules/test.zip"
}
```

