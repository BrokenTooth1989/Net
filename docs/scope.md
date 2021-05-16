Net的网络请求本身支持在官方的自带的作用域内使用, 但是考虑到完整的生命周期和错误处理等推荐使用Net内部定义的作用域.

<br>
全部使用顶层扩展函数


## 异步任务的作用域

快速创建可以捕捉异常的协程作用域, 以下作用域不会触发全局错误处理

|函数|描述|
|-|-|
|`scope`|创建最基础的作用域, 所有作用域都包含异常捕捉|
|`scopeLife`|创建跟随生命周期取消的作用域|
|`ViewModel.scopeLife`|创建跟随`ViewModel`生命周期的作用域|


## 网络请求的作用域

网络请求的作用域可以根据生命周期自动取消网络请求, 发生错误也会自动弹出吐司(可以自定义或者取消), 并且具备一些场景的特殊功能(例如加载对话框, 缺省页, 下拉刷新等)

以下作用域会触发全局错误处理

| 函数 | 描述 |
|-|-|
|`scopeNet`|创建自动处理网络错误的作用域|
|`scopeNetLife`|创建自动处理网络错误的作用域, 且包含跟随Activity或者Fragment生命周期|
|`scopeDialog`|创建自动加载对话框的作用域, 生命周期跟随对话框|
|`ViewModel.scopeNetLife`|创建跟随`ViewModel`生命周期的作用域|
|`PageRefreshLayout.scope`|创建跟随[PageRefreshLayout](https://github.com/liangjingkanji/BRV)生命周期的作用域|
|`StateLayout.scope`|创建跟随[StateLayout](https://github.com/liangjingkanji/BRV)生命周期的作用域|

<br>

> PageRefreshLayout/StateLayout 属于[BRV](https://github.com/liangjingkanji/BRV)框架中的布局, 用于支持[自动化缺省页/下拉刷新](auto-state.md)
<br>

## 捕捉异常/执行完成
```kotlin
scope {
    // scope系列函数的这个大括号里面就是作用域
}.catch {
    // 协程内部发生错误回调, it为异常
    handleError(it) // 该函数会将错误再次传递给全局错误回调处理
}.finally {
    // 协程内全部执行完成回调(包括子协程), it为异常(如果正常完成则为null)
}
```

以下函数幕后字段`it`为异常对象

| 函数 | 描述 |
|-|-|
| catch | 作用域被`catch`则不会被传递到全局异常处理回调中: [全局处理异常](error-handle.md), 除非使用`handleError`再次传递给全局 |
| finally | 同样可以获取到异常对象, 且不影响全局异常回调处理 |


> 如果想了解详细的协程使用方式, 可以查看我的一篇文章: [最全面的Kotlin协程: Coroutine/Channel/Flow 以及实际应用](https://juejin.im/post/6844904037586829320)



