OpenCV4Android
======

[ ![Download](https://api.bintray.com/packages/wanghonglin/maven/opencv-with-header/images/download.svg) ](https://bintray.com/wanghonglin/maven/opencv-with-header/_latestVersion)

This project is created from [opencv](https://github.com/opencv/opencv), with the helper script from [eclipse2as.sh](https://github.com/WanghongLin/miscellaneous/blob/master/tools/eclipse2as.sh)

Use OpenCV in your Android studio project
-----------------------------------------

You can either apply dependency in your project or build aar manually

##### Use the published version from jcenter
```groovy
implementation 'com.wanghong.opencv:opencv-with-header:3.1.0-dev'
```

##### Or build and use AAR manually

* build aar
```shell
$ ./gradlew build
# the aar will output to opencv/build/outputs/aar/opencv-debug.aar
# or opencv/build/outputs/aar/opencv-release.aar depends on your different build flavor
# the aar also contain headers
```

* add aar as a dependency to your project
```gradle
allprojects {
    repositories {
        jcenter()

        flatDir {
            dirs '/path/to/aar'
        }
    }
}

// in your app's build.gradle
dependencies {
    // ...
    compile 'org.opencv:opencv-debug@aar'
    // ...
}
```

##### Use this library and start develop your OpenCV app
* create a reference in your `CMakeLists.txt` if you use `cmake` build system

```cmake

add_library(opencv
            SHARED
            IMPORTED)

set_target_properties(opencv
    PROPERTIES IMPORTED_LOCATION
    ../../../../build/intermediates/exploded-aar/org.opencv/opencv-with-header-3.1.0-dev/jni/${ANDROID_ABI}/libopencv_java3.so
)

target_link_libraries( # Specifies the target library.
                       native-lib
                       opencv )
```

* Enjoy!

Troubleshoot
------------
* `gnustl_static` has been removed started from ndk r18, so make sure you use ndk version before r18 release.
