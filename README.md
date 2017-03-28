
# cordova-plugin-x5WebView

该项目是参照https://github.com/offbye/cordova-plugin-x5engine-webview.git与Cordova 自带的WebView制作而成

```
$ cordova plugin add  https://github.com/Im-Kevin/cordova.plugins.X5WebView.git
```

* Build
```
$ cordova build android
```

* 找到platforms\android\src\ + 包名 + \MainActivity.java
将

```java
        @Override
        public void onCreate(Bundle savedInstanceState)
        {
            super.onCreate(savedInstanceState);
    
            // enable Cordova apps to be started in the background
            Bundle extras = getIntent().getExtras();
            if (extras != null && extras.getBoolean("cdvStartInBackground", false)) {
                moveTaskToBack(true);
            }
   
            // Set by <content src="index.html" /> in config.xml
            loadUrl(launchUrl);
        }
```

修改为

```java
     @Override
      public void onCreate(Bundle savedInstanceState)
        {
            super.onCreate(savedInstanceState);
    
            // enable Cordova apps to be started in the background
            Bundle extras = getIntent().getExtras();
            if (extras != null && extras.getBoolean("cdvStartInBackground", false)) {
                moveTaskToBack(true);
            }
    
          //搜集本地tbs内核信息并上报服务器，服务器返回结果决定使用哪个内核。
          //TbsDownloader.needDownload(getApplicationContext(), false);
    
          QbSdk.PreInitCallback cb = new QbSdk.PreInitCallback() {
    
            @Override
            public void onViewInitFinished(boolean arg0) {
              // TODO Auto-generated method stub
              Log.e("app", " onViewInitFinished is " + arg0);
            }
    
            @Override
            public void onCoreInitFinished() {
              // TODO Auto-generated method stub
    
            }
          };
          QbSdk.setTbsListener(new TbsListener() {
            @Override
            public void onDownloadFinish(int i) {
              Log.d("app","onDownloadFinish is " + i);
            }
    
            @Override
            public void onInstallFinish(int i) {
              Log.d("app","onInstallFinish is " + i);
            }
    
            @Override
            public void onDownloadProgress(int i) {
              Log.d("app","onDownloadProgress:"+i);
            }
          });
    
          QbSdk.initX5Environment(getApplicationContext(),  cb);
            // Set by <content src="index.html" /> in config.xml
            loadUrl(launchUrl);
       }

```

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

