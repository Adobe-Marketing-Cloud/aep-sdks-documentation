# Signals extension and Rules Engine integration

The rules that you set up can use the available triggers and conditions, which results in one of the following actions:

* A postback
* PII data
* An open URL request

After these actions have been configured to be triggered and published, the Signals extension carries out the requested actions.

To send PII data to external destinations, the `PII` action can trigger the Rules engine when certain triggers and traits match. When setting a rule, you can also set the `PII` action for a Signals event. The `collectPii` API can then be used to trigger the rule and send the PII data.

## Rules tokens <a id="rules-tokens"></a>

Tokens are special strings used in rule actions as values, which are expanded by the SDK when the action is carried out. The format of a token is \`\`, which is any period-separated string that identifies the source of the data from which the token is expanded. It can also be one of the reserved key names as described in the [Matching and Retrieving Values by keys](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#matching-and-retrieving-values-by-keys).

Some tokens are modifier functions that specify the transformation that is applied to the value that was replaced by the token. An example is `urlenc`, which specifies that the value will be URL-encoded before it is replaced in the rule.

Here is a usage example:

```text
​
```

### Using tokens in Postbacks and PII rule actions <a id="using-tokens-in-postbacks-and-pii-rule-actions"></a>

`Postbacks` and `PII` actions allow you to specify a `templateUrl` field and an optional `postbody`field that allow you to specify which tokens will be expanded by the Experience Platform SDKs when the postback or PII network call is triggered. For more information on tokens, see [Rule Tokens](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/signals/signals-extension-and-rules-engine-integration#rules-tokens).

To use data that is passed to the `collectPii` API to form a token, the format is:

```text
​
```

**Tip**: `mypii` is the key in the data dictionary that is passed to the `collectPii` API.

For more information about `collectPii` and its usage, see `collectPii` in [Mobile Core API reference](https://aep-sdks.gitbook.io/docs/~/edit/drafts/-LbTmxizQnkdvn7eot_p/using-mobile-extensions/mobile-core/mobile-core-api-reference).

### Using tokens in OpenURL rule actions <a id="using-tokens-in-openurl-rule-actions"></a>

`Open URL` actions allow you to specify a URL, which can contain the tokens that will be expanded by the SDKs. For more information about tokens, see [Rule Tokens](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/signals/signals-extension-and-rules-engine-integration#rules-tokens).

