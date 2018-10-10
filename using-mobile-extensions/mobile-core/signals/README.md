# Signals

By leveraging the same triggers and traits that you use to display an in-app message, you can configure the SDK to send customized data to a third-party destination. Also, with the appropriate permissions and configurations, you can use the `collectPii` API to send personally identifiable information \(PII\) to a remote server.

Here are the implications of the privacy status for this extension:

* When the `global.privacy` configuration is set to `optedout`, the Signals extension clears all queued hits and drops future network send requests.
* If the configuration is `optunknown`, the network send requests will be queued on the SDK but are not sent out.
* If the configuration is `optedin`, the network requests to a third-party destination are allowed, provided the trigger conditions match.

