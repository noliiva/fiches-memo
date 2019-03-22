## Useful commands
### test deeplink
* iOS: `xcrun simctl openurl booted myapp://`
* android: `adb shell am start -W -a android.intent.action.VIEW -d "myapp://" my.app`

## Tips
### iOS
If app don't want to build and display strange message like *main.jsbundle not found*, it should be because your react app did build properly. You can try to run `react-native bundle --platform ios --entry-file ./index.js --bundle-output ios/main.jsbundle` to get better error message.
