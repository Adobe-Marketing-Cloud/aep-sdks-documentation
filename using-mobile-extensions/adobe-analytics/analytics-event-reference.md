# Analytics Event Reference

## Internal Events for Adobe Analytics



In addition to the Analytics hits that are sent as a result of the track call, the Adobe Experience Cloud Platform SDKs also tracks some internal events that are based on the communication with other modules.

Here is a list of the events by module:

### Lifecycle Module

Here are the Analytics events in the Lifecycle module:

#### Install Event

The SDK tracks the application install details when lifecycle is enabled. These details include the install date and the daily engaged/monthly engaged user badges.

#### Launch Event

The SDK tracks every new launch of the application when lifecycle is enabled.

A launch is considered to be new when the following conditions are met:

* The application is reopened from the background after the configured session timeout.
* The application is opened after a force close.

Launch data includes information about the application's number of launches, days since first run, days since last use, user daily/monthly engaged badges along with other lifecycle metrics.

We also track the application version upgrades.

#### Crash Event

If your application is terminated without having first been backgrounded, the SDK reports a crash the next time your app is launched.

This will be sent as an individual hit if the `backdateSessionInfo` flag is enabled in your configuration, otherwise it will be sent as part of the launch event.

#### SessionInfo

This hit contains information about the previous launch session, more specifically the session length.

This will be sent as an individual hit if backdateSessionInfo flag is enabled in your configuration, otherwise it will be sent as part of the launch event.

### Identity Module

Here are the Analytics events that are triggered when the Identity module is enabled:

* Push

The SDK tracks changes in the user's push notifications preference. A new hit is sent whenever the user opt-in/opt-out for push notifications.

### Messages Module

Here are the Analytics events that are triggered when the Messages module is enabled:

* In-App Message

The SDK tracks the following metrics for your in-app messages:

For Full Screen and Alert style in-app messages:

* Impressions: when user triggers an in-app message.
* Click throughs: when user pushes the Click-through button.
* Cancels: when user pushes the Cancel button.

For local \(remote\) notifications:

* Impressions: when user triggers the notification.
* Opens: when user opens app from the notification. This will be tracked with the trackAdobeDeepLink method.

### Target Module

Here is the Analytics event in the Target module:

* AnalyticsForTarget

  The SDK forwards Target's data to analytics when A4T is enabled in Target Services.

