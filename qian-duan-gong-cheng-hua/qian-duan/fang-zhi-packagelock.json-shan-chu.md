---
description: package
---

# 防止package-lock.json删除

借助 [husky](https://typicode.github.io/husky/getting-started.html)通过git hook 进行限制，pre-commit内容如下：

```
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

#定义颜色变量
RED='\033[31m'      # 红
GREEN='\033[32m'    # 绿
RES='\033[0m'       # 清除颜色

# 获取本次提交的文件列表
changed_files=$(git diff --name-only HEAD)

# 检查 package.json 和 package-lock.json 是否发生变化
package_lock_json_changed=$(echo "${changed_files}" | grep -q "package-lock.json" && echo 1 || echo 0)
package_json_changed=$(echo "${changed_files}" | grep -q "package.json" && echo 1 || echo 0)

if [ $package_lock_json_changed -eq 1 ] && [ $package_json_changed -eq 0 ]; then
    echo "${RED} [hook]pre-commit 校验失败: package-lock.json 发生了变化，但 package.json 没有变化，不允许提交。${RES}"
    exit 1
else
    echo "${GREEN} [hook]pre-commit 校验通过，开始提交文件 ${RES}"
    exit 0
fi

```
