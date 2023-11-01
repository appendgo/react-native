# Install

* `yarn add react-native-config`
* `cd ios && pod install && cd ..`

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

# Android Setup

* to `android/app/build.gradle` add this

```
apply plugin: "com.android.application"

// these below
apply from: project(':react-native-config').projectDir.getPath() + '/dotenv.gradle'

project.ext.envConfigFiles = [
        development: ".env.development",
        staging :".env.staging",
        production:'.env.production'
]
```

* also add resValue in default config

```
android {
...
    namespace 'com.reactnativesetup'
    defaultConfig {
        ...
        resValue 'string', 'build_config_package','com.x.y.' // <---- Add this line
    }
...
}
```





