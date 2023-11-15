# CodePush with Fastlane

# Staging

## 1. iOS

```
appcenter codepush release-react -a Billingo/Billingo-iOS -d Staging -m
```

## 2. Android

```
appcenter codepush release-react -a Billingo/Billingo-Android -d Staging -m
```

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

## 3. Create PR `master` <-- `staging`

* e.g. `release 1.80.0 (200)`

## 4. iOS

```
appcenter codepush release-react -a Billingo/Billingo-iOS -d Production -m --rollout 25
```

## 5. Android

```
appcenter codepush release-react -a Billingo/Billingo-Android -d Production -m --rollout 25
```
