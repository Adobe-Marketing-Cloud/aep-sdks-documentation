# Push Messaging Guide

Push notifications serve as a quick communication channel enabling you to convey messages, offers, or other information to your mobile app users. Typically, the end user must opt-in to receive push notifications; opt-in usually takes place during the install process and end users are provided with a way to manage notifications if they change their minds later on. An important advantage of push notifications in mobile computing is that the technology doesn't require specific applications on a mobile device to be open in order for a message to be received. This allows a smartphone to receive and display notifications even when the device's screen is locked and the mobile app is in the background or closed.

Adobe Journey Optimizer allows you to send time-sensitive, relevant, and personalized push messages on a large-scale. A segment of customer profiles can be targeted to receive rich push notifications on their iOS and Android mobile devices. These segments can be created on the basis of past or live user experience events, user record data, or a combination of user interactions and data. Once a journey is live, you can view detailed reports on how many messages were sent, failed for what reason and also push tracking information like how many users clicked on them.

This document will walk you through a basic push notifications end-to-end data flow using Adobe Journey Optimizer and a user flow diagram to explain how each role fulfills its responsibilities and collaborates to bring the push data flow together. 



## Understanding Push Data Flow

This diagram shows a basic push messaging data flow and gives a peek at the various Adobe products and components involved in the flow. 

![Push Data Flow](../../.gitbook/assets/push-data-flow.png)



### Push Data Flow Components

#### Cloud Messaging Providers

Cloud Messaging Providers are third-party services that enable us to deliver notifications from remote servers to mobile apps. We support both Android and iOS platforms and deal with two primary cloud messaging services :

- [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging) (FCM) - to send notifications to Android mobile app
- [Apple Push Notification Service](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html) (APNs) - to send notifications to iOS mobile app

#### Mobile App Integrated with Adobe Mobile SDK

Adobe Mobile SDK helps integrate your mobile apps with Adobe Experience Cloud Solutions like Experience Platform and Journey Optimizer. Mobile SDK is comprised of various Experience Cloud solution extensions to provide features specific to the service they represent. These extensions expose various [APIs](https://aep-sdks.gitbook.io/docs/beta/adobe-journey-optimizer/api-reference) to enable data flow like registering the push token or sending push tracking events or any other custom experience events to Adobe Experience Platform. 

Mobile SDK has now integrated with [Project Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon), which is a new, innovative beta product from Adobe Experience Cloud to help you inspect, proof, simulate, and validate how you collect data or serve experiences in your mobile app. With respect to push notifications, this integration helps validate various configurations across components involved in the data flow, by running a [test end-to-end push notification flow](https://aep-sdks.gitbook.io/docs/resources/troubleshooting-guides/troubleshooting-push). It shows errors encountered and recommendations to solve misconfigurations.

#### Adobe Launch

[Adobe Launch or Data Collection](https://experienceleague.adobe.com/docs/launch/using/home.html) is the next generation of mobile SDK management capabilities which enables data flow from mobile SDK to Experience Platform. It provides capabilities to register extensions, create rules and data elements to send data from your mobile app to the Adobe experience cloud solutions. With respect to the push notifications data flow, the primary configurations required in Launch are :

- Creating a datastream to configure the profile and experience event datasets against which the data flows into experience platform. 
- Creating a client-side mobile property and adding extensions. Mobile SDK closely integrates with these extensions to provide a seamless data collection experience.
- Registering the mobile app bundle identifier and app credentials that would help to uniquely identify and validate sanity of the app at the time of delivering push notification. 

You will find detailed steps for these configurations [here](https://aep-sdks.gitbook.io/docs/beta/adobe-journey-optimizer).

#### Real-time Customer Profile

[Real-time Customer Profile](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html) is the component in [Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html) that allows you to see a holistic view of each individual customer by combining data from multiple channels, including web, mobile, CRM, and third party. Profile allows you to consolidate your customer data into a unified view offering an actionable, timestamped account of every customer interaction. 

Static data that identifies the user of the mobile app such as a push token, is stored against the user's profile as record data while the interactions the user does with push notifications are tracked as time-series events data. 

#### Adobe Journey Optimizer

Once your mobile app integrations with above mentioned components are in place and your customer profiles are available as Real-time customer profiles, you can take advantage of powerful audience segmentation capabilities in [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) to ensure the optimal experience for each person.



### Push Data Flow Steps

Refer to the data flow diagram to identify what each of these bullets represent :

1. The customer develops a mobile app on Android or iOS that they would release to their users. In order to use the push capability provided by push providers i.e APNS by Apple and FCM by Google, the mobile app registers itself and enables the push capability.
2. The push providers generate and send a push token to the mobile app. A Push Token is an identifier that senders use to target specific devices with a push notification.
3. The mobile app is integrated with Adobe Mobile SDK which exposes various extensions and APIs. The Messaging extension exposes an API to register the push token into Adobe Experience Platform against customer's profile.
   Once the mobile app is ready, it is configured in Adobe Launch > App Configurations along with the credentials.
4. The marketer now authors a push notification in Adobe Journey Optimizer > Messages against the mobile app registered. 
5. The marketer orchestrates a customer journey defining the flow of events and actions. To send a push notification at a stage of the journey, the marketer adds an action of type 'Message' and associates it with the message authored in the previous step. 
6. Whenever a customer profile qualifies to receive the push notification for any reason say on trigger of an event or on qualification of a segment, the message is personalized against the profile, if applicable.
7. The personalized push message is sent for further processing to the Push delivery service.
8. The push delivery service validates the credentials of the app associated with the message.
9. The message is sent to the push providers for delivery to the mobile app against the specific push token and credentials.
10. The push providers send a feedback suggesting whether the message was successfully delivered to the provider or not. In case not, the relevant error message is part of the feedback. This feedback is sent to Adobe reporting for the customer to view in their Journey Live and Global Reports.
11. In the meantime, the push providers asynchronously deliver the successful push notification to the mobile app.
12. As the customer interacts with the notification, the impressions such as click/open can then be tracked as Experience Events. The Messaging extension exposes APIs to send tracking events into Adobe Experience Platform against customer's profile.



## Understanding Push User Flow

This diagram shows the various steps involved in configuring the components that form the skeleton of push data flow. The action items have been categorized based on the role performing the configuration and the component being configured. As you can see, before beginning to send push notifications with Journey Optimizer, you need to ensure configurations and integrations are in place on the mobile app, Launch and Experience Platform.

![Push User Flow](../../.gitbook/assets/push-user-flow.png)

