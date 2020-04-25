OpenCV4Android
======

[ ![Download](https://api.bintray.com/packages/wanghonglin/maven/opencv-with-header/images/download.svg) ](https://bintray.com/wanghonglin/maven/opencv-with-header/_latestVersion)

This project is created from [opencv](https://github.com/opencv/opencv), with the helper script from [eclipse2as.sh](https://github.com/WanghongLin/miscellaneous/blob/master/tools/eclipse2as.sh)

Use OpenCV in your Android studio project
-----------------------------------------

##### Add native bundle plugin to your project `build.gradle`
```groovy
buildscript {
    //...
    dependencies {
        //...
        classpath 'com.ydq.android.gradle.build.tool:nativeBundle:1.0.4'
        //...
    }
}
```

#### Use and apply plugin in your app `build.gradle`
```groovy
apply plugin: 'com.android.application'
apply plugin: 'com.ydq.android.gradle.native-aar.import'
```

##### Use the published version from jCenter
```groovy
dependencies {
    //...
    implementation 'com.wanghong.opencv:opencv-with-header:3.1.1-dev'
    //...
}
```

##### Use this library and start develop your OpenCV app
* Create a reference in your `CMakeLists.txt` if you use `cmake` build system

```cmake
include (${ANDROID_GRADLE_NATIVE_BUNDLE_PLUGIN_MK})
target_link_libraries(native-lib ${ANDROID_GRADLE_NATIVE_MODULES})
```
Check the information from [here](https://github.com/howardpang/androidNativeBundle) if you use other build system

* Verify in your code
```cpp
#include <jni.h>
#include <string>
#include <opencv/cv.h>

extern "C" JNIEXPORT jstring JNICALL
Java_com_example_myapp_MainActivity_stringFromJNI(
        JNIEnv* env,
        jobject /* this */) {
    std::string hello = "Hello from C++" + cv::getBuildInformation();
    return env->NewStringUTF(hello.c_str());
}
```

* Enjoy!

Troubleshoot
------------
* `gnustl_static` has been removed started from ndk r18, so make sure you use ndk version before r18 release.

Reference
---------
* Many thanks to this [header bundle plugin](https://github.com/howardpang/androidNativeBundle), it's hard to config and use in newer android studio without this plugin
