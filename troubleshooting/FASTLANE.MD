# Install

* `brew install imagemagick`
* `brew install fastlane`
* `cd ios && fastlane add_plugin appicon && cd ..`
* `cd android && fastlane add_plugin appicon && cd ..`

# Usage

## iOS staging

* `cd ios`
* `FASTLANE_USER=<APPLE_ID> FASTLANE_APPLE_APPLICATION_SPECIFIC_PASSWORD=<PASSWORD> fastlane ios staging`

## iOS release

* `...`

## Android staging

* `cd android`
* `fastlane android staging`

## Android release

* `...`

# iOS setup

## App-Specific Password

* Go to `https://appleid.apple.com/account/manage`
* Create an `App-Specific Passwords`
* http://docs.fastlane.tools/getting-started/ios/authentication/#method-3-application-specific-passwords

## Init

* `cd ios`
* `fastlane init`

## 

# Android setup

## Service Account -> Download Json Key

* https://docs.fastlane.tools/actions/supply/#setup
* Validate
  * `fastlane run validate_play_store_json_key json_key:path/to/play-store-credentials.json`
* Enable `Google Play Android Developer API`
  * https://console.cloud.google.com/apis/library/androidpublisher.googleapis.com
* Add  `client_email` to Google Play Console  -> Setup -> API Access with Admin access
  * get `client_email` from your `play-store-credentials.json`

## Init

* `cd android`
* `fastlane init`
