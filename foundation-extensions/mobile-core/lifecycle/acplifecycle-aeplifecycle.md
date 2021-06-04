# Migrating to AEPLifecycle

This document is a reference comparison of ACPLifecycle \(2.x\) APIs against their equivalent APIs in AEPLifecycle \(3.x\).

## Primary `Classes`

| SDK version | Language | Class name |
| :--- | :--- | :--- |
| ACPLifecycle | Objective-C | ACPLifecycle |
| AEPLifecycle | Swift | Lifecycle |
| AEPLifecycle | Objective-C | AEPMobileLifecycle |

## Lifecycle extension APIs

For more information, please read the [Lifecycle API reference](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/lifecycle/lifecycle-api-reference).

### extensionVersion

* ACPLifecycle

  ```text
  + (nonnull NSString*) extensionVersion;
  ```

* Lifecycle

  ```swift
  static var extensionVersion: String
  ```

* AEPMobileCore

  ```text
  static var extensionVersion: String
  ```

### lifecycleStart

* ACPCore

  ```text
  + (void) lifecycleStart: (nullable NSDictionary<NSString*, NSString*>*) additionalContextData;
  ```

* MobileCore

  ```swift
  @objc(lifecycleStart:)
  static func lifecycleStart(additionalContextData: [String: Any]?)
  ```

* AEPMobileCore

  ```text
  @objc(lifecycleStart:)
  static func lifecycleStart(additionalContextData: [String: Any]?)
  ```

### lifecyclePause

* ACPCore

  ```text
  + (void) lifecyclePause;
  ```

* MobileCore

  ```swift
  @objc(lifecyclePause)
  static func lifecyclePause()
  ```

* AEPMobileCore

  ```text
  @objc(lifecyclePause)
  static func lifecyclePause()
  ```

