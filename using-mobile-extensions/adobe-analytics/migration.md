# Migrating to AEPAnalytics reference

This document is a reference comparison of AEPAnalytics (3.x) APIs against their equivalent ACPAnalytics (2.x) APIs.

The AEPAnalytics extension is implemented purely in Swift and is compatible with the AEPCore Swift SDK. To ensure a smooth transition from the ACPAnalytics SDK, there are no major changes on the API names or definition. For more details, follow the migration guide below for your Swift or Objective-C mobile application.  If explanation beyond showing API differences is necessary, it will be captured as an info hint within that API's section.

## AEPAnalytics classes

| Type          | AEP 3.x (Swift) | AEP 3.x (Objective-C) | ACP 2.x (Objective-C) |
| ------------- | :-------------- | --------------------- | --------------------- |
| Primary Class | Analytics       | AEPMobileAnalytics    | ACPAnalytics          |



## AEPAnalytics APIs

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

### clearQueue

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static func clearQueue()
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (void) clearQueue;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (void) clearQueue;
```

{% endtab %}
{% endtabs %}

### getQueueSize

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static func getQueueSize(completion: @escaping (Int, Error?) -> Void)
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (void) getQueueSize:^(NSInteger, NSError * _Nullable)completion;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (void) getQueueSize: (nonnull void (^) (NSUInteger queueSize)) callback;

+ (void) getQueueSizeWithCompletionHandler: (nonnull void (^) (NSUInteger queueSize, NSError* __nullable error)) completionHandler;
```

{% endtab %}

{% endtabs %}

### sendQueuedHits

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static func sendQueuedHits()
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (void) sendQueuedHits;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (void) sendQueuedHits;
```

{% endtab %}

{% endtabs %}

### getTrackingIdentifier

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static func getTrackingIdentifier(completion: @escaping (String?, Error?) -> Void)
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (void) getTrackingIdentifier:^(NSString * _Nullable, NSError * _Nullable)completion;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (void) getTrackingIdentifier: (nonnull void (^) (NSString* __nullable trackingIdentifier)) callback;

+ (void) getTrackingIdentifierWithCompletionHandler: (nonnull void (^) (NSString* __nullable trackingIdentifier, NSError* __nullable error)) completionHandler;
```

{% endtab %}

{% endtabs %}

### setVisitorIdentifier

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static func setVisitorIdentifier(visitorIdentifier: String)
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (void) setVisitorIdentifier:(NSString * _Nonnull);
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (void) setVisitorIdentifier: (nonnull NSString*) visitorIdentifier;
```

{% endtab %}

{% endtabs %}

### getVisitorIdentifier

{% tabs %}

{% tab title="AEP 3.x (Swift)" %}

```swift
static func getVisitorIdentifier(completion: @escaping (String?, Error?) -> Void)
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objective-c
+ (void) getVisitorIdentifier:^(NSString * _Nullable, NSError * _Nullable)completion;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objective-c
+ (void) getVisitorIdentifier: (nonnull void (^) (NSString* __nullable visitorIdentifier)) callback;

+ (void) getVisitorIdentifierWithCompletionHandler: (nonnull void (^) (NSString* __nullable visitorIdentifier, NSError* __nullable error)) completionHandler;
```

{% endtab %}

{% endtabs %}
