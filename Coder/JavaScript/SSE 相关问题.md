### 页面隐藏时，重复请求

#### 问题描述

默认情况下，`fetchEventSource` 会在页面再次变成可见状态时重新请求。

#### 解决方案

将 `openWhenHidden` 设置为 `true` 保持请求的打开状态。
