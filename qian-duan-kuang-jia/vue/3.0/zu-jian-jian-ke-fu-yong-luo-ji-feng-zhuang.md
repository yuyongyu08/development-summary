---
description: 框架间横向对比
---

# 组件间可复用逻辑封装

目前前端主要是**面向组件开发**，但随着组件越来越多，如何优雅地抽离和组织**组件间可复用的逻辑**非常重要，每个框架及框架不同版本有不同的处理方式：

<table><thead><tr><th width="138">框架</th><th width="288">方式</th><th>实现方式</th><th>优点</th><th>缺点</th></tr></thead><tbody><tr><td>Vue 2.0</td><td><ul><li>mixin：mini版组件</li><li>directive：</li><li>plugin：Vue能力的扩展入口</li></ul></td><td><ul><li>mixin：</li></ul></td><td></td><td></td></tr><tr><td>Vue 3.0</td><td><ul><li>hooks</li><li>mixin（不推荐）</li><li>directive</li><li>plugin</li></ul></td><td></td><td></td><td></td></tr><tr><td>React 18</td><td><ul><li>hooks</li></ul></td><td></td><td></td><td></td></tr></tbody></table>









