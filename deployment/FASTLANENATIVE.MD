# Native build with Fastlane

# Staging

## 1. Bump minor version

```
cd ios && BUMP_TYPE=minor fastlane ios bumpversion && cd .. && cd android && BUMP_TYPE=minor fastlane android bumpversion && cd ..
```

## 2. Check changed versions

```
git log -p
```

## 3. iOS

```
cd ios && FASTLANE_USER=... FASTLANE_APPLE_APPLICATION_SPECIFIC_PASSWORD=... fastlane ios staging
```

## 4. Android

```
cd android && fastlane android staging
```

## 5. Share Android link

* here: ...

---
---
---

# Release

## 1. Release notes

* Kanban board: Gather issues from `Staging` column
* ...

## 2. Bump version in Staging

```
cd ios && fastlane ios bumpversion && cd .. && cd android && fastlane android bumpversion && cd ..
```

## 3. Check changed versions

```
git log -p
```

## 4. Create PR `master` <-- `staging`

* e.g. `release 1.80.0 (200)`

## 5. iOS

```
cd ios && FASTLANE_USER=... FASTLANE_APPLE_APPLICATION_SPECIFIC_PASSWORD=... fastlane ios release
```

## 6. Android

```
cd android && fastlane android release
```

## 7. Testing is done

Send the appps to App store and Marketplace for reviews!
