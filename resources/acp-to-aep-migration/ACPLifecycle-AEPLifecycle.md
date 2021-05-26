# Migration from ACPLifecycle to AEPLifecycle

## Primary Classes

| SdK VERSION  | LANGUAGE    | CLASS NAME         |
| ------------ | ----------- | ------------------ |
| ACPLifecycle | Objective-C | ACPLifecycle       |
| AEPLifecycle | Swift       | Lifecycle          |
| AEPLifecycle | Objective-C | AEPMobileLifecycle |

## Public APIs

### extensionVersion

- ACPLifecycle

  ```objective-c
  + (nonnull NSString*) extensionVersion;
  ```

- Lifecycle

  ```Swift
  static var extensionVersion: String
  ```
  
- AEPMobileCore

  ```objective-c
  static var extensionVersion: String
  ```

### lifecycleStart

- ACPCore

  ```objective-c
  + (void) lifecycleStart: (nullable NSDictionary<NSString*, NSString*>*) additionalContextData;
  ```

- MobileCore

  ```swift
  @objc(lifecycleStart:)
  static func lifecycleStart(additionalContextData: [String: Any]?)
  ```

- AEPMobileCore

  ```objective-c
  @objc(lifecycleStart:)
  static func lifecycleStart(additionalContextData: [String: Any]?)
  ```


###  lifecyclePause

- ACPCore

  ```objective-c
  + (void) lifecyclePause;
  ```

- MobileCore

  ```swift
  @objc(lifecyclePause)
  static func lifecyclePause()
  ```

- AEPMobileCore

  ```objective-c
  @objc(lifecyclePause)
  static func lifecyclePause()
  ```