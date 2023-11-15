# Installation / Android

## OpenJDK

* `brew tap homebrew/cask-versions`
* `brew install --cask zulu11`
* `java --version`

## Android Studio

### Download Android Studio

* Download Android Studio from [https://developer.android.com/studio](https://developer.android.com/studio)
* Standard install

### Open an existing Project in Android Studio

* `-> Open a project or a file`
* Select the Repostitory/Project's `android` directory
  * It's on the root level

### SDK Manager

* `-> Tools / SDK Manager`
* Install 31,32,33,34... API levels

### Simulator

* `-> Tools / Device Manager`
* Here you can create a new Android Device Simulator

## Environment variables

* Add the following lines to your ~/.zprofile or ~/.zshrc (if you are using bash, then ~/.bash_profile or ~/.bashrc) config file:

```
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/platform-tools
```

## Check

* `emulator -list-avds`
