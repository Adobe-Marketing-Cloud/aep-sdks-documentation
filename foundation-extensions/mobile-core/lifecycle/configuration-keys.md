# Configuration keys

## lifecycle.sessionTimeout

{% hint style="warning" %}
This configuration setting is only used in the Analytics use case, when using the [Lifecycle data content response](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/lifecycle/lifecycle-event-reference#lifecycle-data-content-response) event to determine session length.

In the Platform use case, events are dispatched based on [Lifecycle Application Foreground](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/lifecycle/lifecycle-event-reference#lifecycle-application-foreground) and [Lifecycle Application Background](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/lifecycle/lifecycle-event-reference#lifecycle-application-background) and not on a set session timeout.

{% endhint %}

Specifies the length of time, in seconds, that must elapse between the time the app is launched and before the launch is considered to be a new session. This timeout also applies when your application is sent to the background and reactivated.

Default value is 300 seconds (5 minutes).

**Tip**: The time that your app spends in the background is not included in the session length.

