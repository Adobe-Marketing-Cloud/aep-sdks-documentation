# Migration from ACPCore to AEPCore

This document is a reference comparison of ACPCore (2.x) APIs against their equivalent APIs in AEPCore (3.x).

## Primary `Classes`

The class name containing public APIs is different depending on which SDK and language combination being used.

| SDK version | Language    | Class name    |
| ----------- | ----------- | ------------- |
| ACPCore     | Objective-C | ACPCore       |
| AEPCore     | Swift       | MobileCore    |
| AEPCore     | Objective-C | AEPMobileCore |

## Additional public `Classes` and `Enums`

| SDK version | Language    | Class name        |
| ----------- | ----------- | ----------------- |
| ACPCore     | Objective-C | ACPMobileLogLevel |
| AEPCore     | Swift       | LogLevel          |
| AEPCore     | Objective-C | AEPLogLevel       |

## Core extension APIs

For more information, please read the [Mobile Core API reference](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/mobile-core-api-reference).

- [trackAction](#trackAction)
- [trackState](#trackState)
- [collectPii](#collectPii)
- [collectLaunchInfo](#collectLaunchInfo)
- [getSdkIdentities](#getSdkIdentities)
- [setLogLevel](#setLogLevel)
- [registerURLHandler](#registerURLHandler)
- [setAppGroup](#setAppGroup)
- [configureWithAppId](#configureWithAppId)
- [updateConfiguration](#updateConfiguration)
- [configureWithFileInPath](#configureWithFileInPath)
- [extensionVersion](#extensionVersion)

### trackAction

- ACPCore

  ```objective-c
  + (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) contextData
  ```

- MobileCore

  ```Swift
  @objc(trackAction:data:)
  static func track(action: String?, data: [String: Any]?)
  ```

- AEPMobileCore

  ```objective-c
  @objc(trackAction:data:)
  static func track(action: String?, data: [String: Any]?)
  ```

### trackState

- ACPCore

  ```objective-c
  + (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) contextData;
  ```

- MobileCore

  ```swift
  @objc(trackState:data:)
  static func track(state: String?, data: [String: Any]?)
  ```

- AEPMobileCore

  ```objective-c
  @objc(trackState:data:)
  static func track(state: String?, data: [String: Any]?)
  ```


### collectPii

- ACPCore

  ```objective-c
  + (void) collectPii: (nonnull NSDictionary<NSString*, NSString*>*) data;
  ```

- MobileCore

  ```swift
  @objc(collectPii:)
  public static func collectPii(_ data: [String: Any])
  ```

- AEPMobileCore

  ```objective-c
  @objc(collectPii:)
  public static func collectPii(_ data: [String: Any])
  ```

### collectLaunchInfo

- ACPCore

  ```objective-c
  + (void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
  ```

- MobileCore

  ```swift
  @objc(collectLaunchInfo:)
  public static func collectLaunchInfo(_ userInfo: [String: Any])
  ```

- AEPMobileCore

  ```objective-c
  @objc(collectLaunchInfo:)
  public static func collectLaunchInfo(_ userInfo: [String: Any])
  ```

### getSdkIdentities

- ACPCore

  ```objective-c
  + (void) getSdkIdentities: (nullable void (^) (NSString* __nullable content)) callback;
  + (void) getSdkIdentitiesWithCompletionHandler: (nullable void (^) (NSString* __nullable content, NSError* _Nullable error)) completionHandler;
  ```

- MobileCore

  ```swift
  @objc(getSdkIdentities:)
  static func getSdkIdentities(completion: @escaping (String?, Error?) -> Void)
  ```
  
- AEPMobileCore

  ```objective-c
  @objc(getSdkIdentities:)
  static func getSdkIdentities(completion: @escaping (String?, Error?) -> Void)
  ```

### setLogLevel

- ACPCore

  ```objective-c
  + (void) setLogLevel: (ACPMobileLogLevel) logLevel;
  ```

- MobileCore

  ```swift
  @objc(setLogLevel:)
  public static func setLogLevel(_ level: LogLevel)
  ```

- AEPMobileCore

  ```objective-c
  @objc(setLogLevel:)
  public static func setLogLevel(_ level: LogLevel)Void)
  ```
### registerURLHandler

- ACPCore

  ```objective-c
  + (void) registerURLHandler: (nonnull BOOL (^) (NSString* __nullable url)) callback;
  ```

- MobileCore

  ```swift
  // Not supported
  ```
  
- AEPMobileCore

  ```objective-c
  // Not supported
  ```
### setAppGroup

- ACPCore

  ```objective-c
  + (void) setAppGroup: (nullable NSString*) appGroup;
  ```

- MobileCore

  ```swift
  public static func setAppGroup(_ group: String?)
  ```
  
- AEPMobileCore

  ```objective-c
  public static func setAppGroup(_ group: String?)
  ```

### configureWithAppId

- ACPCore

  ```objective-c
  + (void) configureWithAppId: (NSString* __nullable) appid;
  ```

- MobileCore

  ```swift
  static func configureWith(appId: String)
  ```
  
- AEPMobileCore

  ```objective-c
  static func configureWith(appId: String)

### updateConfiguration

- ACPCore

  ```objective-c
  + (void) updateConfiguration: (NSDictionary* __nullable) config;
  ```

- MobileCore

  ```swift
  @objc(updateConfiguration:)
  static func updateConfigurationWith(configDict: [String: Any])
  ```
  
- AEPMobileCore

  ```objective-c
  @objc(updateConfiguration:)
  static func updateConfigurationWith(configDict: [String: Any])

### configureWithFileInPath

- ACPCore

  ```objective-c
  + (void) configureWithFileInPath: (NSString* __nullable) filepath;
  ```

- MobileCore

  ```swift
  static func configureWith(filePath: String)
  ```
  
- AEPMobileCore

  ```objective-c
  static func configureWith(filePath: String)
  ```

### extensionVersion

- ACPCore

  ```objective-c
  + (nonnull NSString*) extensionVersion;
  ```

- MobileCore

  ```swift
  @objc public static var extensionVersion: String 
  ```
  
- AEPMobileCore

  ```objective-c
  @objc public static var extensionVersion: String 
  ```

