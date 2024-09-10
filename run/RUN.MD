### Install packages

* *(`rm -rf node_modules`)*
* *(`yarn cache clean --all`)*
* `yarn install --frozen-lockfile`
* `cd ios`
* *(`rm -rf Pods`)*
* `bundle install`
* `bundle exec pod install`
* `cd ..`

### Generate bundle

* iOS
  * `npx react-native bundle --platform ios --dev false --entry-file index.js --bundle-output ios/main.jsbundle --assets-dest ios`
* Android
  * `npx react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res`

### Run iOS

* `npx react-native run-ios --simulator="iPhone 12 mini"`

### Run Android

* `-> Android Studio terminal`
* run the emulator with: `emulator -avd <avd_name>`
* in project root terminal: `npx react-native run-android`

## Possible errors

### Error with react-native-fingerprint-scanner
* Error message: Could not find com.wei.android.lib:fingerprintidentify:1.2.6.
* `-> node_modules/react-native-fingerprint-scanner/android/build.gradle`
* replace this code: `"com.wei.android.lib:fingerprintidentify:${safeExtGet("fingerprintidentify", "1.2.6")}"`
with this code: `"com.github.uccmawei:FingerprintIdentify:1.2.6"`

### Error with FlipperPlatformWebSocket (in case of iOS)
* `-> ios/Podfile`
* comment out this line: `:flipper_configuration => FlipperConfiguration.enabled`
* `cd ios`
* `bundle exec pod install`
