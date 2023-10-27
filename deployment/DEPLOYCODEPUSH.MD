# Deployment Plan

## Staging Deployment

When the current Staging branch is ready for deployment, follow the steps below for both iOS and Android platforms:

1. **iOS Deployment**:
    ```bash
    appcenter codepush release-react -a Salonic/Salonic-iOS -d Staging -m
    ```

2. **Android Deployment**:
    ```bash
    appcenter codepush release-react -a Salonic/Salonic-Android -d Staging -m
    ```

## Production Deployment

### Preparing Release Notes

1. Collect all issues from the `Staging` column on the Kanban board.
2. Create a new section in the Release Notes file (`./RELEASE_NOTES.MD`) in the git repository, detailing the new version.

### Bumping the Version Number

1. Update the `CFBundleVersion` property in the `ios/salonicMobile/Info.plist` file with the new version number.
2. Update the `versionCode` property in the `android/app/build.gradle` file with the new version number.
3. Review the changes with the following command:
    ```bash
    git diff
    ```

4. Stage, commit, and push the version bump changes:
    ```bash
    git add -A; git commit -m "codepush major.minor.patch (versionCode)"; git push origin HEAD
    ```

5. Create a Pull Request from `staging` to `master` with the title `codepush major.minor.patch (versionCode)`, get it approved, and merge it.
6. Switch to the `master` branch and pull the latest changes:
    ```bash
    git checkout master; git pull
    ```

### Deploying to Production via Codepush

1. **iOS Deployment**:
    ```bash
    appcenter codepush release-react -a Salonic/Salonic-iOS -d Production -m
    ```

2. **Android Deployment**:
    ```bash
    appcenter codepush release-react -a Salonic/Salonic-Android -d Production -m
    ```
