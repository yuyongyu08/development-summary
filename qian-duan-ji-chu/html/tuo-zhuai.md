# 拖拽

* dragstart：事件主体是被拖放元素，在开始拖放被拖放元素时触发。
* **drag**：事件主体是被拖放元素，在正在拖放被拖放元素时触发。
* dragenter：事件主体是目标元素，在被拖放元素进入某元素时触发。
* dragover：事件主体是目标元素，在被拖放在某元素内移动时触发。
* dragleave：事件主体是目标元素，在被拖放元素移出目标元素是触发。
* **drop**：事件主体是目标元素，在目标元素完全接受被拖放元素时触发。
* dragend：事件主体是被拖放元素，在整个拖放操作结束时触发。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      body {
        font-family: "Benton Sans", "Helvetica Neue", helvetica, arial, sans-serif;
        margin: 2em;
      }

      .container {
        display: grid;
        grid-template-columns: repeat(5, 1fr);
        gap: 10px;
      }

      .box {
        border: 3px solid #666;
        background-color: #ddd;
        border-radius: 0.5em;
        padding: 10px;
        cursor: move;
      }

      .box.over {
        border: 3px dotted #666;
      }

      [draggable] {
        user-select: none;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <div draggable="true" class="box">A</div>
      <div draggable="true" class="box">B</div>
      <div draggable="true" class="box">C</div>
    </div>

    <script>
      document.addEventListener("DOMContentLoaded", (event) => {
        var dragSrcEl = null;

        function handleDragStart(e) {
          this.style.opacity = "0.4";

          dragSrcEl = this;

          e.dataTransfer.effectAllowed = "move";
          e.dataTransfer.setData("text/html", this.innerHTML);
        }

        function handleDragOver(e) {
          if (e.preventDefault) {
            e.preventDefault();
          }

          e.dataTransfer.dropEffect = "move";

          return false;
        }

        function handleDragEnter(e) {
          this.classList.add("over");
        }

        function handleDragLeave(e) {
          this.classList.remove("over");
        }

        function handleDrop(e) {
          if (e.stopPropagation) {
            e.stopPropagation(); // stops the browser from redirecting.
          }

          if (dragSrcEl != this) {
            dragSrcEl.innerHTML = this.innerHTML;
            this.innerHTML = e.dataTransfer.getData("text/html");
          }

          return false;
        }

        function handleDragEnd(e) {
          this.style.opacity = "1";

          items.forEach(function (item) {
            item.classList.remove("over");
          });
        }

        let items = document.querySelectorAll(".container .box");
        items.forEach(function (item) {
          item.addEventListener("dragstart", handleDragStart, false);
          item.addEventListener("dragenter", handleDragEnter, false);
          item.addEventListener("dragover", handleDragOver, false);
          item.addEventListener("dragleave", handleDragLeave, false);
          item.addEventListener("drop", handleDrop, false);
          item.addEventListener("dragend", handleDragEnd, false);
        });
      });
    </script>
  </body>
</html>
```
