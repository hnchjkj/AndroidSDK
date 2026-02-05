# Android 支付SDK 接入文档

## 一、概述
### 使用前，先阅读并参考[Android SDK 接入指引](README.md)引入
- `CJPaySdk` 是支付 SDK 的统一入口类，负责支付模块的初始化及支付流程的启动。
- 支付功能依赖登录 SDK，请确保用户在支付前已完成登录。

---

## 二、初始化说明

```kotlin
CJPaySdk.init()
```

#### 注意事项
- 初始化时机请参考[Android SDK 接入指引](README.md)
- 初始化完成前不可发起支付
- 可通过 `CJPaySdk.isInit` 判断初始化状态

---

## 三、发起支付

### 3.1 创建支付请求

```kotlin
CJPaySdk.startPayment(activity)
                .setParams(
                    payMode,
                    customParams,
                    productId,
                    productName,
                    currency,
                    amount,
                    quantity,
                    orderDesc
                ).payment()
```

#### 参数说明

| 参数名 | 类型 | 说明 |
|------|------|------|
| activity | FragmentActivity | 当前页面 Activity（必须） |
| payMode| PayMode | 支付类型（必须） |
| customParams| String | 回传标识，例如订单ID（必须） |
| productId| String | Google的商品ID（必须） |
| productName| String | 商品名（必须） |
| currency| String | 货币代码（必须） |
| amount| String | 单价（必须） |
| quantity| Int | 数量（必须） |
| orderDesc| String | 订单描述（必须） |

枚举类 `PayMode` 包括 `GOOGLE_PAY` `THIRD_PARTY_PAY` 两种

---

## 四、典型接入示例

```kotlin
class App : Application() {

    private val mSdkCoreStateListener = object : SdkCoreStateListener {
        override fun onInitSuccess() {
            CJPaySdk.init()
        }

        override fun onInitFailed(code: Int, msg: String) {
        }
    }
}
```

---

## 五、注意事项

- 支付 SDK 依赖登录 SDK，请确保用户已登录
- 请勿重复调用 `init()` 方法
