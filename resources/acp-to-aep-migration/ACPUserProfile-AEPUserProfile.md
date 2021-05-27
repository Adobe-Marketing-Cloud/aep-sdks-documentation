# Migration from ACPUserProfile to AEPUserProfile

This document is a reference comparison of ACPUserProfile (2.x) APIs against their equivalent APIs in AEPUserProfile (3.x).

## Primary `Classes`

| SdK VERSION    | LANGUAGE    | CLASS NAME           |
| -------------- | ----------- | -------------------- |
| ACPUserProfile | Objective-C | ACPUserProfile       |
| AEPUserProfile | Swift       | UserProfile          |
| AEPUserProfile | Objective-C | AEPMobileUserProfile |

## Public APIs

For more information, please read the [Profile API reference](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile/profile-api-references)

### extensionVersion

- ACPUserProfile

  ```objective-c
  + (nonnull NSString*) extensionVersion;
  ```

- UserProfile

  ```Swift
  static var extensionVersion: String
  ```
  
- AEPMobileUserProfile

  ```objective-c
  static var extensionVersion: String
  ```

### updateUserAttributes

- ACPUserProfile

  ```objective-c
  + (void) updateUserAttribute: (nonnull NSString*) attributeName withValue: (nullable NSString*) attributeValue;
  ```

- UserProfile

  ```swift
  public static func updateUserAttributes(attributeDict: [String: Any])
  ```
  
- AEPMobileUserProfile

  ```objective-c
  public static func updateUserAttributes(attributeDict: [String: Any])
  ```

###  removeUserAttribute

- ACPUserProfile

  ```objective-c
  + (void) removeUserAttribute: (nonnull NSString*) key
  ```

- UserProfile

  ```swift
  public static void removeUserAttribute(String attributeName)
  ```
  
- AEPMobileUserProfile

  ```objective-c
  public static void removeUserAttribute(String attributeName)
  ```

###  getUserAttributes

- ACPUserProfile

  ```objective-c
  + (void) getUserAttributes: (nullable NSArray <NSString*>*) attributNames withCompletionHandler: (nonnull void (^) (NSDictionary* __nullable userAttributes, NSError* _Nullable error)) completionHandler
  ```

- UserProfile

  ```swift
  public static void getUserAttributes(List<String> keys, AdobeCallback<Map<String, Object>> callback)
  ```
  
- AEPMobileUserProfile

  ```objective-c
  public static void getUserAttributes(List<String> keys, AdobeCallback<Map<String, Object>> callback)
  ```
