# Install

* `yarn add react-native-config`
* `cd ios && pod install && cd ..`
* to `android/app/build.gradle` add this

```
apply plugin: "com.android.application"
apply from: project(':react-native-config').projectDir.getPath() + "/dotenv.gradle" // <- add this line
```

# Create .env files for each configuration

* `.env.development`

```
ENV=development
```

* `.env.staging`

```
ENV=staging
```

* `.env.production`

```
ENV=production
```



