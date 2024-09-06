* `yarn install --frozen-lockfile`
* `cd ios`
* `bundle install`
* `sudo xcode-select --switch /Applications/Xcode.app`
* `bundle exec pod install`
* `cd ..`

### iOS

* `npx react-native run-ios --simulator="iPhone 12 mini"`

### Android

* `npx react-native run-android`

## Possible errors

### Error with react-native-fingerprint-scanner
* Error message: Could not find com.wei.android.lib:fingerprintidentify:1.2.6.
* `-> node_modules/react-native-fingerprint-scanner/android/build.gradle`
* replace this code: `"com.wei.android.lib:fingerprintidentify:${safeExtGet("fingerprintidentify", "1.2.6")}"` with this code: `"com.github.uccmawei:FingerprintIdentify:1.2.6"`

### No connected devices error (in case of Android)
* `-> Android Studio terminal`
* run the emulator with: `emulator -avd <avd_name>`

### Error with FlipperPlatformWebSocket (in case of iOS)
* `-> ios/Podfile`
* comment out this line: `:flipper_configuration => FlipperConfiguration.enabled`
* `bundle exec pod install`

### Error with main.jsbundle
* Error message: ios/main.jsbundle : No such file or directory
* in case of iOS: `npx react-native bundle --platform ios --dev false --entry-file index.js --bundle-output ios/main.jsbundle --assets-dest ios`
* in case of android: `npx react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res`
