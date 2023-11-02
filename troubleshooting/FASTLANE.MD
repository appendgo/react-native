# Install

* `brew install imagemagick`
* `brew install fastlane`
* `cd ios && fastlane add_plugin appicon && cd ..`

# iOS setup

* Go to `https://appleid.apple.com/account/manage`
* Create an `App-Specific Passwords`

# Usage

## iOS staging

* `FASTLANE_USER=<APPLE_ID> FASTLANE_APPLE_APPLICATION_SPECIFIC_PASSWORD=<PASSWORD> fastlane ios staging`

## iOS release

* `...`

## Android staging

* `...`

## Android release

* `...`
