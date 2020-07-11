# Audience Manager API reference

## getVisitorProfile

Returns the visitor profile that was most recently updated. The visitor profile is saved in the SDK's local storage for access across multiple launches of your app. If no audience signal has been sent before, when this API is called, a null value is returned.

{% tabs %}
{% tab title="Android" %}
### getVisitorProfile

This API returns the visitor profile that was most recently obtained. For easy access across multiple launches of your app, the visitor profile is saved in `SharedPreferences`. If no signal has been submitted, null is returned.

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

This API returns the visitor profile that was most recently obtained. For easy access across multiple launches of your app, the visitor profile is saved in `NSUserDefaults`. If no signal has been submitted, nil is returned.

#### **Syntax**

```objectivec
+ (void) getVisitorProfile: (nonnull void (^) (NSDictionary* __nullable visitorProfile)) callback;
```

#### **Example**

**Objective C**

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

{% tab title="React Native" %}
**JavaScript**

### getVisitorProfile

```jsx
ACPAudience.getVisitorProfile().then(profile => console.log("AdobeExperienceSDK: Visitor Profile: " + profile));
```
{% endtab %}
{% endtabs %}

## registerExtension

This API registers an extension class that was derived from `ACPExtension` with a unique name. This call validates the parameters to ensure that the name is not empty, the name is unique, and that the parent class is ACPExtension.

{% tabs %}
{% tab title="Android" %}
### registerExtension

#### **Syntax**

```java
public  static void registerExtension() throws InvalidInitException
```

#### **Example**

```java
Audience.registerExtension();
```
{% endtab %}

{% tab title="iOS" %}
### registerExtension

#### **Syntax**

```objectivec
+ (BOOL) registerExtension: (nonnull Class) extensionClass
                     error: (NSError* _Nullable* _Nullable) error;
```

#### **Examples**

**Objective-C**

```objectivec
[ACPAudience registerExtension];
```

**Swift**

```swift
ACPAudience.registerExtension()
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### registerExtension

```jsx
ACPAudience.registerExtension();
```
{% endtab %}
{% endtabs %}

## reset

This API helps you reset the Audience Manager UUID and purges the current visitor profile.

{% hint style="info" %}
For more information about the UUID, the DPID, the DPUUID and other Audience Manager identifiers, see [Index of IDs in Audience Manager](https://marketing.adobe.com/resources/help/en_US/aam/ids-in-aam.html).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### **reset**

This API resets the Audience Manager UUID and purges the current visitor profile from `android.content.SharedPreferences`. The Audience reset also clears the current in-memory DPID and DPUUID variables.

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

This API resets the Audience Manager UUID and purges the current visitor profile from `UserDefaults`. The Audience reset also clears the current in-memory DPID and DPUUID variables.

#### **Syntax**

```objectivec
+ (void) reset;
```

#### **Examples**

**Objective C**

```objectivec
[ACPAudience reset];
```

**Swift**

```swift
ACPAudience.reset()
```
{% endtab %}

{% tab title="React Native" %}
#### **JavaScript**

### **reset**

```jsx
ACPAudience.reset();
```
{% endtab %}
{% endtabs %}

## signalWithData

Use this method to send a signal with traits to Audience Manager and get the matching segments returned in a block callback. Audience manager sends the UUID in response to an initial signal call. The UUID is persisted on local SDK storage and is sent by the SDK to Audience Manager in all subsequent signal requests.

If you are using the Experience Cloud ID \(ECID\) Service \(formerly MCID\), the ECID and other custom identifiers for the same visitor are sent with each signal request. The visitor profile that is returned by Audience Manager is saved in SDK local storage and is updated with subsequent signal calls.

{% hint style="info" %}
For more information about the UUID and other Audience Manager identifiers, see [Index of IDs in Audience Manager](https://marketing.adobe.com/resources/help/en_US/aam/ids-in-aam.html).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### **signalWithData**

This API sends Audience Manager a signal with traits and returns the matching segments for the visitor in a callback.

Audience Manager sends the AAM UUID in response in initial signal call. The AAM UUID is persisted in `SharedPreferences` and is sent by the SDK in all subsequent signal requests. If available, the ECID is also sent in each signal request with the DPID and the DPUUID. The visitor profile that Audience Manager returns is saved in `SharedPreferences` and is updated with every signal call.

#### **Syntax**

```java
public static void signalWithData(final Map<String, String> data, final AdobeCallback<Map<String, String>> callback)
```

* `data` is the traits data for the current visitor.
* `callback` is the void method that is invoked with the visitor's profile as a parameter.

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

This API sends Audience Manager a signal with traits and returns the matching segments for the visitor in a callback.

Audience Manager sends the AAM UUID in response in initial signal call. The AAM UUID is persisted in `NSUserDefaults` and is sent by the SDK in all subsequent signal requests. If available, the Experience Cloud ID \(MID\) is also sent in each signal request with the DPID and the DPUUID. The visitor profile that Audience Manager returns is saved in `NSUserDefaults`ß and is updated with every signal call.

#### **Syntax**

```objectivec
+ (void) signalWithData: (NSDictionary<NSString*, NSString*>* __nullable) data
                       callback: (nullable void (^) (NSDictionary* __nullable visitorProfile)) callback;
```

* `data` is the traits data for the current visitor.
* `callback` is the void method that is invoked with the visitor's profile as a parameter.

#### Examples\*\*

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

{% tab title="React Native" %}
#### JavaScript

### **signalWithData**

```jsx
ACPAudience.signalWithData({"yourDataKey": "yourDataValue"}).then(profile => console.log("AdobeExperienceSDK: Visitor Profile: " + profile));
```
{% endtab %}
{% endtabs %}
