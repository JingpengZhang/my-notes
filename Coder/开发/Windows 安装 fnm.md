### 介绍

`fnm` 是基于 Rust 的 NodeJS 版本管理工具，可代替 Node Version Manager（`nvm`）。

### 安装配置

通过 windows 包管理器命令行工具 `winget` 安装 `fnm` :

```shell
winget install Schniz.fnm --source winget
```

如果在使用 `fnm` 命令时出现如下错误：

```shell
error: We can't find the necessary environment variables to replace the Node version.
You should setup your shell profile to evaluate `fnm env`, see https://github.com/Schniz/fnm#shell-setup on how to do this
Check out our documentation for more information: https://fnm.vercel.app
```

输入如下命令即可：

```shell
fnm env --use-on-cd | Out-String | Invoke-Expression
```


### 常用命令

- `fnm list-remote` - 查看可安装的 node 版本；
- `fnm list` - 查看已安装的 node 版本；
- `fnm install xxx` - 安装指定版本的 node，如果只指定了主版本号，将会安装该主版本最新的版本，如 `fnm install 22` 等于 `fnm install 22.13.1`；
- `fnm use` - 如果运行目录中存在 `.nvmrc` 文件，将会切换到文件中指定的 node 版本（前提是该版本已安装）；
- `fnm use xxx`- 切换到指定版本；