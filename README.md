## HyperLPR3-License Plate Recognition Android SDK

[中文文档](README_CH.md)

High performance license plate recognition based on deep learning HyperLPR Android SDK implementation.

### Source Code Project

If you need to learn about the build steps in the source code of the project, you can go : [HyperLPR](https://github.com/szad670401/HyperLPR).

### Supporting Platform

- Android: arm64-v8a、armeabi-v7a

### Add Dependency

Add Jitpack dependencies to your Gradle configuration

```java
allprojects {
	repositories {
		...
		maven { url 'https://jitpack.io' }
	}
}
```

Add dependencies in build.gradle for projects where you need hyperlpr

```java
dependencies {
	  implementation 'com.github.HyperInspire:hyperlpr3-android-sdk:1.0.3'
}
```

### How to Use

#### Initialize  HyperLPR

Before implementing the license plate recognition algorithm, the initialization function needs to be executed, and the storage read and write permissions need to be opened in advance. Initialization is performed only once, usually when the program is started.

```Java
// License plate recognition algorithm configuration parameters
 HyperLPRParameter parameter = new HyperLPRParameter()
     .setDetLevel(HyperLPR3.DETECT_LEVEL_LOW)
     .setMaxNum(1)
     .setRecConfidenceThreshold(0.85f);
// Initialization (performed only once)
HyperLPR3.getInstance().init(this, parameter);
```

#### License plate recognition on an image

Bitmap is used as an example for license plate recognition

```Java
// Use Bitmap as picture parameter for license plate recognition
Plate[] plates =  HyperLPR3.getInstance().plateRecognition(bitmap, HyperLPR3.CAMERA_ROTATION_0, HyperLPR3.STREAM_BGRA);
for (Plate plate: plates) {
	// Print the detected license plate number
	Log.i(TAG, plate.getCode());
}

```
#### License plate recognition on an steam

License plate recognition using camera stream or file stream

```Java
// License plate recognition using a stream of NV21
Plate[] plates = HyperLPR3.getInstance().plateRecognition(data, previewSize.height, previewSize.width, HyperLPR3.CAMERA_ROTATION_270, HyperLPR3.STREAM_YUV_NV21);
```

#### Note

The Android-SDK of hyperlpr is currently in the testing phase. If you encounter any problems during use, please raise your questions in issues. PR welcome.