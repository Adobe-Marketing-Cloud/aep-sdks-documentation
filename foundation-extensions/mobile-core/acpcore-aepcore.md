# Migrating to AEPCore reference

This document is a reference comparison of ACPCore \(2.x\) APIs against their equivalent APIs in AEPCore \(3.x\).

## Primary Classes

| Type | AEP 3.x \(Swift\) | AEP 3.x \(Objective-C\) | ACP 2.x \(Objective-C\) |
| :--- | :--- | :--- | :--- |
| Primary Class | MobileCore | AEPMobileCore | ACPCore |
| Enum | LogLevel | AEPLogLevel | ACPMobileLogLevel |

## Core extension APIs

### trackAction

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

{% hint style="info" %}
For additional details see also [Mobile Core API reference](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/mobile-core-api-reference).
{% endhint %}

