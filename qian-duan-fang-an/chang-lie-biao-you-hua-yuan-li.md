# 长列表优化原理



**核心原理**：根据滚动的偏移量，计算出需要渲染的起始索引，只渲染其实索引之间的列表项

待优化

* 列表项如果不定高如何处理？
* 滚动过快有白屏

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

参见：

* [https://zhuanlan.zhihu.com/p/444778554](https://zhuanlan.zhihu.com/p/444778554)
