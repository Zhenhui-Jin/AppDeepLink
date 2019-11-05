# AppDeepLink

1、	拥有一个SSL通道的域名，如：https://zhenhui-jin.github.io

2、	创建一个名为“assetlinks.json”的JSON文件，内容为：
    [
      {
        "relation": ["delegate_permission/common.handle_all_urls"],
        "target": {
          "namespace": "android_app",
          "package_name": "调起的应用包名",
          "sha256_cert_fingerprints": ["keystore产生一个sha256指纹"]
        }
      }
    ]
    可打开https://developers.google.com/digital-asset-links/tools/generator进行生成内容。

3、	上传"assetlinks.json"文件到https://zhenhui-jin.github.io生成以下链接：
    https://zhenhui-jin.github.io/.well-known/assetlinks.json

4、	在app中处理深度链接：
    <activity
        android:name=""
        android:alwaysRetainTaskState="true"
        android:launchMode="singleTask"
        android:noHistory="true">
        <intent-filter android:autoVerify="true">
            <action android:name="android.intent.action.VIEW"/>
            <category android:name="android.intent.category.DEFAULT"/>
            <category android:name="android.intent.category.BROWSABLE"/>
            <data android:host="zhenhui-jin.github.io" android:scheme="https"/>
        </intent-filter>
    </activity>
    注意：必须添加android:autoVerify="true"，host对应的域名都需要上传"assetlinks.json"文件，否则会认证失败

5、	添加网络权限：
    <uses-permission android:name="android.permission.INTERNET"/>

6、	参考：
    http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2015/0609/3022.html
    https://segmentfault.com/a/1190000011169174
