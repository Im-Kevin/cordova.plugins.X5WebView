
# cordova-plugin-x5WebView

该项目是参照https://github.com/offbye/cordova-plugin-x5engine-webview.git与Cordova 自带的WebView制作而成

```
$ cordova plugin add  https://github.com/Im-Kevin/cordova.plugins.X5WebView.git
```

* Build
```
$ cordova build android
```

* Android 64无法使用腾讯浏览服务的解决方案
* 找到platforms\android\build.gradle里面的
```gradle
android {
    ...
    defaultConfig {
        versionCode cdvVersionCode ?: new BigInteger("" + privateHelpers.extractIntFromManifest("versionCode"))
        applicationId privateHelpers.extractStringFromManifest("package")

        if (cdvMinSdkVersion != null) {
            minSdkVersion cdvMinSdkVersion
        }
        
        在此处添加
        ndk {
          abiFilters"armeabi","armeabi-v7a","x86"
        }
        ...
   }
   ...
}
```

