# 6-symbol

* 不支持语法："`new Symbol()`" (原始数据类型创建一个显式包装器对象从 ECMAScript 6 开始不再被支持，不过`new Boolean`、`new String`以及`new Number`由于历史遗留仍然允许）
* 每个从 `Symbol()` 返回的 symbol 值都是唯一的



常见应用：作为对象的key，[手写apply](../han-shu/apply-call-bind.md#yi-apply)就有用到



