# 生命周期

### 不同场景生命周期钩子函数执行顺序

组件嵌套情况：祖组件 => 父组件 => 子组件

#### 1.启动：

* <mark style="color:purple;">grand father beforeCreate</mark>
* <mark style="color:purple;">grand father created</mark>
* <mark style="color:purple;">grand father beforeMount</mark>
* <mark style="color:orange;">father beforeCreate</mark>
* <mark style="color:orange;">father created</mark>
* <mark style="color:orange;">father beforeMount</mark>
* <mark style="color:green;">son beforeCreate</mark>
* <mark style="color:green;">son created</mark>
* <mark style="color:green;">son beforeMount</mark>
* <mark style="color:green;">son mounted</mark>
* <mark style="color:orange;">father mounted</mark>
* <mark style="color:purple;">grand father mounted</mark>

#### 2.卸载父组件：

* <mark style="color:purple;">grand father beforeUpdate</mark>
* <mark style="color:orange;">father beforeUnmount</mark>
* <mark style="color:green;">son beforeUnmount</mark>
* <mark style="color:green;">son unmounted</mark>
* <mark style="color:orange;">father unmounted</mark>
* <mark style="color:purple;">grand father updated</mark>

#### 3.挂载父组件

* <mark style="color:purple;">grand father beforeUpdate</mark>
* <mark style="color:orange;">father beforeCreate</mark>
* <mark style="color:orange;">father created</mark>
* <mark style="color:orange;">father beforeMount</mark>
* <mark style="color:green;">son beforeCreate</mark>
* <mark style="color:green;">son created</mark>
* <mark style="color:green;">son beforeMount</mark>
* <mark style="color:green;">son mounted</mark>
* <mark style="color:orange;">father mounted</mark>
* <mark style="color:purple;">grand father updated</mark>

#### 在线验证：[入口](https://sfc.vuejs.org/#eNrNVs1u00AQfpWpT63U2LS9pW4FqgQnTghOvjjxJnZr71q767QoioQQBxAVqIILUqVeQOXIqZe2b0MSOPEKzK4dx/lpSGyQuETe8cw3PzvfF3eNB3FsdhJi1A1bNHkQy32HBlHMuIQ2d6nXcqVPOLQ4i8AxTOuRMj7URhXnGLsOJSfa3yMtNwkldB0K0GQIQgmVop4aoIi3qSw9/O1huG3lmfEgSRSHriR4ArD9rf1nCRl+vOif3fbPvg7OL37dnA7efOjfvBi8u+y/vuq//za4+DI8f2tb6KtjinVbaLKtAqaxaaTt1SI3Ng8Fo9i6LtDJXgjHyEt2DN1jHR98KWNRtyzRaqrGD4XJeNvCJ5MnVAYRMYmIag3OjgWO5hBRdJMZhoXGDuE1TqhHOOGLMKdcZ3D17HB02MrUbahbnJyfF3RAyOch2XOMBuMIWIet+AQECwMPOPF2IXY9L6DtOmzfi08cQ8elk+92IRJt6PXy2aaI2SMeGomUjML9Zhg0jzCFj+WE5ECd1ltuKMgGAg4vr39++pxeyPD61ffrK9tKA5cDkjzROIPTlz9ubxfg2Na4ODtbgE4taCGe8NnxgR+EHuLYVvounVAWM7EkM1SYZkE5AkztPkDMGd4/dNOT50p3fWPkzIlMOB2dQN2EWpnicucp1vJlA8g7rYMaXGZXPBtlbZAW4+SAE2x2nK/JKC4FMUPWXs/SjNouBjjGRgGqqW3eUiiZ7yRACv2YIYVWKEX7TwJFyrRkJZnvvEqexngLq0wlDZiESrRtuVoy37m1UF3oKsWkEVPVpMZl6xl5T42XSJ9541Uu8lNtXA4NIP1AmPkWwh6sramTBhvBzZF+VLPyQtbmhNApKduFyOXtgNYki2fEbXtC3Larihv+jVRXtrtAJmQNneZrGr5YQdAUTK5mTxjNpWxpMUOEakr270WsqnxVFK6KklVVrKrKVGWB+gvS9B+IUkaOWUXydxYIUhzQo9lPq6Lm7NzN0XkMLEEwxfE57FqVRQqmNIV0DSX5M068OnlUbGnmjBOXoI0KLs+ZQupShNHZ/8SWeYve+w3fcM7Y)
