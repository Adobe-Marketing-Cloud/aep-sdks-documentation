# Using Project Griffon

## Logging in

{% hint style="warning" %}
Project Griffon is in beta. To use Project Griffon, you must accept the terms outlined in [https://griffon.adobe.com](https://griffon.adobe.com).
{% endhint %}

1. Go to to [https://griffon.adobe.com](https://griffon.adobe.com).
2. Log in using your Adobe ID credentials for the Experience Cloud.

    {% hint style="info" %}
    If you do not know your Adobe ID credentials, contact your Adobe administrator or see [how to log in](https://docs.adobe.com/content/help/en/core-services/interface/manage-users-and-products/getting-started-experience-cloud.html).
    {% endhint %}

3. In the beta access page, click **Register**. 

## Project Griffon sessions

To begin a session, you need to create a session and connect your device.

### 1. Create a session

1. Log in to Project Griffon. 

2. Click **Create Session** in the top right. 

3. Click **Start**.

4. In **Session Name**, enter a name to identify the session.  
    This definition is used to launch your app from a URL and initiate the Project Griffon session. An example value might look like: `grifflab://default`.
e. In the **Base URL** field, type your app's base deep link definition.
5. Click **Next**.


### 2. Connect your device

1. Ensure that you see a screen that shows you a link, a QR code, and a PIN. 
2. Complete one of the following tasks:
   * Use your iOS Camera app to scan the QR code and to open your app.
   * Copy the link and open in your app or the Xcode simulator.
   
   ![](../../.gitbook/assets/image-3.png)

3. When your app launches, you should see the Project Griffon PIN entry screen overlaid. 
4. Type in the PIN from the previous step and press **Connect**.

   ![](../../.gitbook/assets/image-6.png)

5. Verify that your app is connected to Project Griffon when the red Experience Cloud icon is displayed on your app.

   ![](../../.gitbook/assets/image-8.png)

## Exporting a session

To export a Project Griffon session, on your app’s sessions details page, click **Export to JSON** in a session:

![](../../.gitbook/assets/screen-shot-2019-07-10-at-4.07.02-pm.png)

{% hint style="info" %}
This export operation maintains the search filter results and exports only the events displayed in the event view. For example, if you searched for “track” events and then click **Export to JSON**, only the “track” event results are exported.
{% endhint %}

