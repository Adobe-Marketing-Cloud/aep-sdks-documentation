# Migration from ACPCore to AEPCore

This document is a reference comparison of ACPCore \(2.x\) APIs against their equivalent APIs in AEPCore \(3.x\).

## Primary `Classes`

The class name containing public APIs is different depending on which SDK and language combination being used.

| SDK version | Language | Class name |
| :--- | :--- | :--- |
| ACPCore | Objective-C | ACPCore |
| AEPCore | Swift | MobileCore |
| AEPCore | Objective-C | AEPMobileCore |

## Additional public `Classes` and `Enums`

| SDK version | Language | Class name |
| :--- | :--- | :--- |
| ACPCore | Objective-C | ACPMobileLogLevel |
| AEPCore | Swift | LogLevel |
| AEPCore | Objective-C | AEPLogLevel |

## Core extension APIs

For more information, please read the [Mobile Core API reference](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/mobile-core-api-reference).

* [trackAction](acpcore-aepcore.md#trackAction)
* [trackState](acpcore-aepcore.md#trackState)
* [collectPii](acpcore-aepcore.md#collectPii)
* [collectLaunchInfo](acpcore-aepcore.md#collectLaunchInfo)
* [getSdkIdentities](acpcore-aepcore.md#getSdkIdentities)
* [setLogLevel](acpcore-aepcore.md#setLogLevel)
* [registerURLHandler](acpcore-aepcore.md#registerURLHandler)
* [setAppGroup](acpcore-aepcore.md#setAppGroup)
* [configureWithAppId](acpcore-aepcore.md#configureWithAppId)
* [updateConfiguration](acpcore-aepcore.md#updateConfiguration)
* [configureWithFileInPath](acpcore-aepcore.md#configureWithFileInPath)
* [extensionVersion](acpcore-aepcore.md#extensionVersion)

### trackAction

* ACPCore

  ```text
  + (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) contextData
  ```

* MobileCore

  ```swift
  @objc(trackAction:data:)
  static func track(action: String?, data: [String: Any]?)
  ```

* AEPMobileCore

  ```text
  @objc(trackAction:data:)
  static func track(action: String?, data: [String: Any]?)
  ```

### trackState

* ACPCore

  ```text
  + (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) contextData;
  ```

* MobileCore

  ```swift
  @objc(trackState:data:)
  static func track(state: String?, data: [String: Any]?)
  ```

* AEPMobileCore

  ```text
  @objc(trackState:data:)
  static func track(state: String?, data: [String: Any]?)
  ```

### collectPii

* ACPCore

  ```text
  + (void) collectPii: (nonnull NSDictionary<NSString*, NSString*>*) data;
  ```

* MobileCore

  ```swift
  @objc(collectPii:)
  public static func collectPii(_ data: [String: Any])
  ```

* AEPMobileCore

  ```text
  @objc(collectPii:)
  public static func collectPii(_ data: [String: Any])
  ```

### collectLaunchInfo

* ACPCore

  ```text
  + (void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
  ```

* MobileCore

  ```swift
  @objc(collectLaunchInfo:)
  public static func collectLaunchInfo(_ userInfo: [String: Any])
  ```

* AEPMobileCore

  ```text
  @objc(collectLaunchInfo:)
  public static func collectLaunchInfo(_ userInfo: [String: Any])
  ```

### getSdkIdentities

* ACPCore

  ```text
  + (void) getSdkIdentities: (nullable void (^) (NSString* __nullable content)) callback;
  + (void) getSdkIdentitiesWithCompletionHandler: (nullable void (^) (NSString* __nullable content, NSError* _Nullable error)) completionHandler;
  ```

* MobileCore

  ```swift
  @objc(getSdkIdentities:)
  static func getSdkIdentities(completion: @escaping (String?, Error?) -> Void)
  ```

* AEPMobileCore

  ```text
  @objc(getSdkIdentities:)
  static func getSdkIdentities(completion: @escaping (String?, Error?) -> Void)
  ```

### setLogLevel

* ACPCore

  ```text
  + (void) setLogLevel: (ACPMobileLogLevel) logLevel;
  ```

* MobileCore

  ```swift
  @objc(setLogLevel:)
  public static func setLogLevel(_ level: LogLevel)
  ```

* AEPMobileCore

  ```text
  @objc(setLogLevel:)
  public static func setLogLevel(_ level: LogLevel)Void)
  ```

  **registerURLHandler**

* ACPCore

  ```text
  + (void) registerURLHandler: (nonnull BOOL (^) (NSString* __nullable url)) callback;
  ```

* MobileCore

  ```swift
  // Not supported
  ```

* AEPMobileCore

  ```text
  // Not supported
  ```

  **setAppGroup**

* ACPCore

  ```text
  + (void) setAppGroup: (nullable NSString*) appGroup;
  ```

* MobileCore

  ```swift
  public static func setAppGroup(_ group: String?)
  ```

* AEPMobileCore

  ```text
  public static func setAppGroup(_ group: String?)
  ```

### configureWithAppId

* ACPCore

  ```text
  + (void) configureWithAppId: (NSString* __nullable) appid;
  ```

* MobileCore

  ```swift
  static func configureWith(appId: String)
  ```

* AEPMobileCore

  \`\`\`objective-c static func configureWith\(appId: String\)

### updateConfiguration

* ACPCore

  ```text
  + (void) updateConfiguration: (NSDictionary* __nullable) config;
  ```

* MobileCore

  ```swift
  @objc(updateConfiguration:)
  static func updateConfigurationWith(configDict: [String: Any])
  ```

* AEPMobileCore

  \`\`\`objective-c @objc\(updateConfiguration:\) static func updateConfigurationWith\(configDict: \[String: Any\]\)

### configureWithFileInPath

* ACPCore

  ```text
  + (void) configureWithFileInPath: (NSString* __nullable) filepath;
  ```

* MobileCore

  ```swift
  static func configureWith(filePath: String)
  ```

* AEPMobileCore

  ```text
  static func configureWith(filePath: String)
  ```

### extensionVersion

* ACPCore

  ```text
  + (nonnull NSString*) extensionVersion;
  ```

* MobileCore

  ```swift
  @objc public static var extensionVersion: String
  ```

* AEPMobileCore

  ```text
  @objc public static var extensionVersion: String
  ```

