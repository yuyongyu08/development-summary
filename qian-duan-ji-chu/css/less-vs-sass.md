---
description: CSS 预处理器
---

# Less vs Sass

## 一、**Less：**

* **Variables**
* **Mixins**
* **Nesting**
* **Operations**
* `Escaping`
* Functions
* Namespaces
* Maps
* Scope
* Comments
* Importing

## 二、S**ass：**

* **Variables**
* **Nesting**
* Partials
* Modules
* **Mixins**
* Extends/Inheritance
* **Opterators**

\
\
Sass中M**ixins 与 Extend的区别？**

* 语义：
  * mixin是混入，将css片段植入目标区域，编译后**会**产生重复的css片段
  * extend是扩展（继承），共用css片段，编译后**不会**产生重复的css片段
*   语法：

    * mixin：

    ```css
    @mixin theme($theme: DarkGray) {
      background: $theme;
      box-shadow: 0 0 1px rgba($theme, .25);
      color: #fff;
    }

    .info {
      @include theme;
    }
    .alert {
      @include theme($theme: DarkRed);
    }
    ```

    * extend：

    ```css
    %message-shared {
      border: 1px solid #ccc;
      padding: 10px;
      color: #333;
    }

    .success {
      @extend %message-shared;
      border-color: green;
    }

    .error {
      @extend %message-shared;
      border-color: red;
    }
    ```
* 灵活度：
  * mixin：可以接受参数，灵活度高，类似函数
  * extend：无法传参，单纯的CSS片段

\
二者功能相同，都是为了实现css片段的复用。<mark style="color:green;">如果不需要传参，建议用extend</mark>。











