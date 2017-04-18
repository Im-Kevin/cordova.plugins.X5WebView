
# cordova-plugin-x5WebView

该项目是参照https://github.com/offbye/cordova-plugin-x5engine-webview.git与Cordova 自带的WebView制作而成

改进了64位无法使用的问题

```
$ cordova plugin add cordova.plugins.x5webview
```

* Build
```
$ cordova build android
```

无需其他步骤,添加完毕就已经使用了腾讯浏览服务


验证方式可以调用window.navigator.userAgent

返回如下结果即代表成功

![alt text](/result.png "返回结果")
