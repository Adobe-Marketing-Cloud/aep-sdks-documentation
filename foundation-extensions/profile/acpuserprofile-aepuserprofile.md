# Migrating to AEPUserProfile

This document is a reference comparison of ACPUserProfile \(2.x\) APIs against their equivalent APIs in AEPUserProfile \(3.x\).

## Primary `Classes`

| SDK version | Language | Class name |
| :--- | :--- | :--- |
| ACPUserProfile | Objective-C | ACPUserProfile |
| AEPUserProfile | Swift | UserProfile |
| AEPUserProfile | Objective-C | AEPMobileUserProfile |

## UserProfile extension APIs

For more information, please read the [Profile API reference](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile/profile-api-references).

### extensionVersion

* ACPUserProfile

  ```text
  + (nonnull NSString*) extensionVersion;
  ```

* UserProfile

  ```swift
  static var extensionVersion: String
  ```

* AEPMobileUserProfile

  ```text
  static var extensionVersion: String
  ```

### updateUserAttributes

* ACPUserProfile

  ```text
  + (void) updateUserAttribute: (nonnull NSString*) attributeName withValue: (nullable NSString*) attributeValue;
  ```

* UserProfile

  ```swift
  public static func updateUserAttributes(attributeDict: [String: Any])
  ```

* AEPMobileUserProfile

  ```text
  public static func updateUserAttributes(attributeDict: [String: Any])
  ```

### removeUserAttribute

* ACPUserProfile

  ```text
  + (void) removeUserAttribute: (nonnull NSString*) key
  ```

* UserProfile

  ```swift
  public static void removeUserAttribute(String attributeName)
  ```

* AEPMobileUserProfile

  ```text
  public static void removeUserAttribute(String attributeName)
  ```

### getUserAttributes

* ACPUserProfile

  ```text
  + (void) getUserAttributes: (nullable NSArray <NSString*>*) attributNames withCompletionHandler: (nonnull void (^) (NSDictionary* __nullable userAttributes, NSError* _Nullable error)) completionHandler
  ```

* UserProfile

  ```swift
  public static void getUserAttributes(List<String> keys, AdobeCallback<Map<String, Object>> callback)
  ```

* AEPMobileUserProfile

  ```text
  public static void getUserAttributes(List<String> keys, AdobeCallback<Map<String, Object>> callback)
  ```

