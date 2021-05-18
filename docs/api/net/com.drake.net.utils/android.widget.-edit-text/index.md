[net](../../index.md) / [com.drake.net.utils](../index.md) / [android.widget.EditText](./index.md)

### Extensions for android.widget.EditText

| Name | Summary |
|---|---|
| [debounce](debounce.md) | 为EditText的输入框文本变化启用节流阀, 即超过指定时间后(默认800毫秒)的输入框文本变化事件[TextWatcher.onTextChanged](https://developer.android.com/reference/android/text/TextWatcher.html#onTextChanged(java.lang.CharSequence, int, int, int))会被下游收集到`fun `[`EditText`](https://developer.android.com/reference/android/widget/EditText.html)`.debounce(timeoutMillis: `[`Long`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-long/index.html)` = 800): Flow<`[`String`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-string/index.html)`>` |