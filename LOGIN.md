# Android 登录SDK 接入文档

## 1、本文档将向您说明 Android 端 CJAuthSDK 的接入方式及使用说明
## 2、SDK 初始化（必须）
   需要在CJCore初始化成功之后调用  CJAuthSdk.init(mSdkLoginStateListener)
   需要在载体的Activity中创建一个监听器，用于监听登录，登出，注销 回调
    private val mSdkLoginStateListener = object : SdkLoginStateListener {
        
//登录成功
        override fun onLoginSuccess(loginResult: LoginResp) {
            ToastUtils.showShort(getString(com.hacj.sdk.login.R.string.login_success))
        }
//登录失败
        override fun onLoginFailed(code: Int, msg: String?) {
            ToastUtils.showShort("${getString(com.hacj.sdk.login.R.string.login_failed)}：${code} : ${msg}")
        }
// 登出成功
        override fun onLoginOutSuccess() {
            ToastUtils.showShort("退出登录")
        }

// 登出失败
        override fun onLoginOutOnFailed(code: Int, msg: String?) {
            ToastUtils.showShort("${getString(com.hacj.sdk.login.R.string.login_failed)}：${code} : ${msg}")
        }

// 注销成功
        override fun onDeactivateAccountSuccess() {

        }

//注销失败
        override fun oneDactivateAccountFailed(code: Int, msg: String?) {
            super.oneDactivateAccountFailed(code, msg)
        }
    }

## 3、登录调用 type 登录方式（支持游客，Google, Facebook, X, Line）   context 载体  必传
   CJAuthSdk.gameAuth(LoginType type, Context context)

## 4、调用登录页面 获取登录回调也是走初始化的监听
   CJAuthSdk.showLoginActivity()

## 5、邮箱验证码登录
   CJAuthSdk.sendEmailCode("邮箱地址","回调": SignInCallback)
   callback.onSuccessResult 发送成功
   callback.onFailure  发送失败

   CJAuthSdk.emailCodeLogin("邮箱地址": String, "邮箱验证码": String) 

## 6、账号登出 初始化监听器监听
   CJAuthSdk.loginOut()

## 7、账号注销 初始化监听器监听
   CJAuthSdk.deactivateAccount()
