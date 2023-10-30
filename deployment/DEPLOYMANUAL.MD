# Android

## Android - Staging

1. `rm -rf android/app/build && rm -rf android/.gradle && rm -rf $HOME/.gradle; rm android/app/src/main/assets/index.android.bundle; npx react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res; cd android; ./gradlew clean; rm -rf app/src/main/res/drawable-*; rm -rf app/src/main/res/raw; ./gradlew assembleReleaseStaging`
2. `./gradlew bundleReleaseStaging`

## Android - Production

1. `rm -rf android/app/build && rm -rf android/.gradle && rm -rf $HOME/.gradle; rm android/app/src/main/assets/index.android.bundle; npx react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res; cd android; ./gradlew clean; rm -rf app/src/main/res/drawable-*; rm -rf app/src/main/res/raw; ./gradlew assembleRelease`
2. `./gradlew bundleRelease`
