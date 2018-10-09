# Signals Extension and Rules Engine integration

The rules that you set up can use the available triggers and conditions, and the action for these triggers and conditions will be one of the following types:

* A Postback
* PII data
* An open URL request

After these actions have been configured to be triggered and published, the Signals extension carries out the requested actions.

To send PII data to external destinations, the `PII` action can be set up to use the Rules engine to be triggered when certain triggers and traits match. The `PII` action can also be set up for a Signals event when setting up a rule. The `collectPii` API can then be used to trigger the rule and send the PII data.

## Rules Tokens {#rules-tokens}

Tokens are special strings used in rule actions as values which will be expanded by the SDK when the action is carried out. The format of a token is \`\`, which is any period-separated string that identifies the source of the data from which the token will be expanded. It can also be one of the reserved key names as described in the [Matching and Retreiving Values by keys](https://launch.gitbook.io/marketing-mobile-sdk-v5-by-adobe-documentation/rules-engine/rules-json#matching-and-retrieving-values-by-keys).

Some tokens are modifier functions that specify the transformation that is applied to the value that was replaced by the token. An example is `urlenc`, which specifies that the value will be URL-encoded before it is replaced in the rule.

Here is a usage example:

```text
​
```

### Using Tokens in Postbacks and PII Rule Actions {#using-tokens-in-postbacks-and-pii-rule-actions}

`Postbacks` and `PII` actions allow you to specify a `templateUrl` field and an optional `postbody`field that allow you to specify which tokens will be expanded by the Adobe Experience Cloud Platform SDKs when the postback or PII network call is triggered. For more information on tokens, see [Rule Tokens](https://docs.adobelaunch.com/extension-reference/mobile/signals/signals-extension-rules-engine-integration#rules-tokens).

To use data that is passed to the `collectPii` API to form a token, the format is:

```text
​
```

**Tip**: `mypii` is the key in the data dictionary that is passed to the `collectPii` API.

For more information about `collectPii` and its usage, see `collectPii` documentation in `ACPCore` extension for iOS and `MobileCore` extension for Android.

### Using Tokens in OpenURL Rule Actions {#using-tokens-in-openurl-rule-actions}

`Open URL` actions allow you to specify a URL, which can contain tokens that will be expanded by the Adobe Cloud Platform SDKs. For more information on tokens, see [Rule Tokens](https://docs.adobelaunch.com/extension-reference/mobile/signals/signals-extension-rules-engine-integration#rules-tokens).

