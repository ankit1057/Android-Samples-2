Custom Referrer Receiver
------------------------

### Problem

We want to pre-configure some elements of our app based on an installation link the user clicked (i.e. from a website).

### Example

Alice installs our news-reader app from website X. The news-feed of website X will be automatically added to the app after installation. 

### Solution

This project shows how to add an optional parameter to the Android referrer URL. We will parse the referrer sent to our app by the Google Play Store upon an installation, read our optional parameter to pre-configure the app, and forward the referrer to Google Analytics for further tracking.

Example of URLs to use for redirecting our users to the Google Play Store:

	https://play.google.com/store/apps/details?id=com.example.android&referrer=utm_source%3DYourAppName%26utm_medium%3DYourMedium%26utm_campaign%3DYourCampaign%26utm_content%3DYourSampleContent

	market://details??id=com.example.android&referrer=utm_source%3DYourAppName%26utm_medium%3DYourMedium%26utm_campaign%3DYourCampaign%26utm_content%3DYourSampleContent

**Note**: we are using the optional parameter "utm_content" to add our payload.

### Test

To test the Intent sent to our app by the Google Play Store, please do the following from a console:

1) Open the ADB shell:

	adb shell

2) Send the broadcast to our app:

	am broadcast -a com.android.vending.INSTALL_REFERRER -n com.example.android.custom.referrer.receiver/.ReferrerReceiver --es "referrer" "utm_source=YourAppName&utm_medium=YourMedium&utm_campaign=YourCampaign&utm_content=YourSampleContent"

**Note**: replace "YourSampleContent" with some more meaningful value for your app, like the ID of a product, plugin, etc. You can use this value in the class "ReferrerReceiver" to pre-configure the app as needed.