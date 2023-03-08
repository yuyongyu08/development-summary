# diff算法

Virtual-DOM&#x20;

节点：

* type：bian qiabianqia
* props：
* children：



核心点：

* 节点只在同层对比
* 新旧虚拟DOM采用双指针标记，节点对比顺序：头头对比、尾尾对比、头尾对比、尾头对比
* 节点相同的判断条件：key相同 && tag相同（data？） && 不是注释节点
* <mark style="color:red;">diff过程边对比边操作真实DOM</mark>
* 操作DOM的类型：增加节点、删除节点、更新节点



面试题：分别说下用index作为key和使用其他唯一id做为key的diff过程

```JavaScript
oldVnode：A B C
newVnode：A D B C
```





v-for时使用数组的index作为key时的问题：

* diff效率低
* 数据错位：[演示](https://sfc.vuejs.org/#eNplUs1u1DAQfpWRL7srZW1acYCQVnBH4sCx7iGbOMVbx7b8swhFkbgCoic4VZXgBRA3EPA43fAajJM2rcRtxvP5m2++mY48s5buoiA5KXzlpA3gRYj2mGvZWuMCdOBEAz00zrSwQOiCa66VQGCItdDhufQBjhJqecI1QCfrHA4y0GUrcljs/3y5/vlukUF5hunBoz6bQYczaLi62F9ezqDHPdenqycJyHUTdRWk0VDW9cup5XIFXSpWRmPvGx0vNluUMRI/nIn/Xny4/vXplvjwQT+S3lNOd6WKAj+e3NFkQCn9D3PKNcoq2GQTGoRJEK1VZRCYARS13EGlSu+POHkllDKcjAUsRXUTYawk7NaNcYhaSmTIQK5A6vuqOIH8XLxBhESOroOEo2km6PtCahsDsOOCKXnbgM0dio2boxgCGve0UrI6R7I7B5F1+PF7/x5383a4+jp8/j58/Faw6cM0DcNxMCrYPCTJyHQU67a0dOuNxrMZF4E6x4LnJJ9Wk97wWFKOZoRgfc6Yb6p0bFtPjTtjGFEXdZCtoMK3640zr71wSMxJokC3e9L/A2Tp7Oo=)



参考：

* [https://vue3js.cn/interview/vue/diff.html](https://vue3js.cn/interview/vue/diff.html)
* [https://www.cnblogs.com/yingzi1028/p/16647253.html](https://www.cnblogs.com/yingzi1028/p/16647253.html)

