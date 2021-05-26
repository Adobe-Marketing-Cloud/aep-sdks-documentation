# Migration from ACPCore to AEPCore

## Primary Classes

The class name containing public APIs is different depending on which SDK and language combination being used.

| SdK VERSION | LANGUAGE    | CLASS NAME    |
| ----------- | ----------- | ------------- |
| ACPCore     | Objective-C | ACPCore       |
| AEPCore     | Swift       | MobileCore    |
| AEPCore     | Objective-C | AEPMobileCore |

## Additional Public Classes and Enums

| SdK VERSION | LANGUAGE    | CLASS NAME        |
| ----------- | ----------- | ----------------- |
| ACPCore     | Objective-C | ACPMobileLogLevel |
| AEPCore     | Swift       | LogLevel          |
| AEPCore     | Objective-C | AEPLogLevel       |

## Public APIs

### Track app actions

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

### Track app states and views

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


###  Collect PII

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

### Collect launch information

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

### Retrieving stored identifiers

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

### Logging

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
### Handle open URL action

- ACPCore

  ```objective-c
  + (void) registerURLHandler: (nonnull BOOL (^) (NSString* __nullable url)) callback;
  ```

- MobileCore

  ```swift
  // Not supported
  ```

### Set App Group

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

### configureWithAppID

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

