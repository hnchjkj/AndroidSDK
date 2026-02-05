# 海外游戏 Android SDK 接入文档

## 1、写在开头
本文档将向您说明 **海外游戏 Android SDK** 的接入方式及使用说明。

### 相关库清单
```text
core       // 核心库，必须引用
login      // 登录库，按需引用
pay        // 支付库，按需引用（依赖登录库）
service    // 客服库，按需引用（依赖登录库）
```

---

## 2、引入工程
SDK 通过 **Gradle** 形式进行引用，请按需添加对应 **SDK** 至工程。

### 2.1 添加镜像配置
```gradle
dependencyResolutionManagement {
    repositories {
        maven ( url= "https://raw.githubusercontent.com/hnchjkj/AndroidSDK/main/" )
    }
}
```

### 2.2 Gradle 配置
在 `app/build.gradle` 中添加如下配置：

```gradle
dependencies {
    implementation("com.hncj.sdk:core:1.0.3")      // 核心库，必须引用
    implementation("com.hncj.sdk:login:1.0.3")     // 登录库，按需引用
    implementation("com.hncj.sdk:pay:1.0.3")       // 支付库，按需引用（依赖登录库）
    implementation("com.hncj.sdk:service:1.0.3")   // 客服库，按需引用（依赖登录库）
}
```

### 2.3 当前版本：1.0.3

---

## 3、SDK 初始化（必须）

SDK 必须在 **Application** 中完成初始化，否则将导致功能不可用。

### 3.1 Application 初始化示例（Kotlin）

```kotlin
class App : Application() {

    private val mSdkCoreStateListener = object : SdkCoreStateListener {
        override fun onInitSuccess() {
            // TODO 请务必在Core库初始化成功回调中初始化其他模块，具体请查看相关文档

        }

        override fun onInitFailed(code: Int, msg: String) {
        }
    }

    override fun onCreate() {
        super.onCreate()

        CJSdkCore.init(
            application = this,
            appKey = "your_app_key",
            appSecret = "your_app_secret",
            sdkCoreStateListener = mSdkCoreStateListener,
            isDebug = true, // 可选，正式环境不建议开启
            debugLevel = Log.ERROR // 可选，默认ERROR
        )
    }
}
```

---

## 4、如何使用

### 4.1 登录 SDK
登录模块用于用户身份认证，是支付和客服功能的基础模块。

[登录 SDK 使用说明](LOGIN.md)

---

### 4.2 支付 SDK
支付功能依赖登录模块，请确保用户已完成登录。

[支付 SDK 使用说明](PAY.md)

---

### 4.3 客服 SDK
客服模块依赖登录态，可用于在线客服、问题反馈等场景。

[客服 SDK 使用说明](SERVICE.md)

---

## 5、注意事项

- SDK 初始化需在 **主进程** 中调用  
- 请确保在调用支付、客服接口前用户已登录   
- SDK 仅支持 Android 6.0（API 24）及以上系统  
