# Install

* `brew install imagemagick`
* `brew install fastlane`
* `cd ios && fastlane add_plugin appicon && cd ..`
* `cd android && fastlane add_plugin appicon && cd ..`

### Android - How to use Internal App Sharing

(How to Enable Developer Options in the Play Store)

Follow these steps to access developer options in the Google Play Store:

* Steps
  * Step 1: Open the Play Store
    * Start by launching the **Play Store** app on your device.
  * Step 2: Access Settings
    * Navigate to the settings by clicking on your **account profile picture**, which is located at the top right corner of the screen.
  * Step 3: Enable Developer Options
    * Go to the **About section** of the settings.
    * Tap **seven times** on the *Play Store Version*. This is a common easter egg in Android systems to unlock developer options.
  * Step 4: Developer Status Confirmation
    * After the seventh tap, you should see a prompt saying **“You are now a developer!”**. Post this, the **“Internal App Sharing”** option will become visible to you in the **General -> User Controls** section.

# iOS setup

## App-Specific Password

* Go to `https://appleid.apple.com/account/manage`
* Create an `App-Specific Passwords`
* http://docs.fastlane.tools/getting-started/ios/authentication/#method-3-application-specific-passwords

## Init

* `cd ios`
* `fastlane init`

## Appfile

```
app_identifier("com.your.project") # The bundle identifier of your app
#apple_id(ENV['FASTLANE_USER']) # Your Apple Developer Portal username

itc_team_id("122564699") # App Store Connect Team ID
team_id("96H4HCU6TD") # Developer Portal Team ID

# For more information about the Appfile, see:
#     https://docs.fastlane.tools/advanced/#appfile
```

## Fastfile

```
default_platform(:ios)

platform :ios do
  desc "Bump version"
  lane :bumpversion do
    ensure_git_branch(branch: 'staging')
    ensure_git_status_clean
    git_pull

    new_version_number = get_version_number(xcodeproj: "BillingoMobile.xcodeproj")
    new_build_number = increment_build_number(xcodeproj: "BillingoMobile.xcodeproj")

    if ENV['BUMP_TYPE']
      new_version_number = increment_version_number(
        xcodeproj: "BillingoMobile.xcodeproj",
        bump_type: ENV['BUMP_TYPE'] # Can be "patch", "minor", or "major"
      )
    end

    # Output the new version and build numbers
    puts "New Version Number: #{new_version_number}"
    puts "New Build Number: #{new_build_number}"

    # Read version.js
    version_js_path = '../../version.js'
    version_js_content = File.read(version_js_path)

    # Update version and versionCode
    version_js_content.gsub!(/version: '\d+\.\d+\.\d+'/, "version: '#{new_version_number}'") unless new_version_number.nil?
    version_js_content.gsub!(/versionCode: '\d+'/, "versionCode: '#{new_build_number}'")

    # Write the changes back to version.js
    File.open(version_js_path, "w") { |file| file.puts version_js_content }

    sh "git add #{version_js_path}"

    commit_version_bump(
      message: "Bump build to version #{new_version_number} (#{new_build_number})",
      xcodeproj: 'BillingoMobile.xcodeproj',
      include: ['version.js']
    )

    push_to_git_remote
  end

  desc "Push a new staging build to TestFlight"
  lane :staging do
    ensure_git_branch(
      branch: 'staging'
    )
    ensure_git_status_clean
    git_pull
    clear_derived_data
    clean_build_artifacts
    appicon(
      appicon_image_file: './appiconstaging.png',
      appicon_devices: [:iphone, :ipad, :ios_marketing],
      appicon_path: './BillingoMobile/Images.xcassets'
    )
    build_app(workspace: "BillingoMobile.xcworkspace", scheme: "BillingoMobile staging")
    upload_to_testflight
    appicon(
      appicon_image_file: './appiconrelease.png',
      appicon_devices: [:iphone, :ipad, :ios_marketing],
      appicon_path: './BillingoMobile/Images.xcassets'
    )
  end

  desc "Push a new release build to TestFlight"
  lane :release do
    ensure_git_branch(
      branch: 'master'
    )
    ensure_git_status_clean
    git_pull
    clear_derived_data
    clean_build_artifacts
    build_app(workspace: "BillingoMobile.xcworkspace", scheme: "BillingoMobile")
    upload_to_testflight
  end
end
```

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

