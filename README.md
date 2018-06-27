# rncamera

working version with android (react-native-camera example)

  ```
  "dependencies": {
    "react": "16.3.1",
    "react-native": "0.55.4",
    "react-native-camera": "^1.1.4"
  }
  ```

step1:
```
yarn add react-native-camera
react-native link react-native-camera
```

step2: AndroidManifest.xml

```
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.RECORD_AUDIO"/>
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

step3: android/app/build.gradle

```
compileSdkVersion 27
buildToolsVersion "27.0.3"
...
defaultConfig {
  ...
}

...

dependencies {
    compile project(':react-native-camera')
    compile fileTree(dir: "libs", include: ["*.jar"])
    compile "com.android.support:appcompat-v7:27.1.0"
    compile "com.facebook.react:react-native:+"  // From node_modules
}
```

step4: android/build.gradle

```
buildscript {
    repositories {
        jcenter()
        google()
        maven { url 'https://maven.google.com' }
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.1.0'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}
allprojects {
    repositories {
        mavenLocal()
        jcenter()
        maven {
            // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm
            url "$rootDir/../node_modules/react-native/android"
        }
        maven {
            url "https://maven.google.com" // Google's Maven repository
        }
        maven { url "https://jitpack.io" }
    }
}
ext {
    compileSdkVersion = 27
    buildToolsVersion = '27.0.3'
}

subprojects { subproject ->
    afterEvaluate{
        if((subproject.plugins.hasPlugin('android') || subproject.plugins.hasPlugin('android-library'))) {
            android {
                compileSdkVersion rootProject.ext.compileSdkVersion
                buildToolsVersion rootProject.ext.buildToolsVersion
            }
        }
    }
}
```

step5: android/gradle/wrapper/gradle-wrapper.properties

```
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-4.4-all.zip
```