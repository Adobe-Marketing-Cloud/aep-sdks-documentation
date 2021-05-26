# Migration from ACPSignal to AEPSignal

## Primary Classes

| SdK VERSION | LANGUAGE    | CLASS NAME      |
| ----------- | ----------- | --------------- |
| ACPSignal   | Objective-C | ACPSignal       |
| AEPSignal   | Swift       | Signal          |
| AEPSignal   | Objective-C | AEPMobileSignal |

## Public APIs

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