# Migrating to AEPAudience reference

This document is a reference comparison of AEPAudience (3.x) APIs against their equivalent ACPAudience (2.x) APIs.

The AEPAudience extension is implemented purely in Swift and is compatible with the AEPCore Swift SDK. To ensure a smooth transition from the ACPAudience SDK, there are no major changes on the API names or definition. For more details, follow the migration guide below for your Swift or Objective-C mobile application.  If explanation beyond showing API differences is necessary, it will be captured as an info hint within that API's section.

## AEPAudience classes

| Type          | AEP 3.x (Swift) | AEP 3.x (Objective-C) | ACP 2.x (Objective-C) |
| ------------- | :-------------- | --------------------- | --------------------- |
| Primary Class | Audience        | AEPMobileAudience     | ACPAudience           |



## AEPAudience APIs

### extensionVersion

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static var extensionVersion: String
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (nonnull NSString*) extensionVersion;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (nonnull NSString*) extensionVersion;
```

{% endtab %}

{% endtabs %}

### getVisitorProfile

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static func getVisitorProfile(completion: @escaping ([String: String]?, Error?) -> Void)
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (void) getVisitorProfile:^(NSDictionary<NSString *,NSString *> * _Nullable visitorProfile, NSError * _Nullable error)completion
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (void) getVisitorProfile:^(NSDictionary * _Nullable visitorProfile) callback;

+ (void) getVisitorProfileWithCompletionHandler:^(NSDictionary * _Nullable visitorProfile, NSError * _Nullable error) completionHandler;
```

{% endtab %}
{% endtabs %}

### reset

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static func reset()
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (void) reset;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (void) reset;
```

{% endtab %}

{% endtabs %}

### signalWithData

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static func signalWithData(data: [String: String], completion: @escaping ([String: String]?, Error?) -> Void) 
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (void) signalWithData:(NSDictionary<NSString *,NSString *> * _Nonnull data) completion:^(NSDictionary<NSString *,NSString *> * _Nullable vistorProfile, NSError * _Nullable error)completion
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (void) signalWithData: (NSDictionary<NSString *, NSString *> * _Nullable) data
                       callback:^(NSDictionary* _Nullable visitorProfile) callback;

+ (void) signalWithData: (NSDictionary<NSString *, NSString *> * _Nonnull) data
                        withCompletionHandler:^(NSDictionary * _Nullable visitorProfile, NSError *         _Nullable error) completionHandler;
```

{% endtab %}

{% endtabs %}

