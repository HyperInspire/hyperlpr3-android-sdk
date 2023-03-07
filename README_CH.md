## HyperLPR3-Android-SDK   HyperLPR3-车牌识别安卓SDK

基于深度学习高性能车牌识别HyperLPR的安卓SDK实现

### 源码工程

需要了解编译相关源码可移步到[HyperLPR工程](https://github.com/szad670401/HyperLPR)。

### 支持平台

- Android: arm64-v8a、armeabi-v7a

### 添加依赖

在你的Gradle配置中添加Jitpack依赖

```java
allprojects {
	repositories {
		...
		maven { url 'https://jitpack.io' }
	}
}
```

在你需要使用hyperlpr的项目中的build.gradle添加依赖

```java
dependencies {
	  implementation 'com.github.HyperInspire:hyperlpr3-android-sdk:1.0.2'
}
```

### 如何使用

#### 初始化HyperLPR

在执行车牌识别算法之前需要先执行初始化函数，需要提前开启存储读写权限；初始化仅需执行一次，通常在程序启动的时候执行。

```Java
// 车牌识别算法配置参数
 HyperLPRParameter parameter = new HyperLPRParameter()
     .setDetLevel(HyperLPR3.DETECT_LEVEL_LOW)
     .setMaxNum(1)
     .setRecConfidenceThreshold(0.85f);
// 初始化(仅执行一次生效)
HyperLPR3.getInstance().init(this, parameter);
```

#### 对一张图片进行车牌识别

采用Bitmap作为示例进行车牌识别

```Java
// 使用Bitmap作为图片参数进行车牌识别
Plate[] plates =  HyperLPR3.getInstance().plateRecognition(bitmap, HyperLPR3.CAMERA_ROTATION_0, HyperLPR3.STREAM_BGRA);
for (Plate plate: plates) {
	// 打印检测到的车牌号
	Log.i(TAG, plate.getCode());
}

```
#### 对流进行识别

通常可以传入相机流或文件流进行车牌识别

```Java
// 使用一段NV21的流进行车牌识别
Plate[] plates = HyperLPR3.getInstance().plateRecognition(data, previewSize.height, previewSize.width, HyperLPR3.CAMERA_ROTATION_270, HyperLPR3.STREAM_YUV_NV21);
```

#### 注意

hyperlpr的Android-SDK当前属于测试阶段，如果您在使用过程中遇到任何问题请在issues中提出你的问题，也很欢迎大家多提PR。