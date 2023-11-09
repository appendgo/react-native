# Cache

## iOS

### Complete cleanup (pod reset)

```
rm -rf ~/Library/Caches/CocoaPods
rm -rf ~/Library/Developer/Xcode/DerivedData/*
cd ios
rm -rf Pods
pod deintegrate
pod setup
pod install
```

### Clean all cached CocoaPods

```
pod cache clean --all
```

### Clean CocoaPods cache, re-download and re-install all pods

```
rm -rf "${HOME}/Library/Caches/CocoaPods"
cd ios
rm -rf Pods
pod update
```

## Android

### Clean project build outputs

```
./gradlew clean
```

### Cleaning the Build Cache
```
./gradlew cleanBuildCache
```
