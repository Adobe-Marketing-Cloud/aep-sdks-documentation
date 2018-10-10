# Target API Reference

## Get custom visitor IDs

Use this API to get the custom visitor ID for Target.

{% tabs %}
{% tab title="Android" %}
### getThirdPartyId

The callback will be invoked to return the `thirdPartyId` value, or if no third-party ID is set, `null` is returned.

#### Syntax

```java
public static void getThirdPartyId(final AdobeCallback<String> callback)
```

#### Example

```java
Target.getThirdPartyId(new AdobeCallback<String>() {                    
    @Override
    public void call(String thirdPartyID) {
                // read target's thirdPartyID
    }
});
```
{% endtab %}

{% tab title="iOS" %}

{% endtab %}
{% endtabs %}

## Set custom visitor IDs

Use this API to set custom visitor IDs for Target. 

{% hint style="info" %}
This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall or when the reset experience API is used.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### setThirdPartyId

### Syntax

```java
public static void setThirdPartyId(final String thirdPartyId)
```

### Example

```java
Target.setThirdPartyId("third-party-id");
```
{% endtab %}

{% tab title="iOS" %}

{% endtab %}
{% endtabs %}

## Reset user experience

Use this API to reset the user's experience by removing the visitor identifiers. This method also removes previously set third-party and Target IDs from persistent storage.

{% tabs %}
{% tab title="Android" %}
### resetExperience

#### Syntax

```java
public static void resetExperience()
```

#### Example

```java
Target.resetExperience();
```
{% endtab %}

{% tab title="iOS" %}

{% endtab %}
{% endtabs %}

## Get Target user identifier

Gets the Target user identifier.

{% tabs %}
{% tab title="Android" %}
### getTntId

The callback will be invoked to return the `tntId` value, o, if no Target ID is set, `null` is returned.

Target returns `tntId` upon a successful call to `loadRequests` or `prefetchContent`. Once set in the SDK, this ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall or when `resetExperience` API is called.

#### Syntax

```java
public static void getTntId(final AdobeCallback<String> callback)
```

#### Example

```java
Target.getTntId(new AdobeCallback<String>() {
    @Override
    public void call(String value) {
        // read target's tntid
    }
});
```
{% endtab %}

{% tab title="iOS" %}

{% endtab %}
{% endtabs %}

## Load Target requests

Sends a batch request to your configured Target server for multiple mbox locations that are specified.

{% tabs %}
{% tab title="Android" %}
### TargetRequest Builder

`TargetRequest` builder helps to create a `TargetRequest` instance. The returned instance can be used with `loadRequests`, which accepts a `TargetRequest` object list to retrieve offers for the specified mbox locations.

#### Syntax

```java
TargetRequest request = new TargetRequest.Builder("mboxName","defaultContent")
                .setMboxParameters(new HashMap<String, String>())
                .setOrderParameters(new HashMap<String, Object>())
                .setProductParameters(new HashMap<String, String>())
                .setContentCallback(new AdobeCallback<String>() {
                    @Override
                    public void call(String value) {
                        // do something with target content.
                    }
                }).build();
```

### loadRequests

Sends a batch request to your configured Target server for multiple mbox locations that are specified in the `TargetRequest` list. Each object in the array contains a callback function, which will be invoked when content is available for its given mbox location.

#### Syntax

```java
public static void loadRequests(final List<TargetRequest> requestArray,
                                    final Map<String, Object> profileParameters);
```

#### Example

```java
// define parameters for first request
Map<String, Object> mboxParameters1 = new HashMap<>();
mboxParameters1.put("status", "platinum");

// define parameters for second request
Map<String, Object> mboxParameters2 = new HashMap<>();
mboxParameters2.put("userType", "paid");

List<String> purchasedIds = new ArrayList<String>();
purchasedIds.add("34");
purchasedIds.add("125"); 

Map<String, Object> orderParameters2 = new HashMap<>();
orderParameters2.put("id", "ADCKKIM");
orderParameters2.put("total", "344.30");
orderParameters2.put("purchasedProductIds",  purchasedIds);

Map<String, Object> productParameters2 = new HashMap<>();
productParameters2.put("id", "24D3412");
productParameters2.put("categoryId","Books");

TargetRequest request1 = new TargetRequest.Builder("mboxName1", "defaultContent1")
                .setMboxParameters(mboxParameters1)
                .setContentCallback(new AdobeCallback<String>() {
                    @Override
                    public void call(String value) {
                        // do something with target content.
                    }
                }).build();

TargetRequest request2 = new TargetRequest.Builder("mboxName2", "defaultContent2")
                .setMboxParameters(mboxParameters2)
                .setOrderParameters(orderParameters2)
                .setProductParameters(productParameters2)
                .setContentCallback(new AdobeCallback<String>() {
                    @Override
                    public void call(String value) {
                        // do something with target content.
                    }
                }).build();

// Creating Array of Request Objects
List<TargetRequest> locationRequests = new ArrayList<>();
locationRequests.add(request1);
locationRequests.add(request2);

 // Define the profile parameters map.
Map<String, Object> profileParameters = new HashMap<>();
profileParameters.put("ageGroup", "20-32");

// Call the targetLoadRequests API.
Target.loadRequests(locationRequests, profileParameters);
```
{% endtab %}

