# iOS Installation for React Native

## Ruby

```
brew install ruby@3.0
ruby --version
```

## Cocoapods

- Uninstall existing Cocoapods version (if needed):
```
sudo gem uninstall cocoapods -v 1.11.2
```

- Install specific version of Cocoapods:
```
sudo gem install cocoapods -v 1.11.3
pod --version
```

## Xcode
- Install Xcode from the App Store.
- Launch Xcode and configure:
1. Open Xcode.
2. Go to Settings.
3. Navigate to Locations.
4. Ensure a dropdown option is selected for command line tools: `sudo xcode-select --switch /Applications/Xcode.app`


## Open Project in Xcode
- Navigate to `Open a project or a file`.
- Select the repository/project's `ios` directory, located at the root level.

## How to Downgrade an Xcode Version
- Example: Downgrading from Xcode 14.3 to Xcode 14.2.
1. Download the required version from [Apple Developer Downloads](https://developer.apple.com/download/more).
2. Extract the downloaded file:
   ```
   sudo xip -x /tmp/Xcode2.xip
   ```
3. Switch to the extracted Xcode version:
   ```
   sudo xcode-select --switch /Applications/Xcode2.app
   ```
4. Verify the version:
   ```
   /usr/bin/xcodebuild -version
   ```
