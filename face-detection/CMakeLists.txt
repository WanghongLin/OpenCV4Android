

cmake_minimum_required(VERSION 2.8.2)

add_library(detection_based_tracker
	SHARED
	src/main/cpp/DetectionBasedTracker_jni.cpp
)

find_library(lib-log log)
find_library(lib-dl dl)

add_library(opencv-lib
    SHARED
    IMPORTED
)
set_target_properties(opencv-lib
    PROPERTIES IMPORTED_LOCATION
    ../../../../../opencv/src/main/jniLibs/${ANDROID_ABI}/libopencv_java3.so
    )

include_directories(../opencv/src/main/cpp/include)

target_link_libraries(detection_based_tracker
    opencv-lib
	${lib-log}
	${lib-dl}
	)