## Appfile

```
json_key_file("./fastlane/play-store-credentials.json") # Path to the json secret file - Follow https://docs.fastlane.tools/actions/supply/#setup to get one
package_name("com.your.project") # e.g. com.krausefx.app
```

## Fastfile

```
default_platform(:android)

platform :android do
  desc "Bump version"
  lane :bumpversion do
    ensure_git_branch(
      branch: 'staging'
    )
    ensure_git_status_clean
    git_pull
    if ENV['BUMP_TYPE']
      increment_versions
    else
      increment_version_code
    end
    sh("git add -A")
    sh("git commit -m 'Bump version'") 
    push_to_git_remote
  end

  desc "Push a new staging build to Play Store :: In App Share"
  lane :staging do
    ensure_git_branch(
      branch: 'staging'
    )
    ensure_git_status_clean
    git_pull
    gradle(task: 'clean', project_dir: './')
    set_appicon_to_staging
    gradle(
      task: 'bundle',
      build_type: 'ReleaseStaging'
    )
    download_url = upload_to_play_store_internal_app_sharing(
      aab: './app/build/outputs/bundle/releaseStaging/app-releaseStaging.aab',
      package_name: 'com.billingo.mobile'
    )
    set_appicon_to_release
    UI.message("---------------------------------------")
    UI.message("======> Download URL: #{download_url}")
    UI.message("---------------------------------------")
  end

  desc "Push a new release build to Play Store :: Internal Test"
  lane :release do
    ensure_git_branch(
      branch: 'master'
    )
    ensure_git_status_clean
    git_pull
    gradle(task: 'clean', project_dir: './')
    gradle(
      task: 'bundle',
      build_type: 'Release'
    )
    supply(
      track: 'internal',
      aab: './app/build/outputs/bundle/release/app-release.aab',
      package_name: 'com.billingo.mobile'
    )
  end

  private_lane :increment_version_code do
    gradle_file_path = "../app/build.gradle"
    gradle_file = File.read(gradle_file_path)
    new_version_code = gradle_file.match(/versionCode (\d+)/)[1].to_i + 1
    updated_gradle_file = gradle_file.sub(/versionCode (\d+)/, "versionCode #{new_version_code}")
    File.open(gradle_file_path, "w") { |file| file.puts updated_gradle_file }
  end

  private_lane :increment_versions do
    gradle_file_path = "../app/build.gradle"
    gradle_file = File.read(gradle_file_path)
  
    # Increment versionCode
    new_version_code = gradle_file.match(/versionCode (\d+)/)[1].to_i + 1
    updated_gradle_file = gradle_file.sub(/versionCode (\d+)/, "versionCode #{new_version_code}")
  
    # Increment versionName
    version_name_match = gradle_file.match(/versionName "(\d+)\.(\d+)\.(\d+)"/)
    major, minor, patch = version_name_match.captures.map(&:to_i)
  
    bump_type = ENV['BUMP_TYPE']
    case bump_type
    when 'major'
      major += 1
      minor = 0
      patch = 0
    when 'minor'
      minor += 1
      patch = 0
    else  # default to 'patch' if BUMP_TYPE is not set or unrecognized
      patch += 1
    end
  
    new_version_name = "#{major}.#{minor}.#{patch}"
    updated_gradle_file = updated_gradle_file.sub(/versionName "(\d+)\.(\d+)\.(\d+)"/, "versionName \"#{new_version_name}\"")
  
    # Write updated gradle file
    File.open(gradle_file_path, "w") { |file| file.puts updated_gradle_file }
  end
  

  private_lane :set_appicon_to_staging do
    Dir.glob("../staging_ic_launcher/**/*").each do |icon_file|
      next if File.directory?(icon_file)
      target_file = icon_file.sub("../staging_ic_launcher/res/", "../app/src/main/res/")
      FileUtils.cp(icon_file, target_file)
    end
  end

  private_lane :set_appicon_to_release do
    Dir.glob("../release_ic_launcher/**/*").each do |icon_file|
      next if File.directory?(icon_file)
      target_file = icon_file.sub("../release_ic_launcher/res/", "../app/src/main/res/")
      FileUtils.cp(icon_file, target_file)
    end
  end
end
```
