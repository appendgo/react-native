# Android

1. `rm -rf android/app/build && rm -rf android/.gradle && rm -rf $HOME/.gradle`
2. `rm android/app/src/main/assets/index.android.bundle`
3. `npx react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res`
4. `cd android`
5. `./gradlew clean`
6. `rm -rf app/src/main/res/drawable-*`
7. `rm -rf app/src/main/res/raw`
8. `./gradlew assembleRelease`

* `rm -rf android/app/build && rm -rf android/.gradle && rm -rf $HOME/.gradle; rm android/app/src/main/assets/index.android.bundle; npx react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res; cd android; ./gradlew clean; rm -rf app/src/main/res/drawable-*; rm -rf app/src/main/res/raw; ./gradlew assembleRelease`
