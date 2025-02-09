### 问题描述

在使用 `npm` 命令安装 `pnpm` 时，控制到输出错误：

```shell
npm : 无法加载文件 C:\Users\41261\AppData\Local\fnm_multishells\21172_1739087098551\npm.ps1，因为在此系统上禁止运行脚本
。有关详细信息，请参阅 https:/go.microsoft.com/fwlink/?LinkID=135170 中的 about_Execution_Policies。
所在位置 行:1 字符: 1
+ npm install -g pnpm
+ ~~~
    + CategoryInfo          : SecurityError: (:) []，PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess
```

### 解决方案

#### 查看执行策略/权限

```shell
get-ExecutionPolicy
```

如果控制台输出 `Restricted`，执行下一步。

#### 赋予权限

```shell
 Set-ExecutionPolicy -Scope CurrentUser
```

根据提示输入：

```shell
RemoteSigned
```
 
再次查看权限，控制台输出 `RemoteSigned`，即表示成功。