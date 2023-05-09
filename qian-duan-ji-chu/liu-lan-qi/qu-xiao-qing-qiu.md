# 取消请求

## 一、XMLHttpRequest

用<mark style="color:red;">**xhr.abort()**</mark>取消

```markup
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <h2>XMLHttpRequest取消请求用xhr.abort()</h2>
    <script>
      const xhr = new XMLHttpRequest();
      xhr.open("GET", "http://localhost:8000/topics/cancle-request/xhr.html", true);
      xhr.send();
      setTimeout(() => {
        xhr.abort();
      }, 0);
    </script>
  </body>
</html>
```

## 二、fetch

借助[`AbortController`](https://developer.mozilla.org/zh-CN/docs/Web/API/AbortController)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>fetch</title>
  </head>
  <body>
    <h2>fetch取消请求用AbortController.abort()</h2>
    <script>
      const controller = new AbortController();
      void (async function () {
        const response = await fetch("http://localhost:8000/topics/cancle-request/fetch.html", {
          signal: controller.signal,
        });
        const data = await response.json();
      })();
      setTimeout(() => {
        controller.abort();
      }, 0);
    </script>
  </body>
</html>

```

> axios进行取消请求也是借助AbortController.abort()

