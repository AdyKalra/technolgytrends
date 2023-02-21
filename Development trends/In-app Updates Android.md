## In-app updates

* When your users keep your app up to date on their devices, they can try new features, as well as benefit from performance improvements and bug fixes. Although some users enable background updates when their device is connected to an unmetered connection, other users might need to be reminded to install updates. In-app updates is a Google Play Core libraries feature that prompts active users to update your app.

* The in-app updates feature is supported on devices running Android 5.0 (API level 21) or higher. Additionally, in-app updates are only supported for Android mobile devices, Android tablets, and Chrome OS devices. 
* Note: In-app updates are not compatible with apps that use APK expansion files (.obb files).

* There are two signals that can start the update:

### Priority: 
You specify the update’s importance in each release by providing an integer that ranges from 0 to 5. (5 being the highest priority). In order to update the app, this will start the appropriate update flow (Immediate or Flexible).
#### Staleness: 
Specifies the amount of time the device has been aware that an update is available. This aids in setting off the appropriate flow. For instance, the Flexible flow would be triggered if the user hadn’t updated the app in the previous 30 days following the release of the update, and the Immediate flow would be triggered if it had been longer than 90 days.
For a better user experience, you may also combine the two signals.

