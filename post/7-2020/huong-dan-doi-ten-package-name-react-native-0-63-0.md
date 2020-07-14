<h1 style="text-align: center"> Hướng dẫn đổi tên package name React Native 0.63.0 </h1>

---

Mình mới được tiếp xúc với React Native cách đây không lâu, cũng tập tành làm cái app be bé để "Hello world". Thêm plugin, code phần logic, thả thính thêm chút giao diện. Mọi thứ đều ổn trừ 1 thứ: tên app hiển thị ngoài màn hình chính và package name của app. Mặc định khi khởi tạo project với react-native init TenProjectNay sẽ là:

1. Package name: com.TenProjectNay
2. Tên app ngoài màn hình chính: TenProjectNay
   
Trông rất là khó chịu :((, không có tuỳ chọn khi khởi tạo project mà luôn là mặc định. Mình tốn kha khá thời gian lội google, stackoverflow, dev.to và cả medium cuối cùng cũng tìm đc bài này: [Quick guide for updating package name in React Native](https://dev.to/karanpratapsingh/quick-guide-for-updating-package-name-in-react-native-3ei3) Mừng rớt nước mẳt.

Nhân dịp React native ra mắt bản cập nhật 0.63.0, mình viết bài này tiện cho các bạn tìm kiếm đơn giản hơn sau này. 

Để sửa package name không bị lỗi, các bạn nên khởi tạo 1 project mới, sửa package name sau đó mới lắp code của mình vào để đảm bảo project clear nhất có thể. Có 3 biến cần lưu ý khi sửa: 

1. **APPLICATION_NAME** : cái này được react-native định danh ứng dụng của bạn
2. **APPLICATION_DISPLAY_NAME** : đây là tên được hiển thị ở màn hình chính
3. **ANDROID_PACKAGE_NAME** : không cần giải thích nhiều, android package name :DDD




## /app.json

``` json
{
  "name": "APPLICATION_NAME",
  "displayName": "APPLICATION_DISPLAY_NAME"
}

```
<br>

## /package.json

``` json
{
  "name": "APPLICATION_NAME",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "android": "react-native run-android",
    "ios": "react-native run-ios",
    "start": "react-native start",
    "test": "jest",
    "lint": "eslint ."
  },
  "dependencies": {
    "react": "16.13.1",
    "react-native": "0.63.0"
  }
}
```
 <br>

## /android/settings.gradle

``` json
rootProject.name = 'HUBTHub'
apply from: file("../node_modules/@react-native-community/cli-platform-android/native_modules.gradle"); applyNativeModulesSettingsGradle(settings)
include ':app'
```
<br>

## /android/app/_BUCK

``` json
android_build_config(
    name = "build_config",
    package = "ANDROID_PACKAGE_NAME",
)

android_resource(
    name = "res",
    package = "ANDROID_PACKAGE_NAME",
    res = "src/main/res",
)
```
<br>

## /android/app/build.gradle

``` json

android {
    compileSdkVersion rootProject.ext.compileSdkVersion

    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }

    defaultConfig {
        applicationId "ANDROID_PACKAGE_NAME"
        minSdkVersion rootProject.ext.minSdkVersion
        targetSdkVersion rootProject.ext.targetSdkVersion
        versionCode 1
        versionName "1.0"
    }

```
<br>


## /android/app/src/main/AndroidManifest.xml
``` xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
  package="ANDROID_PACKAGE_NAME">
```
<br>


## /android/app/src/main/java/MainActivity.java
``` java
package ANDROID_PACKAGE_NAME;

import com.facebook.react.ReactActivity;

public class MainActivity extends ReactActivity {

  /**
   * Returns the name of the main component registered from JavaScript. This is used to schedule
   * rendering of the component.
   */
  @Override
  protected String getMainComponentName() {
    return "APPLICATION_NAME";
  }
}
```
<br>



## /android/app/src/main/java/MainApplication.java
``` java
package ANDROID_PACKAGE_NAME;

import android.app.Application;
import android.content.Context;
```

``` java
  private static void initializeFlipper(
      Context context, ReactInstanceManager reactInstanceManager) {
    if (BuildConfig.DEBUG) {
      try {
        /*
         We use reflection here to pick up the class that initializes Flipper,
        since Flipper library is not available in release mode
        */
        Class<?> aClass = Class.forName("ANDROID_PACKAGE_NAME.ReactNativeFlipper");
        aClass
            .getMethod("initializeFlipper", Context.class, ReactInstanceManager.class)
            .invoke(null, context, reactInstanceManager);
      } catch (ClassNotFoundException e) {
        e.printStackTrace();
      } catch (NoSuchMethodException e) {
        e.printStackTrace();
      } catch (IllegalAccessException e) {
        e.printStackTrace();
      } catch (InvocationTargetException e) {
        e.printStackTrace();
      }
    }
  }
```

<br>

## /android/app/src/main/res/values/strings.xml
``` xml
<resources>
    <string name="app_name">APPLICATION_DISPLAY_NAME</string>
</resources>
```



## /android/app/src/debug/java/com/APPLICATION_NAME/ReactNativeFlipper.java
``` java
/**
 * Copyright (c) Facebook, Inc. and its affiliates.
 *
 * <p>This source code is licensed under the MIT license found in the LICENSE file in the root
 * directory of this source tree.
 */
package ANDROID_PACKAGE_NAME;
```



Bài tới đây là hết rồi, nếu có cập nhật thay đổi gì các bạn cứ để lại comment ở dưới để mình cập nhật nha. 

Thanks for reading.
Have a nice day <3