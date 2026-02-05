# Android 登录SDK 账号管理模块说明文档

## 一、概述
### 账号管理模块提供各第三方账号的绑定与解绑功能。

---

## 二、初始化说明
### 阅读并参考[Android 登录SDK 接入文档](LOGIN.md)

#### 注意事项
- 可通过 `CJAuthSdk.isInit` 判断初始化状态

---

## 三、使用账号管理

### 3.1 拉起账号管理页面

```kotlin
CJAuthSdk.startAccountManagement(context)
```

#### 参数说明

| 参数名 | 类型 | 说明 |
|------|------|------|
| context | Context | 上下文（必须） |

---

## 四、注意事项

- 请确保用户打开账号管理页面前已登录（包括游客登录）