{% tab title="iOS" %}

{% endtab %}
{% endtabs %}

## Send mbox click notification

Sends a click notification to configured Target server for a prefetched or regular mbox location. Click metric should be enabled for the provided location name in Target.

{% tabs %}
{% tab title="Android" %}
### locationClicked

Sends a click notification to configured Target server for a prefetched or regular mbox location. Click metric should be enabled for the provided location name in Target. If notification is sent for a prefetched mbox, its contents should already have been requested with `loadRequests` indicating that the mbox was viewed.

#### Syntax:

```java
public static void locationClicked(final String mboxName,
                                    final Map<String, String> mboxParameters
                                    final Map<String, String> productParameters
                                    final Map<String, Object> orderParameters
                                    final Map<String, String> profileParameters);
```

#### Example

```java
// Define Mbox parameters
Map<String, Object> mboxParameters = new HashMap<>();
mboxParameters.put("membership", "prime");

// Define Product parameters
Map<String, Object> productParameters = new HashMap<>();
productParameters.put("id", "CEDFJC");
productParameters.put("categoryId","Electronics");

List<String> purchasedIds = new ArrayList<String>();
purchasedIds.add("81");
purchasedIds.add("123"); 
purchasedIds.add("190");

// Define Order parameters
Map<String, Object> orderParameters = new HashMap<>();
orderParameters.put("id", "NJJICK");
orderParameters.put("total", "650");
orderParameters.put("purchasedProductIds",  purchasedIds);

// Creating Profile parameters
Map<String, Object> profileParameters = new HashMap<>();
profileParameters.put("ageGroup", "20-32");

Target.locationClicked("cartLocation", mboxParameters, productParameters, orderParameters, profileParameters);
```
{% endtab %}

{% tab title="iOS" %}

{% endtab %}
{% endtabs %}

## Public classes

{% tabs %}
{% tab title="Android" %}
### TargetRequest

Here is a code sample for this class in Android:

```java
public class TargetRequest extends TargetObject {

    private TargetRequest() {}

    /**
    * Builder used to construct a TargetRequest object.
    */
    public static class Builder {
        private TargetRequest targetRequest;

        /**
         * Create a TargetRequest Builder.
         *
         * @param mboxName String mbox name for this request
         * @param defaultContent String default content for this request
         */
        public Builder(final String mboxName, final String defaultContent);

        /**
         * Set mbox parameters for this request.
         *
         * @param mboxParameters Map<String, String> mbox parameters
         * @return this builder
         */
        public Builder setMboxParameters(final Map<String, String> mboxParameters);

        /**
        * Set order parameters for this request.
        *
        * @param orderParameters Map<String, Object> order parameters
        * @return this builder
        */
        public Builder setOrderParameters(final Map<String, Object> orderParameters);

        /**
         * Set profile parameters for this request.
         *
         * @param productParameters Map<String, String> product parameters
         * @return this builder
         */
        public Builder setProductParameters(final Map<String, String> productParameters);

        /**
        * Set the callback function for this request.
        *
        * @param contentCallback AdobeCallback<String> which will get called with the returning content
        * @return this builder
        */
        public Builder setContentCallback(final AdobeCallback<String> contentCallback);

        /**
         * Build the TargetRequest.
         *
         * @return TargetRequest the target request object
         */
        public TargetRequest build();
    }
}
```

### TargetPrefetch

Here is a code sample for this class in Android:

```java
public class TargetPrefetch extends TargetObject {
    private TargetPrefetch() {}

    /**
     * Builder used to construct a TargetPrefetch object
     */
    public static class Builder {
        private TargetPrefetch targetPrefetch;

        /**
         * Create a TargetPrefetch Builder.
         *
         * @param mboxName String mbox name for this request
         */
         public Builder(final String mboxName);

        /**
         * Set mbox parameters for this request.
         *
         * @param mboxParameters Map<String, String> mbox parameters
         * @return this builder
         */
         public Builder setMboxParameters(final Map<String, String> mboxParameters);

        /**
         * Set order parameters for this request.
         *
         * @param orderParameters Map<String, String> order parameters
         * @return this builder
         */
         public Builder setOrderParameters(final Map<String, Object> orderParameters);

        /**
         * Set product parameters for this request.
         *
         * @param productParameters Map<String, String> product parameters
         * @return this builder
         */
         public Builder setProductParameters(final Map<String, String> productParameters);

        /**
         * Build and return TargetPrefetch
         *
         * @return TargetPrefetch the target prefetch object
         */
         public TargetPrefetch build();
    }

}
```
{% endtab %}

{% tab title="iOS" %}

{% endtab %}
{% endtabs %}

