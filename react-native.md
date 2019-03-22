## Useful commands
### test deeplink
* iOS: `xcrun simctl openurl booted myapp://`
* android: `adb shell am start -W -a android.intent.action.VIEW -d "myapp://" my.app`

## Tips
### iOS
#### main.jsbundle does not exist. This must be a bug with
If app don't want to build and display this strange message, it could be because your react app did build properly. You can try to run the following command to get a better error message :

`react-native bundle --platform ios --entry-file ./index.js --bundle-output ios/main.jsbundle`
