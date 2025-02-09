### 介绍

### 安装配置

通过 windows 包管理器命令行工具 `winget` 安装 `fnm` :

```shell
winget install Schniz.fnm --source winget
```

如果在使用 `fnm` 命令时出现：

```shell
error: We can't find the necessary environment variables to replace the Node version.
You should setup your shell profile to evaluate `fnm env`, see https://github.com/Schniz/fnm#shell-setup on how to do this
Check out our documentation for more information: https://fnm.vercel.app
```



```shell
fnm env --use-on-cd | Out-String | Invoke-Expression
```

