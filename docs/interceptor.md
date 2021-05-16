拦截器(Interceptor)一般用于修改请求的参数或者进行请求转发/重试. Net就是使用的OkHttp的拦截器. 所以支持市面上的所有OkHttp拦截器组件库
<br>

> 你的业务可能需要请求参数加密或者拼接一串特殊含义的参数, 或者响应信息需要解密. 请不要一上来就封装Post或者Get等请求函数(这是愚蠢的做法), 自定义拦截器和转换器可以应对任何项目需求.


```kotlin
class App : Application() {
    override fun onCreate() {
        super.onCreate()

        initNet("http://github.com/") {
            addInterceptor { chain -> chain.proceed(chain.request()) }
        }
    }
}
```

## 请求拦截器

RequestInterceptor属于轻量级的请求拦截器, 在每次请求的时候该拦截器都会被触发. 一般用于添加全局的参数和请求头

初始化时添加请求拦截器的示例代码

```kotlin
initNet("http://github.com/") {
    setRequestInterceptor(object : RequestInterceptor {
        override fun interceptor(request: BaseRequest) {
            request.param("client", "Net")
            request.setHeader("token", "123456")
        }
    })
}
```

可以看到`setRequestInterceptor`是set开头. 仅支持一个请求拦截器, 不像`addInterceptor`支持多个请求拦截器