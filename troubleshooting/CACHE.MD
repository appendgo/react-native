# iOS

## Complete cleanup (pod reset)

```
rm -rf ~/Library/Caches/CocoaPods
rm -rf Pods
rm -rf ~/Library/Developer/Xcode/DerivedData/*
pod deintegrate
pod setup
pod install
```

## Clean all cached CocoaPods

```
pod cache clean --all
```

## Clean CocoaPods cache, re-download and re-install all pods

```
rm -rf "${HOME}/Library/Caches/CocoaPods"
rm -rf "`pwd`/Pods/"
pod update
```

# Android

## Clean project build outputs

```
./gradlew clean
```

## Cleaning the Build Cache
```
./gradlew cleanBuildCache
```
