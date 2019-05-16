# Audience Manager API reference

## Send signals to Audience Manager

Use this method to send a signal with traits to Audience Manager and get the matching segments returned in a block callback. Audience manager sends the UUID in response to an initial signal call. The UUID is persisted on local SDK storage and is sent by the SDK to Audience Manager in all subsequent signal requests.

If you are using the Experience Cloud ID \(ECID\) Service \(formerly MCID\), the ECID and other custom identifiers for the same visitor are sent with each signal request. The visitor profile that is returned by Audience Manager is saved in SDK local storage and is updated with subsequent signal calls.

{% hint style="info" %}
For more information about the UUID and other Audience Manager identifiers, see [Index of IDs in Audience Manager](https://marketing.adobe.com/resources/help/en_US/aam/ids-in-aam.html).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### **signalWithData**

In Android, the UUID is persisted in `SharedPreferences`.

#### **Syntax**

```java
public static void signalWithData(final Map<String, String> data, final AdobeCallback<Map<String, String>> callback)
```

#### **Example**

```java
AdobeCallback<Map<String, String>> visitorProfileCallback = new AdobeCallback<Map<String, String>>() {
    @Override
    public void call(final Map<String, String> visitorProfile) {
        // your own customized code
    }
};
​
Map<String, String> traits = new HashMap<String, String>();
traits.put("trait", "xyz");
Audience.signalWithData(traits, visitorProfileCallback);
```
{% endtab %}

{% tab title="iOS" %}
### signalWithData

On iOS, UUID is persisted in `NSUserDefaults`.

#### **Syntax**

```objectivec
+ (void) signalWithData: (NSDictionary<NSString*, NSString*>* __nullable) data
                       callback: (nullable void (^) (NSDictionary* __nullable visitorProfile)) callback;
```

#### **Examples**

**Objective-C**

```objectivec
NSDictionary *traits = @{@"key1":@"value1",@"key2":@"value2"};
[ACPAudience signalWithData:traits callback:^(NSDictionary* visitorProfile){
  // your customized code
}];
```

**Swift**

```swift
ACPAudience.signal(withData: ["key1": "value1", "key2": "value2"], callback: {(_ response: [AnyHashable: Any]?) -> Void in
  // your customized code
})
```
{% endtab %}
{% endtabs %}

## Reset identifiers and profiles

This API helps you reset the Audience Manager UUID and purges the current visitor profile.

{% hint style="info" %}
For more information about the UUID, the DPID, the DPUUID and other Audience Manager identifiers, see [Index of IDs in Audience Manager](https://marketing.adobe.com/resources/help/en_US/aam/ids-in-aam.html).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### **reset**

#### **Syntax**

```java
public static void reset()
```

#### **Example**

```java
Audience.reset();
```
{% endtab %}

{% tab title="iOS" %}
### **reset**

#### **Syntax**

```objectivec
+ (void) reset;
```

#### **Examples**

**Objective-C**

```objectivec
[ACPAudience reset];
```

**Swift**

```swift
ACPAudience.reset()
```
{% endtab %}
{% endtabs %}

## Get the visitor profile

Returns the visitor profile that was most recently updated. The visitor profile is saved in the SDK's local storage for access across multiple launches of your app. If no audience signal has been sent before, when this API is called, a null value is returned.

{% tabs %}
{% tab title="Android" %}
### getVisitorProfile

In Android, the visitor profile is saved in `SharedPreferences`.

#### **Syntax**

```java
public static void getVisitorProfile(final AdobeCallback<Map<String, String>> adobeCallback)
```

#### **Example**

```java
AdobeCallback<Map<String, String>> visitorProfileCallback = new AdobeCallback<Map<String, String>>() {
    @Override
    public void call(final Map<String, String> visitorProfile) {
        // your own customized code
    }
};

Audience.getVisitorProfile(visitorProfileCallback);
```
{% endtab %}

{% tab title="iOS" %}
### getVisitorProfile

On iOS, the visitor profile is saved in `NSUserDefaults`.

#### **Syntax**

```objectivec
+ (void) getVisitorProfile: (nonnull void (^) (NSDictionary* __nullable visitorProfile)) callback;
```

#### **Example**

**Objective-C**

```objectivec
[ACPAudience getVisitorProfile:^(NSDictionary* visitorProfile){
  // your customized code
}];
```

**Swift**

```swift
ACPAudience.getVisitorProfile({(_ response: [AnyHashable: Any]?) -> Void in
    // your customized code
})
```
{% endtab %}
{% endtabs %}

