# Migrating to AEPCore reference

This document is a reference comparison of ACPCore \(2.x\) APIs against their equivalent APIs in AEPCore \(3.x\).

## Primary Classes

| Type | AEP 3.x \(Swift\) | AEP 3.x \(Objective-C\) | ACP 2.x \(Objective-C\) |
| :--- | :--- | :--- | :--- |
| Primary Class | MobileCore | AEPMobileCore | ACPCore |
| Enum | LogLevel | AEPLogLevel | ACPMobileLogLevel |

## Core extension APIs

### trackAction

Actions are events that occur in your application. You can use the `trackAction` method to track and measure an action. Each action has one or more corresponding metrics that are incremented each time the event occurs. For example, you can use an action to track new subscriptions, every time an article is viewed, or every time a level is completed.

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func track(action: String?, data: [String: Any]?)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void)trackAction:(NSString * _Nullable)action data:(NSDictionary<NSString *, id> * _Nullable)data;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) contextData;
```
{% endtab %}
{% endtabs %}

### trackState

States represent screens or views in your application. The `trackState` method needs to be called every time a new state is displayed in your application. For example, this method should be called when a user navigates from the home page to the news feed. This method sends an Adobe Analytics state tracking hit with optional context data.

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func track(state: String?, data: [String: Any]?)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void)trackState:(NSString * _Nullable)state data:(NSDictionary<NSString *, id> * _Nullable)data;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) contextData;
```
{% endtab %}
{% endtabs %}

### collectPii

The `collectPii` method lets the SDK to collect sensitive or personally identifiable information \(PII\).

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
public static func collectPii(_ data: [String: Any])
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void)collectPii:(NSDictionary<NSString *, id> * _Nonnull)data;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) collectPii: (nonnull NSDictionary<NSString*, NSString*>*) data;
```
{% endtab %}
{% endtabs %}

### collectLaunchInfo

You can provide the user information to the SDK from various launch points in your application.

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
public static func collectLaunchInfo(_ userInfo: [String: Any])
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void)collectLaunchInfo:(NSDictionary<NSString *, id> * _Nonnull)userInfo;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```
{% endtab %}
{% endtabs %}

### getSdkIdentities

The following SDK identities, as applicable, are locally stored:

* Company Context - IMS Org IDs
* Experience Cloud ID \(MID\)
* User IDs
* Integration codes \(ADID, push IDs\)
* Data source IDs \(DPID, DPUUID\)
* Analytics IDs \(AVID, AID, VID, and associated RSIDs\)
* Target legacy IDs \(TNTID, TNT3rdpartyID\)
* Audience Manager ID \(UUID\)

To retrieve data as a JSON string from the SDKs and send this data to your servers, use the `getSdkIdentities` method.

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func getSdkIdentities(completion: @escaping (String?, Error?) -> Void)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void)getSdkIdentities:(void (^ _Nonnull)(NSString * _Nullable, NSError * _Nullable))completion;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) getSdkIdentities: (nullable void (^) (NSString* __nullable content)) callback;
+ (void) getSdkIdentitiesWithCompletionHandler: (nullable void (^) (NSString* __nullable content, NSError* _Nullable error)) completionHandler;
```
{% endtab %}
{% endtabs %}

### setLogLevel

The logging APIs allow log messages to be tagged and filtered with the Mobile SDK log messages. This allows application developers to filter the logged messages based on the current logging mode.

Application developers can use the `setLogLevel` method to filter the log messages that are coming from the Mobile SDK.

From least to most verbose, the order of Mobile SDK logging modes is as follows:

* ERROR
* WARNING
* DEBUG
* VERBOSE / TRACE

When debugging on iOS, you can use `LogLevel.verbose` to enable all the logging messages that are coming from Mobile SDK and partner extensions. Similarly, on Android, you can use `LoggingMode.VERBOSE` to enable all the logging messages that are coming from Mobile SDK and partner extensions.

In a production application, you should use a less verbose logging mode, such as error-level logging.

By default, Mobile SDK logging mode is set to `LoggingMode.ERROR` for Android and `LogLevel.error`on iOS.

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
public static func setLogLevel(_ level: LogLevel)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void)setLogLevel:(enum AEPLogLevel)level;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) setLogLevel: (ACPMobileLogLevel) logLevel;
```
{% endtab %}
{% endtabs %}

### registerURLHandler

Mobile SDK allows you to add a callback function that is triggered before the [`open url`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#consequence-types) action occurs. If the callback function returns **Yes**, the SDK does not complete the `open url` action. If the callback function returns **No**, the SDK completes the `open url` action.

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
  // Not supported
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
  // Not supported
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) registerURLHandler: (nonnull BOOL (^) (NSString* __nullable url)) callback;
```
{% endtab %}
{% endtabs %}

### setAppGroup

You can use the `setAppGroup` method to set the app group, which is used to share user defaults and files among the containing app and the extension apps.

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
public static func setAppGroup(_ group: String?)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void)setAppGroup:(NSString * _Nullable)group;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) setAppGroup: (nullable NSString*) appGroup;
```
{% endtab %}
{% endtabs %}

### configureWithAppId

This API causes the SDK to download the configuration for the provided app ID and apply the configuration to the current session.

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func configureWith(appId: String)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void)configureWithAppId:(NSString * _Nonnull)appId;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) configureWithAppId: (NSString* __nullable) appid;
```
{% endtab %}
{% endtabs %}

### updateConfiguration

You can also update the configuration programmatically by passing configuration keys and values to override the existing configuration.

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func updateConfigurationWith(configDict: [String: Any])
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void)updateConfiguration:(NSDictionary<NSString *, id> * _Nonnull)configDict;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) updateConfiguration: (NSDictionary* __nullable) config;
```
{% endtab %}
{% endtabs %}

### configureWithFileInPath

You can include a bundled JSON configuration file in your app package to replace or complement the configuration that was downloaded by using the [Configure with Launch App ID](./#configure-with-launch-app-id) approach.

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func configureWith(filePath: String)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void)configureWithFilePath:(NSString * _Nonnull)filePath;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) configureWithFileInPath: (NSString* __nullable) filepath;
```
{% endtab %}
{% endtabs %}

### extensionVersion

The `extensionVersion()` API returns the version of the Configuration extension.

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
public static var extensionVersion: String
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (nonnull NSString*) extensionVersion;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (nonnull NSString*) extensionVersion;
```
{% endtab %}
{% endtabs %}

