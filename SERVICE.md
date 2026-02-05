# Android 客服SDK 接入文档

## 一、概述
### 使用前，先阅读并参考[Android SDK 接入指引](README.md)引入
- `CJServiceSdk` 是客服 SDK 的统一入口类，负责客服模块的初始化及具体页面的启动。
- 客服功能依赖登录 SDK，请确保用户在拉起客服页面前已完成登录。

---

## 二、初始化说明

```kotlin
CJServiceSdk.init()
```

#### 注意事项
- 初始化时机请参考[Android SDK 接入指引](README.md)
- 初始化完成前不可拉起客服页面
- 可通过 `CJServiceSdk.isInit` 判断初始化状态

---

## 三、使用客服

### 3.1 拉起客服页面

```kotlin
CJServiceSdk.startFeedback(context)
```

#### 参数说明

| 参数名 | 类型 | 说明 |
|------|------|------|
| context | Context | 上下文（必须） |

---

## 四、典型接入示例

```kotlin
class App : Application() {

    private val mSdkCoreStateListener = object : SdkCoreStateListener {
        override fun onInitSuccess() {
            CJServiceSdk.init()
        }

        override fun onInitFailed(code: Int, msg: String) {
        }
    }
}
```

---

## 五、注意事项

- 客服 SDK 依赖登录 SDK，请确保用户已登录
- 请勿重复调用 `init()` 方法
