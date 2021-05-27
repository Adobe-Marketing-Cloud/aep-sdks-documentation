# Migration from ACPSignal to AEPSignal

This document is a reference comparison of ACPSignal (2.x) APIs against their equivalent APIs in AEPSignal (3.x).

## Primary `Classes`

| SdK VERSION | LANGUAGE    | CLASS NAME      |
| ----------- | ----------- | --------------- |
| ACPSignal   | Objective-C | ACPSignal       |
| AEPSignal   | Swift       | Signal          |
| AEPSignal   | Objective-C | AEPMobileSignal |

## Public APIs

For more information, please read the [Signal API reference](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/signals/signal-api-reference)

### extensionVersion

- ACPSignal 

  ```objective-c
  + (nonnull NSString*) extensionVersion;
  ```

- Signal

  ```Swift
  static var extensionVersion: String
  ```
  
- AEPMobileSignal

  ```objective-c
  static var extensionVersion: String
  ```
