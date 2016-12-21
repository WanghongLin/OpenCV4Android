# OpenCV4Android
created from https://github.com/opencv/opencv

with the helper script https://github.com/WanghongLin/miscellaneous/blob/master/tools/eclipse2as.sh

#### Use opencv in your Android studio project
* build aar
```shell
$ ./gradlew aarWithHeadersDebug
# the aar will output to opencv/build/outputs/aar/opencv-with-header-3.1.0-dev.aar
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
    compile 'org.opencv:opencv-with-header-3.1.0-dev@aar'
    // ...
}
```

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

* Finish
