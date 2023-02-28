---
description: 各个阶段生命周期钩子函数
---

# 生命周期

### 一、组件嵌套时执行顺序

嵌套情况：祖组件 => 父组件 => 子组件

#### 1.启动：

1. <mark style="color:purple;">grand father beforeCreate</mark>
2. <mark style="color:purple;">grand father created</mark>
3. <mark style="color:purple;">grand father beforeMount</mark>
4. <mark style="color:orange;">father beforeCreate</mark>
5. <mark style="color:orange;">father created</mark>
6. <mark style="color:orange;">**father beforeMount**</mark>
7. <mark style="color:green;">son beforeCreate</mark>
8. <mark style="color:green;">son created</mark>
9. <mark style="color:green;">son beforeMount</mark>
10. <mark style="color:green;">son mounted</mark>
11. <mark style="color:orange;">**father mounted**</mark>
12. <mark style="color:purple;">grand father mounted</mark>

#### 2.卸载父组件：

1. <mark style="color:purple;">grand father beforeUpdate</mark>
2. <mark style="color:orange;">**father beforeUnmount**</mark>
3. <mark style="color:green;">son beforeUnmount</mark>
4. <mark style="color:green;">son unmounted</mark>
5. <mark style="color:orange;">**father unmounted**</mark>
6. <mark style="color:purple;">grand father updated</mark>

#### 3.挂载父组件

1. <mark style="color:purple;">grand father beforeUpdate</mark>
2. <mark style="color:orange;">father beforeCreate</mark>
3. <mark style="color:orange;">father created</mark>
4. <mark style="color:orange;">**father beforeMount**</mark>
5. <mark style="color:green;">son beforeCreate</mark>
6. <mark style="color:green;">son created</mark>
7. <mark style="color:green;">son beforeMount</mark>
8. <mark style="color:green;">son mounted</mark>
9. <mark style="color:orange;">**father mounted**</mark>
10. <mark style="color:purple;">grand father updated</mark>



**结论：**beforeMount之后开始示例化子组件

#### 在线验证：[入口](https://sfc.vuejs.org/#eNrNVs1u00AQfpWpT63U2LS9pW4FqgQnTghOvjjxJnZr71q767QoioQQBxAVqIILUqVeQOXIqZe2b0MSOPEKzK4dx/lpSGyQuETe8cw3PzvfF3eNB3FsdhJi1A1bNHkQy32HBlHMuIQ2d6nXcqVPOLQ4i8AxTOuRMj7URhXnGLsOJSfa3yMtNwkldB0K0GQIQgmVop4aoIi3qSw9/O1huG3lmfEgSRSHriR4ArD9rf1nCRl+vOif3fbPvg7OL37dnA7efOjfvBi8u+y/vuq//za4+DI8f2tb6KtjinVbaLKtAqaxaaTt1SI3Ng8Fo9i6LtDJXgjHyEt2DN1jHR98KWNRtyzRaqrGD4XJeNvCJ5MnVAYRMYmIag3OjgWO5hBRdJMZhoXGDuE1TqhHOOGLMKdcZ3D17HB02MrUbahbnJyfF3RAyOch2XOMBuMIWIet+AQECwMPOPF2IXY9L6DtOmzfi08cQ8elk+92IRJt6PXy2aaI2SMeGomUjML9Zhg0jzCFj+WE5ECd1ltuKMgGAg4vr39++pxeyPD61ffrK9tKA5cDkjzROIPTlz9ubxfg2Na4ODtbgE4taCGe8NnxgR+EHuLYVvounVAWM7EkM1SYZkE5AkztPkDMGd4/dNOT50p3fWPkzIlMOB2dQN2EWpnicucp1vJlA8g7rYMaXGZXPBtlbZAW4+SAE2x2nK/JKC4FMUPWXs/SjNouBjjGRgGqqW3eUiiZ7yRACv2YIYVWKEX7TwJFyrRkJZnvvEqexngLq0wlDZiESrRtuVoy37m1UF3oKsWkEVPVpMZl6xl5T42XSJ9541Uu8lNtXA4NIP1AmPkWwh6sramTBhvBzZF+VLPyQtbmhNApKduFyOXtgNYki2fEbXtC3Larihv+jVRXtrtAJmQNneZrGr5YQdAUTK5mTxjNpWxpMUOEakr270WsqnxVFK6KklVVrKrKVGWB+gvS9B+IUkaOWUXydxYIUhzQo9lPq6Lm7NzN0XkMLEEwxfE57FqVRQqmNIV0DSX5M068OnlUbGnmjBOXoI0KLs+ZQupShNHZ/8SWeYve+w3fcM7Y)

### 二、\<KeepAlive>的情况

#### 1.初始化

![](<../../../.gitbook/assets/image (4) (3).png>)

#### 2.切走

![](<../../../.gitbook/assets/image (2).png>)

#### 3.切回

<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

**结论**：

* 挂载时，mounted后再activated
* 切走的时候先加载新组件，再缓存旧组件：不执行unmount相关钩子，而是deactivated
* 切回的时候不再执行create和mount相关钩子，而是activated

所以keep-alive是对组件实例的缓存，无需重新渲染

**在线验证**：[入口](https://sfc.vuejs.org/#eNrNVT9z0zAU/yrCS9u71qaMrtuj16lwbLB5ceyXxMWWdJKSppfzJ+COiYGBiWNkZmCAb9PyMXiSbNkJoUk0dfFJz78/z/L72cvgkvNwPoMgDhKZi5IrIkHN+EVKy5ozocg1LWBBxoLVJA3CyGw1Iw3OUprSJLI0JOBGQc2rTAHuCEkMNsJ1ErkbwXFghU/qjIc3klG0Xmp42t6QaRATU9E14xTjYqoUl3EUyXGu7W9kyMQkwlUoZlSVNYQg65ORYLcSBAqnwfFAI8LiHMSJAOxJgHhMcw36j66WbVLa4KO409Dnt/rwRTknUt1VcJ4GIyZQKianfEEkq8qCCCjOCM+KoqSTmLx4zhdpYHjInJ5eLJeklhPSNEmEu7b+GoBfVuXcGphSzvDIKFBF4lKi0byEWxRKInejI0frbN1gLzSaKcUoeZlXZf4ehaYZLSq40rvDA8XqgyOUvf/86+Hbz7esTiKL35F/A0LcDRRe6f2aRhJ1/XSrwdDgxk1ZO5bYUz+U2JIbyfa+8ewRxtJhYGEwBYyzWaXssLkTk2760KOdIaNm1o25csFwcMjS7opMZYdHHUtgfgTtdkS/SD1r99+//vn98f7Tj4cvH7BfggdETFfP3KQSot+fBqOzqzbYcOc7gjETcCUAT6V3zBnFqYKwYpNDTJEJ7BCZBkcDjdzUisfpLWiVaTXfMMzbLuYGuKpQ69I27xa0yfsdx7Pe6cktclVjZmpb3FvQRndqWtvJ3kLX/G1xawcdbO3sQE1Z0U/nMGJ6bpwmDu60lKGukXMzUkal09FXPVODLzd+ydoI7fsdmwgAegdVxW73+55tSfmmhHqE7vqgJvhkfcT2DZNOqneUNNk3SL3x/jHSXO8Q9cYeEdJk/wANrL3iY9w3hyfLVTnf1rkDrXIL2Ik9gP0vuJuj5/5NXuF7qrFb+7ftGzxD94+epfuGb2i+f/ws2zuAQ3OPCFq6fwhX7L1i2HbgGUTL9o+i5XuGsfkLCwRblg==)

****
