# Migrating to AEPSignal

This document is a reference comparison of ACPSignal \(2.x\) APIs against their equivalent APIs in AEPSignal \(3.x\).

## Primary `Classes`

| SDK version | Language | Class name |
| :--- | :--- | :--- |
| ACPSignal | Objective-C | ACPSignal |
| AEPSignal | Swift | Signal |
| AEPSignal | Objective-C | AEPMobileSignal |

## Signal extension APIs

For more information, please read the [Signal API reference](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/signals/signal-api-reference).

### extensionVersion

* ACPSignal

  ```text
  + (nonnull NSString*) extensionVersion;
  ```

* Signal

  ```swift
  static var extensionVersion: String
  ```

* AEPMobileSignal

  ```text
  static var extensionVersion: String
  ```

